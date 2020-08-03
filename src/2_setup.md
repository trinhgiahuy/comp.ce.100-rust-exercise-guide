# Setup

## Summary

On this page, we'll set up the workspace such that a native Rust baremetal application can be run on the PYNQ-Z1 device.

## Rust project work template

Download or clone the [project work template]()

`git clone ...`

### Install Rust and the cross-compiler toolchain

1. Go to [rustup.rs](https://rustup.rs/) and follow the instructions.
2. Install the nightly toolchain
    * `rustup install nightly`
    * We need the nightly toolchain to compile a line of assembly to enable interrupts via a `libxil` C-FFI library.
3. Set the nightly toolchain as the default in the project directory `rustup override set nightly` (do this from within the project directory).
4. Install the cross-compiler by running `rustup target add arm-none-eabi` on the command line.

These instructions are also available in the project template.
