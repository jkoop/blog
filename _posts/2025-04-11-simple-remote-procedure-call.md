---
title: "Simple Remote Procedure Call"
description: A simple application-layer message-passing protocol
tags: api-schema
---

**Supersedes [SPJC][spjc]**

SRPC is a JSON-based RPC protocol for clients, like webpages, to call a server via a standardized JSON interface. It requires a carrier protocol, like HTTP.

The keywords SHOULD, MAY, MUST, etc. are defined in [RFC 2119][rfc2119].

## Scope

- Successful response
- Successful response with warnings
- Error response
- Access control is not handled by SRPC
- Request deduplication is not handled by SRPC
- Rate limiting is not handled by SRPC

## Comparison with SPJC

SPJC is a similar protocol, but it encourages bad practices in the client code.

- SPJC requires more complex code for both the server, and the client
- SPJC doesn't require any kind of error handling in the client
- SRPC doesn't describe any request aggregation or batching

## Schemas

### Request

```json
{
  "action": "string|undefined",
  "payload": "number|string|array|object|null"
  // all other properties are forbidden
}
```

### Response

```json
{
  "payload": "number|string|array|object|null|undefined",
  "error": "string|undefined",
  "warnings": "array<string>|undefined",
  "debug": "array<string|object>|undefined" // SHOULD not be used in a production environment

  // all other properties are forbidden
  // additionally, `payload`, and `error` are mutually exclusive, and at least one must be present
}
```

Clients MUST handle errors and warnings.

## Efficient Payload Encoding

This requires the carrier protocol to support Request and Response headers.

This spec does not describe a negotiation protocol; whether to use efficient payload encoding is an implementation detail.

When sending a large string, like a fragment of HTML, JSON-encoding it will cause it to expand in byte count by up to three times ($json \approx 3 \times plain$). To counter this, the sender MAY send the payload directly, without JSONizing it, if (and only if) there isn't an error, and there aren't any warnings or debug messages.

1. When sending only the payload, the sender MUST set a header to indicate that the payload is not JSONized: `X-SRPC-Raw-Payload: 1`.
2. The request `action` is moved to the `X-SRPC-Action` header.

## Implementation

Below are some example implementations of the SRPC client and server.

### Client

```js
// this reference code assumes a few functions are set:
// display_error_to_user(string) - display an error to the user
// display_warning_to_user(string) - display a warning to the user

/**
 * @param {string} path
 * @param {string|null} action
 * @param {number|string|array|object|null} payload
 * @returns {Promise<number|string|array|object|null|undefined>} the response payload or undefined if there was an error
 */
async function srpc(path, action, payload) {
  try {
    if (
      typeof payload == "string" &&
      payload.length > 1024 &&
      action?.length < 200
    ) {
      // efficient payload encoding

      let response = await fetch(path, {
        method: "POST",
        headers: {
          Accept: "application/json, application/octet-stream",
          "Content-Type": "application/octet-stream",
          "X-SRPC-Action": action ?? "", // maybe just don't set this header if action is null
          "X-SRPC-Raw-Payload": "1",
        },
        body: payload,
        redirect: "error",
      });
    } else {
      // JSON-encoding

      let response = await fetch(path, {
        method: "POST",
        headers: {
          Accept: "application/json, application/octet-stream",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ action, payload }),
        redirect: "error",
      });
    }

    if (response.headers.get("X-SRPC-Raw-Payload") == "1") {
      return await response.text();
    }

    response = await response.json();

    if (response.error) {
      console.error(response.error);
      display_error_to_user(response.error);
      return undefined;
    }

    if (response.warnings) {
      for (let warning of response.warnings) {
        console.warn(warning);
        display_warning_to_user(warning);
      }
    }

    if (response.debug) {
      for (let debug of response.debug) {
        console.debug(debug);
      }
    }

    return response.payload;
  } catch (err) {
    display_error_to_user("An error occurred: " + err.message);
  }
}
```

### Server

