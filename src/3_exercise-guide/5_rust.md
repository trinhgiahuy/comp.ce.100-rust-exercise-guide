# Rust things of note

## Printing

Like in the C-version, we must use a platform provided implementation of the print-functionality.

Several facilities for printing are provided by the course template. The simplest way to print is through the `print64` and `println64` macros exported in `print.rs`:

```rs
println64!("Hello World from Rust!");

println64!("This is an integer: {}.", 42);
```

The `print64` and `println64` macros print a maximum of 64 characters per call using Rust style format. Alternatively, you could call `xil::xil_printf` of the C-FFI to use the Xilinx version of the standard `printf` C-interface and C format strings:

```rs
unsafe {
    xil::xil_printf("Hello World via xil_printf\0".as_ptr());

    xil::xil_printf("This is an integer: %d\0".as_ptr(), 42);
}
```

As shown above, using this interface requires you to use raw pointers, unsafe and nul-terminated strings like so `"Hello World!\0"`, but it gets rid of the 64 byte limitation.


## Unsafe
Unsafe blocks `unsafe {}` are used to wrap whatever code that the compiler cannot verify to not contain certain kinds of errors. Examples of code that needs to be wrapped in `unsafe {}` are:
- reading from or writing to an arbitrary physical memory address or dereferencing a raw-pointer (`*ptr`),
- calling a function in `C`, eg. almost anything in the `xil_sys` / `xil` crate.

Runtime errors will mostly occur inside of `unsafe {}` blocks.

### Usage example
```rs
unsafe {
    xil::Xil_ExceptionEnable();
}
```


## Xilinx functions
NOTE: You will not need to work with Xilinx Cortex-A9 board support package (BSP) functions in this course work.

The basic exercise template uses special functions from the Xilinx Cortex-A9 BSP. These functions are accessed from Rust using the `xil-custom-sys` crate, which contains the pre-built Xilinx driver package static library with soft-floats (`libxil_sf.a`). The `main.rs` of the template renames the library as `xil`, thus the Xilinx BSP functions are accessed as `xil::*`.
