# Running the application on-device


## Build the application

`cargo build`

The project is configured to automatically run the `armv7a-none-eabi` cross-compilation toolchain.

## Open an input-output interface to the board
In this exercise, we're going to open an UART over USB connection to the board. This allows us to see the output of our print statements. Guide to opening UART over USB is provided for Windows

### Windows
- Open the Windows Device Manager, and visually monitor the "Ports (COM & LPT)" section. Connect the board to the computer using the supplied micro-USB cable (sa. main exercise guide), then **turn on the device**, and then take note of which serial line the device gets connected to in the device manager, eg. USB Serial Port (COM5). In this case, the serial line would be "COM5".
- Open PuTTY, and select the following settings:
    * connection type: serial,
    * serial line: COM5 (yours maybe different, see device manager),
    * speed: 115200.
- You may optionally save the configuration by typing a name into the "Saved Sessions" field and pressing 'Save'.
- A successful connection will result in an idle PuTTY window.

## Set up xsct
- Open an `xsct` terminal (ie. look for "Xilinx Software Command Line Tool" in the Windows menu)
- Navigate to the project directory using `cd` and `dir`:
    * `cd path/to/project`

## Upload the application onto the processor
- Use the supplied tickle-script to initialize the board and run the application:
    * `source run_on_pynq.tcl`
- The program should now print something on a connected PuTTY terminal.
- Feel free to look inside "run_on_pynq.tcl" to see what `xsct` is doing (reset, program, upload, ...).
