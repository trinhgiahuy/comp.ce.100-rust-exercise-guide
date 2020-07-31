# Setup


## Board template

Follow the main exercise guide until the project is set up, **or** do the following:

- Download "Johsul_harkka.zip" from the course page in moodle, and extract it to `P:\INTRA_HOME\Johsul_harkka` or a location of your choosing.
- Although the Rust version can be completed without the Xilinx SDK, you might as well verify that the project works alright. Here are the steps to do that:
    * open Xilinx SDK,
    * select the directory `P:\INTRA_HOME\Johsul_harkka` as the workspace,
    * make sure the PYNQ-Z1 board is turned on and connected,
    * right click on "Embedded_exercise", and select "Run As -> Launch on Hardware (System Debugger)".

While the Rust version of the coursework can be completed without using the Xilinx SDK, you will need it to gain access to the Xilinx® Software Command-Line tool (`xsct`). `xsct` will be used to run a script to reset the Pynq-Z1 board, program the FPGA on it, and upload a baremetal application onto the processor. Xilinx SDK comes pre-installed on the computers used for the course work.


## Install Rust and cross-compiler

- Go to [rustup.rs](https://rustup.rs/) and follow the instructions.
- Install the nightly toolchain `rustup install nightly`.
- Set the nightly toolchain as the default in the project directory `rustup override set nightly` (do this from within the project directory).
- Install the cross-compiler by running `rustup target add arm-none-eabi` on the command line.


## Rust project work template
- Download or clone the [project work template]().
