# Running the application on-device


## Build the application


## Open an input-output interface to the board
In this exercise, we're going to open an UART over USB connection to the board. This allows us to see the output of our print statements. Guide to open UART over USB is provided both for Windows and Linux.

### Windows
- Open the Windows Device Manager, and visually monitor the "Ports (COM & LPT)" section. Connect the board to the computer using the supplied micro-USB cable (sa. main exercise guide) and take note of which serial line the device gets connected to in the device manager, eg. USB Serial Port (COM5). In this case, the serial line would be "COM5".
- Open PuTTY, and select the following settings:
    * connection type: serial,
    * serial line: COM5,
    * speed: 115200.
- You may optionally save the configuration by typing a name into the "Saved Sessions" field and pressing 'Save'.
- A successful connection will result in an idle PuTTY window.

### Linux


## Upload the application onto the processor
- Run the script
    * feel free to look inside to see what `xsct` is doing (reset, program, upload, ...)
