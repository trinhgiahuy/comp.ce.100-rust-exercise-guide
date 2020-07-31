# Setup

## Summary

On this page, we'll set up the workspace such that a native Rust baremetal application can be run on the PYNQ-Z1 device.

## Board template

- TODO: this may be optional

Follow the main exercise guide until the project is set up, **or** do the following:

- Download "Johsul_harkka.zip" from the course page in moodle, and extract it to `P:\INTRA_HOME\Johsul_harkka` or a location of your choosing.
- Although the Rust version can be completed without the Xilinx SDK, you might as well verify that the project works alright. Here are the steps to do that:
    * open Xilinx SDK,
    * select the directory `P:\INTRA_HOME\Johsul_harkka` as the workspace,
    * make sure the PYNQ-Z1 board is turned on and connected,
    * right click on "Embedded_exercise", and select "Run As -> Launch on Hardware (System Debugger)".

## Rust project work template

- Download or clone the [project work template]().

## Install Rust and the cross-compiler toolchain

- Go to [rustup.rs](https://rustup.rs/) and follow the instructions.
- Install the nightly toolchain `rustup install nightly`. We need the nightly toolchain to compile a line of assembly to enable interrupts via a `libxil` C-FFI library.
- Set the nightly toolchain as the default in the project directory `rustup override set nightly` (do this from within the project directory).
- Install the cross-compiler by running `rustup target add arm-none-eabi` on the command line.

