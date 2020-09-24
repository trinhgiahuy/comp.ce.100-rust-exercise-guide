# Xilinx tools


## Summary

Everything described on this page already comes pre-installed on the course computers, so if you're using one of those, feel free to skip onto the next page. However, if you're working on a personal computer, this page will help in attaining the software required for the course work.


## Install `xsct`

To run the course work template on PYNQ-Z1 System-on-Chip (SoC), you will need a working installation of the Xilinx® Software Command-Line tool (`xsct`).`xsct` comes along with most other Xilinx tools like Xilinx SDK. Here we'll use the unified installer as instructed at [ArchWiki](https://wiki.archlinux.org/index.php/Xilinx_Vivado#Vivado_and_SDK). Downloading the file will require a "Xilinx account" that can be created at the cost of your download privacy (ie. Xilinx wants to know who's downloading the installer). The installer will run for quite a while so give it at least a few hours. Once installed, the Xilinx toolchain should be available at `/opt/Xilinx` or whatever location you installed it to.

`xsct` will be used to run a script to reset the Pynq-Z1 board, program the FPGA on it, and upload a baremetal application onto the processor. Xilinx SDK comes pre-installed on the computers used for the course work.