```php
// written for Laravel, but should be portable to other frameworks

use Illuminate\Http\Request;
use Illuminate\Http\Response;
use Symfony\Component\HttpFoundation\Request;

// this class handles receiving requests from a client, not sending a request to another server
final class SrpcRequest extends Request {
  public readonly string|null $action;
  public readonly int|float|array|object|string|null $payload;

  public function __construct(...$params) {
    if (count($params) < 1) {
      parent::__construct(
        query: request()->query->all(),
        request: request()->request->all(),
        attributes: request()->attributes->all(),
        cookies: request()->cookies->all(),
        files: request()->files->all(),
        server: request()->server->all(),
        content: request()->getContent(),
      );
    } else {
      parent::__construct(...$params);
    }

    $this->action = parent::get("action", null);
    $this->payload = parent::get("payload", null);
  }

  /**
   * Validate the contents of the payload. Assumes the payload is an object.
   */
  public function validate($rules, ...$params): array {
    $newRules = [];
    foreach ($rules as $key => $rule) {
      $newRules["payload." . $key] = $rule;
    }
    return parent::validate($newRules, ...$params);
  }

  /**
   * Call Laravel's validator on the payload.
   */
  public function validatePayload(string $rules): void {
    parent::validate(["payload" => $rules]);
  }

  /**
   * Fallback: Get a value from the payload. Not recommended; use ->payload->key instead.
   */
  public function __get($key): int|float|null|array|object|string {
    return $this->get("payload." . $key, null);
  }
}

final class SrpcResponse extends Response {
  private bool $payloadOrErrorIsSet = false;
  private mixed $payload = null;
  private string|null $error = null;
  private array $warnings = [];
  private array $debug = [];

  // Recommended use in your controller:
  // return $response->withPayload("Saved successfully");
  public function withPayload(mixed $payload): self {
    if ($this->payloadOrErrorIsSet) {
      throw new \Exception("Payload or error already set");
    }

    $this->payload = $payload;
    $this->payloadOrErrorIsSet = true;
    return $this;
  }

  // Recommended use in your controller:
  // return $response->withError("Couldn't save: collision");
  public function withError(string $error): self {
    if ($this->payloadOrErrorIsSet) {
      throw new \Exception("Payload or error already set");
    }

    $this->error = $error;
    $this->payloadOrErrorIsSet = true;
    return $this;
  }

  // Recommended use in your controller:
  // $response->addWarning('Format of postal code was corrected to "A1A 1A1"');
  public function addWarning(string $warning): void {
    $this->warnings[] = $warning;
  }

  // Recommended use in your controller:
  // $response->addDebug("Your user ID is " . Auth::id());
  public function addDebug(string|object $debug): void {
    $this->debug[] = $debug;
  }

  // called by Laravel automatically
  public function prepare(Request $request): static {
    if ($this->payloadOrErrorIsSet == false) {
      throw new \Exception("Payload or error not set");
    }

    if (
      gettype($this->payload) == "string" &&
      strlen($this->payload) > 1024 &&
      empty($this->warnings) &&
      empty($this->debug)
    ) {
      $this->headers->set("X-SRPC-Raw-Payload", "1");
      $this->headers->set("Content-Type", "application/octet-stream");
      $this->setContent($this->payload);
    } else {
      $this->headers->set("Content-Type", "application/json");

      $theResponse = [];
      if ($this->error != null) {
        $theResponse["error"] = $this->error;
      } else {
        $theResponse["payload"] = $this->payload;
      }
      if (!empty($this->warnings)) {
        $theResponse["warnings"] = $this->warnings;
      }
      if (!empty($this->debug)) {
        $theResponse["debug"] = $this->debug;
      }

      $this->setContent(json_encode($theResponse));
    }

    return parent::prepare($request);
  }
}
```

[spjc]: https://joekoop.com/blog/2023/10/18/spjc.html
[rfc2119]: https://www.rfc-editor.org/rfc/rfc2119
