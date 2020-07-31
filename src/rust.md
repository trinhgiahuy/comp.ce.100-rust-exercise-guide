# Rust quick reference

## Printing
Several facilities for printing are provided by the platform and by the course template. The simplest way to print is through the `print64` macro exported in `print.rs`. The `print64` and `println64` macros prints a maximum of 64 characters per call using standard Rust format print. Alternatively, you could call `xil::xil_printf` of the C-FFI to use the Xilinx version of the standard `printf` C-interface and C format strings. Using this interface, however, requires you to use nul-terminated strings like `"Hello World!\0"`.

## Unsafe
Unsafe blocks `unsafe {}` are used to wrap whatever code that the compiler cannot verify to not contain certain kinds of errors. Examples of code that needs to be wrapped in `unsafe {}` are:
- reading from or writing to an arbitrary physical memory address,
- dereferencing a raw-pointer (`*ptr`),
- call a function in `C`, eg. almost anything in the `xil_sys` / `xil` crate.

Runtime errors will mostly occur in `unsafe {}` blocks.

### Usage example
```
unsafe {
    xil::Xil_ExceptionEnable();
}
```


## Creating bindings to physical memory addresses

```const TEST: *mut u8 = 0x1234 as *mut u8;```

This line creates a constant pointer to an 8-bit value in a particular memory address (0x1234);


## Pointer access
Since the Rust standard library (std) is not available on the Cortex-A9, we use `core` versions of pointer operations. To read a pointer at an `address`, use

```let value: *const u8 = core::ptr::read_volatile( address );```,

to write a value at an `address`, use

```core::ptr::write_volatile( address, value );```.


## Xilinx functions
NOTE: You will not need to work with Xilinx Cortex-A9 board support package (BSP) functions in this course work.

The basic exercise template uses special functions from the Xilinx Cortex-A9 BSP. These functions are accessed from Rust using the `xil-custom-sys` crate, which contains the pre-built Xilinx driver package static library with soft-floats (`libxil_sf.a`). The `main.rs` of the template renames the library as `xil`, thus the Xilinx BSP functions are accessed as `xil::*`.
