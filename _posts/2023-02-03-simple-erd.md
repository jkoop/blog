---
title: Simple ERD
description: Easier to remember and faster to write than crow's foot
tags: notation
---

Simplified ERD is designed for fast writing (drawing?) of ERD ideas and is based on [Crow's Foot ERD][crows-foot], but with these key differences:

-   The arrow heads are easier to remember
-   There aren't redundant / badly described arrow heads
-   A full entity definition isn't required

## Arrow Heads

| Symbol  | Description / Designation |
| ------- | ------------------------- |
| `---|O` | zero or one               |
| `--||O` | zero or more              |
| `----|` | exactly one               |
| `---||` | one or more               |

## Examples

### Example 1

-   Users each have exactly one language
-   Languages can each have many users

```plain
user O||----| language
```

### Example 2

-   Users each have at least one email address
-   Email addresses each have at most one user

```plain
user O|----|| email_address
```

[crows-foot]: https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model#Crow's_foot_notation
