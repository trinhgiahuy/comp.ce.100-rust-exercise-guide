## Special integer types

Rust makes a big deal about treating pointer-size related types different from ordinary integers. Rust uses `usize` for the unsigned pointer-width address value, and `isize` for the signed difference between two addresses. In our case on PYNQ-Z1 this is a 32-bit integer, but on your desktop computer it's probably a 64-bit integer. The most important thing to note about Rust's behavior around these types is that the pointer-width unsigned integer "`usize`" is required whenever we need to address an array (e.g. `DOTS[x][y][color] = value;`).

In practice, if you happen to have the wrong type, you can explicitly cast integers into these pointer-width types using the binary `as` operator: `DOTS[x][y][color as usize] = value;`. As usual, follow the instructions of the compiler.

