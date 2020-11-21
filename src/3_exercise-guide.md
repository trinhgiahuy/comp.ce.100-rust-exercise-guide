# Exercise Guide

We recommend you use "Visual Studio Code" to edit Rust source code. This is because as of the time of writing, Visual Studio Code has the best support for Rust language tools. Visual Studio Code also comes pre-installed on the computers at TC219.

## Register access

Let's get started. Register access in Rust is more complicated than in C. Please refer to the Rust book for the following relevant concepts that will not be explained here: [variable bindings](https://doc.rust-lang.org/rust-by-example/variable_bindings.html), [mutability](https://doc.rust-lang.org/rust-by-example/variable_bindings/mut.html), [constants](https://doc.rust-lang.org/rust-by-example/custom_types/constants.html?highlight=const#constants), [for-loops](https://doc.rust-lang.org/std/keyword.for.html).


### C

In C, you would first declare the register access using a 8 hexadecimal numbers, representing a 64-bit address to an 8-bit value like so:

```c
#define ADDRESS *(uint8_t*) 0x42010002
```

Then you'd perhaps define a particular combination of bits to help setting a particular bit in the 8-bit register value:

```c
#define A_BIT 0b00000001
```

And finally, you might set the value in the register by first de-referencing, and then using a bitwise OR to set the particular bit:

```c
*ADDRESS |= A_BIT;
```

### Rust

In Rust, you'd first declare the 64-bit address to an 8-bit value and the bit combination as constant globals like so:

```rs
const ADDRESS: *mut u8 = 0x42010002 as *mut u8;
const A_BIT: u8 = 0b00000001;
```

Now's the complicated part. Rust doesn't allow direct register access, and the compiler is more aggressive at optimizing. That's why we must use a set of method designed for register access, called `core::ptr::read_volatile` and `core::ptr::write_volatile`.

First, we must retrieve the 64-bit pointer to the 8-bit value into a **mutable binding**:

```rs
let value: *mut u8 = core::ptr::read_volatile( ADDRESS );
```

Then we must flip the bit, and write back into the register at the end of the 64-bit pointer:

```rs
value |= A_BIT;

// Write `value` back to main memory at `ADDRESS`
core::ptr::write_volatile( ADDRESS, value );
```

For your convenience, we have also provided a method called `mutate_ptr` to help do all of the above in one go:

```rs
const ADDRESS: *mut u8 = 0x42010002 as *mut u8;
const A_BIT: u8 = 0b00000001;

fn some_function() {
    mutate_ptr(ADDRESS, |val| val |= A_BIT);
}
```

Now that you know how to do register access, you might be able to rewrite the `setup` function from C in Rust.

## Bit-width

Rust makes a big deal about treating pointer-size related types different from ordinary integers. Rust uses `usize` for the unsigned 64-bit address value, and `isize` for the signed difference between two addresses. The most important thing to note about Rust's behavior around these types is that the pointer-width unsigned integer "`usize`" is required whenever we need to address an array (e.g. `DOTS[x][y][color] = value;`).

In practice, if you happen to have the wrong type, you can explicitly cast integers into these pointer-width types using the binary `as` operator: `DOTS[x][y][color as usize] = value;`. As usual, follow the instructions of the compiler.

## Leds-array

Indexing the leds-array works a little different between C and Rust.

### C

The C-version of the course project declares a global volatile three-dimensional array like so:

`volatile uint8_t dots[8][8][3] = {0};`

Volatile means that the values of the table are prone to change by something other than the code that is currently executing close by. An instance of such a situation would be when two different interrupt handlers are simultaneously reading from and writing into the array.

### Rust

In Rust, a similar three-dimensional array would be declared like so:

`static mut dots: [[[u8; 3]; 8]; 8] = [[[0; 3]; 8]; 8];`

While the indexing looks different, the meaning is the same: there's two 8-length outer dimensions for the x- and y-coordinates, and the innermost dimension for the color with a length of three.

Indexing the first color (perhaps red) at "x = 1", "y = 2" would then in both languages be expressed as `dots[1][2][0]`.

With this knowledge, you might be able to re-write `SetPixel` from the original C code.


## Match statements

Your C-code likely contains many `if-else` chains and `switch` cases. In Rust, these are both replaced by something called a [`match-statement`](https://doc.rust-lang.org/rust-by-example/flow_control/match.html). In the interrupt handlers, there are very good use cases for matching into binary numbers.

Use this information to re-write the game logic in main.rs, and possibly other files.


## Proceeding from here

With the above differences covered, the rest of the work should mostly consist of copy-pasting the C-code from the source, and adjusting based on compiler instructions. The next page of the guide contains some more curiosities that may or may not be relevant to completing the exercise.