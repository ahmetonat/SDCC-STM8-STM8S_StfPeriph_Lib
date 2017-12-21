# Running SDCC for STM8 with STM8S_StfPeriph_Lib official libraries.

STM8 is an interesting processor. It is very simple to understanb by one person but has a modern core and peripheral architecture. Extremely cheap small development boards and device programmers are available. 
ST Microelectronics has a nice standard peripheral library (provided as source and with examples) that simplifies code development. However, the standard peripheral library was meant to be compiled only with commercial compilers which require registration, and limited capability in the evaluation (free) versions. The packages are also quite large to download and install, for such a simple processor.

Simple Device C Compiler (SDCC) has recently introduced support for STM8 series. However, some effort is needed to adapt the ST Standard Peripheral Library to SDCC, especially if make will be used for compilation. Here the necessary steps to build and run a LED blink code are provided, which will give the insight to get you going. The following steps are needed to setup a working environment:
1. Modify one file in the ST Standard Peripheral Library
2. Prepare the Makefile
3. Prepare your source code, compile and flash.
SDCC has one peculiarity: It can only compile one source file, which makes it somewhat tricky to build projects with many files. However, it has a solution that all the accompanying files in a project can be compiled into a project specific library (with extension .lib), which is then linked against the main source file during final compilation. The provided Makefile automaticaly does this and flashes the code to the processor.

The sample project blinks the LED on a STM8S103F3. The device programmer is the ST-LINK V2 with an included SWIM port.

**How to use:**
(In Linux)
- Install SDCC (I used version 3.5.0; earlier versions do not support stm8). 
- Download the ST 'STM8S_StdPeriph_Lib' under a suitable folder.
- Modify the file 'STM8S_StdPeriph_Lib/Libraries/STM8S_StdPeriph_Driver/inc/stm8s.h' (explained below)
- Edit the 'Makefile' provided to modify the library path.
- Similarly edit the 'Makefile' in 'libs' directory.
- Install 'stm8flash' from github. It is a device progammer for the SWIM port of the ST-Link V2 programmer.
- in the project folder type 'make flash'
The last step will compile the libraries under 'libs', compile main.c, and finally flash the code on the processor.

Once you set up your project correctly, all that you need to do is to execute **make flash** for a re-build any time you modiy your source and want to flash the code on your processor. It is possible to remove the intermediate files by executing **make clean** or simply compile the project by executing **make**.

