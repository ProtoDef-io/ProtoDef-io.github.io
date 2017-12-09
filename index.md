---
title: ProtoDef
permalink: /
---

ProtoDef is simply a specification for defining your binary formats: from game protocols, to the MPEG3 format, you can define it all in one concise, portable language standard. This is much like Protocol Buffers, however, ProtoDef is far more extensible. With Protocol Buffers you're limited to certain types and specific use-cases. With ProtoDef, we let you do whatever you like, however you like; if that's not enough for you: no worries, just fill the gap using your preferred language. Tell me more, you say? No, let me show you.

Given your protocol:

```ruby
@type integer("i32")
def_native("i32");

def("position") => container {
    field("x") => ::i32;
    field("y") => ::i32;
    field("z") => ::i32;
};
```

Compile it using `protodefc --language javascript --input protocol.pds --output output.js`

Then import it into your language (in this case, JavaScript):
```javascript
var output = require('./output.js');

var { size_of, serialize, deserialize } = output['::position'];

var offset = 0;
var input = { x: 1, y: 2, z: 3 };
var output = new Buffer(size_of(input));

serialize(input, output, offset);

console.log(output);

// => <Buffer 00 00 00 01 00 00 00 02 00 00 00 03>
```

## Use cases

You can use it for anything you want, but here are some cool usages:

- Game protocols (such as Minecraft, Terraria, etc.)
- File formats (MPEG3, PDF, Minecraft Map format, etc.)
- Keeping things concise over the wire with no rewriting: using Rust on the server-side, then using the same protocol specification in JavaScript, no porting required!
- Legacy protocols that are implemented in different languages across your clients and servers
