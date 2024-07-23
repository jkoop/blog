---
description: Seriously, it's super easy. Just do it like this
tags: json webdev zig # ok-analytics
---

## Parsing JSON in Zig isn't Hard

```plain
> zig version
0.13.0
```

While working on <!-- the foundations of my web analytics server, [OK Analytics][ok-analytics] --> a project of mine, I needed to add functionality to parse JSON. As it turns out, it's not very hard once you figure out how `std.json` wants to do it.

**Q:** What do you mean, "it's not very hard"? I know [`std.json`][zig-json] exists, but it's very tedious, isn't it? You get an iterator of "tokens" that you have to match to your preferred type, yourself, right?

**A:** Yes, but actually no.

You could handle the token stream yourself if you really wanted to, but if your JSON document is relatively small, you could pass it as a `[]u8` to `std.json.parseFromSlice`, or `...parseFromSliceLeaky`, depending or your memory situation, like this:

```zig
const std = @import("std");

test "parseFromSliceLeaky u16" {
    var arena = std.heap.ArenaAllocator.init(std.testing.allocator);
    defer arena.deinit();
    const allocator = arena.allocator();
    const result = try std.json.parseFromSliceLeaky(u16, allocator, "1234", .{});
    try std.testing.expect(result == 1234);
}
```

In fact, it even handles structs:

```zig
const std = @import("std");

const Contact = struct {
    id: u64,
    first_name: []u8,
    last_name: ?[]u8 = null, // to support parsing JSON without this member set, give it a default value
    phone_numbers: []struct {
        type: enum { home, mobile, work },
        number: []u8,
    },
    custom_fields: std.json.ArrayHashMap([]u8),
};

test "parseFromSliceLeaky Contact" {
    var arena = std.heap.ArenaAllocator.init(std.testing.allocator);
    defer arena.deinit();
    const allocator = arena.allocator();
    const result = try std.json.parseFromSliceLeaky(Contact, allocator,
        \\{
        \\  "id": 1234,
        \\  "first_name": "John",
        \\  "phone_numbers": [
        \\      { "type": "home", "number": "+18885550123" },
        \\      { "type": "mobile", "number": "+18885550189" }
        \\  ],
        \\  "custom_fields": {
        \\      "Hat size": "7\u00bc"
        \\  }
        \\}
    , .{});
    try std.testing.expect(result.id == 1234);
    try std.testing.expect(std.mem.eql(u8, result.first_name, "John"));
    try std.testing.expect(result.last_name == null);
    try std.testing.expect(result.phone_numbers[0].type == .home);
    try std.testing.expect(std.mem.eql(u8, result.phone_numbers[0].number, "+18885550123"));
    try std.testing.expect(result.phone_numbers[1].type == .mobile);
    try std.testing.expect(std.mem.eql(u8, result.phone_numbers[1].number, "+18885550189"));
    try std.testing.expect(std.mem.eql(u8, result.custom_fields.map.get("Hat size") orelse "", "7¼"));
}
```

I tried to include every type of data that you'd want to parse from a JSON document.

**TIP**  
There are some gotchas here: Nothing has a default value out-of-the-box. Even if you define something as being optional, if the JSON document doesn't specify a value for it, it won't default to `null`; it'll cause `std.json.<whatever>` to return a `MissingField` error.

[ok-analytics]: https://github.com/jkoop/ok-analytics
[zig-json]: https://ziglang.org/documentation/0.13.0/std/#std.json
