# Setup

## Summary

On this page, we'll set up the workspace such that a native Rust baremetal application can be run on the PYNQ-Z1 device.

### Install Rust and the cross-compiler toolchain

These instructions are also available in the project template.

1. Go to [rustup.rs](https://rustup.rs/) and follow the instructions.
2. Install the nightly toolchain
    * `rustup install nightly`
    * We need the nightly toolchain to be able to compile a single line of assembly to enable interrupts via the `libxil` C-FFI library.
3. Set the nightly toolchain as the default in the project directory `rustup override set nightly` (do this from within the project directory).
4. Install the cross-compiler by running `rustup target add armv7a-none-eabi` on the command line.
