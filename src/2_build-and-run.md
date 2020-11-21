# Building and running the application on-device

To get started, you'll need to download the repository onto your computer. You could do this by opening a terminal (e.g. Git Bash) and typing the following:

`git clone https://github.com/hegza/alien-shooter-template-rs`

This will download the project directory "alien-shooter-template-rs" onto your computer.

The downloaded Rust project comprises board configuration files, Rust source code and Rust build configurations. They are arranged in the following manner:

| Path          | Description | Notes |
|---------------|-------------|-------|
| src/          | The Rust source code | This is what you will need to edit in the next phase |
| pynq/         | PYNQ-Z1 board configuration files | You will **not** need to make changes to these |
| Cargo.toml    | Rust library dependencies and package configuration | |
| .cargo/config | Rust build configurations | Especially: linker configurations |

Building and running a Rust application is usually as simple as invoking the main toolchain build command. Unfortunately, we're cross-compiling from desktop to another device provided by a manufacturer with specific requirements. Because of this, we'll need to provide the location of the manufacturer's tools with the build command.

## Build the application

Before we start, switch to the project directory in your terminal (e.g. Git Bash):

`cd alien-shooter-template-rs`

Then set the cross-compiler for this directory. We use Cortex-A9 v7 with "none" operating system and embedded application binary interface (EABI):

`rustup target add armv7a-none-eabi`

We're going to need to provide the location of the manufacturer's tools as an environment variable. Setting the environment variable is different on different types of terminals. **OBS:** Note that using Windows command prompt is not recommended. Here's The synopsis:

| Terminal | Command |
|-|-|
| Git Bash, WSL, native Linux | `export XILINX_SDK="/path/to/Xilinx/SDK/version"`  |
| PowerShell | `$Env:XILINX_SDK = "/path/to/Xilinx/SDK/version"`
| Windows command prompt | `setx XILINX_SDK "/path/to/Xilinx/SDK/version"` |

When the environment variable is set, we should be able to use:

`cargo build`, to produce an executable file that we can run on the PYNQ-Z1.

For instance, at TC219 using on Git Bash and Vivado 2017.2:
1. `export XILINX_SDK="C:/Apps/Xilinx_Vivado2017/SDK/2017.2"`
2. `cargo build`

or just `XILINX_SDK="C:/Apps/Xilinx_Vivado2017/SDK/2017.2" cargo build`.

## Open an input-output interface to the board

Just building the application is not enough. We also need to put the binary executable on the device and start executing. Before that, we'll want to open an interface to the board to be able to see what we are printing. In this exercise, we're going to open an UART over USB connection to the board. First, we'll need to figure out which COM port the device maps itself to:

- Open the Windows Device Manager, and visually monitor the "Ports (COM & LPT)" section. Connect the board to the computer using the supplied micro-USB cable (sa. main exercise guide), then **turn on the device**, and then take note of which serial line the device gets connected to in the device manager, eg. USB Serial Port (COM5). In this case, the serial line would be "COM5".
- Open PuTTY, and select the following settings:
    * connection type: serial,
    * serial line: COM5 (yours maybe different, see device manager),
    * speed: 115200.
- You may optionally save the configuration by typing a name into the "Saved Sessions" field and pressing 'Save'. Finally, press "Open".
- A successful connection will result in an idle PuTTY window.

## Running our code on device

We'll need to use Xilinx' own tools to install the binary executable onto the device. We'll use their command line interface called `xsct`. On Windows, you can find it in the Start Menu by typing "Xilinx Software Command Line Tool". Running that will open a blank command prompt.

With the command prompt open, you'll need to navigate to the project directory. You can use `cd name_of_directory` to switch directories, and `dir` to list the contents to find the next directory to switch to. You can use e.g. `cd P:/` to switch drives.

With luck, you might be able to just type: `cd P:/`, and `cd alien-shooter-template-rs`.

## Upload the application onto the processor

Once we have located the project in the `xsct` command prompt, we'll need to upload our executable onto the device. The project provides an automation script in the Xilinx preferred Tickle-script format. The script can be run with:

`source run_on_pynq.tcl`

The program should now print something on a connected PuTTY terminal.

Feel free to look inside "run_on_pynq.tcl" to see what `xsct` is doing (reset, program FPGA, upload, ...).

# Summary

Once you make edits to the program source code in "src/", you will need to rebuild the project using e.g. Git Bash:

`cargo build`

Then you will need to upload the built program executable into the device using Xilinx Software Command Line Tool:

`source run_on_pynq.tcl`
