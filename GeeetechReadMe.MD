# Setup for Geeetech I3 Pro W
Use this readme for the future updates.

## Using Marlin:
For marlin, open this folder in vscode, with marlin and platformio plugins installed. 
Here the changes are already commited for geeetech printer.
Use -v when using platformio commands , this will help to see what is happening during the build or flash. 

relevent files are: 
```
./Marlin/Configuration.h
./Marlin/Configuration_adv.h
./Marlin/src/pins/mega/pins_GT2560_REV_A_PLUS.h
```
Check the commit: 9a4aaef56a32af9c28c2f4ef682a90a114cd9dde
for relevent changes.

## Using Klipper:
For klipper one needs to install the klipper on a raspberrypi, for that use : kiauh 
install klipper, then moonraker, then either use octoprint or mainsail as ui.

Its important to add the correct printer id into the printer.cfg : 
```bash
[mcu]
# Find with:  ls /dev/serial/by-id/*
serial: /dev/serial/by-id/usb-1a86_USB_Serial-if00-port0
```

For octoprint add this to the settings/serial connects: `home/[user]/printer_data/comms/klippy.serial`

**Klipper firmware:** 

The hex file is not commited, but to use the flash command below copy the hex file to this location: `klipper/klipper.elf.hex`

To build the klipper hex file, use the following commands in the klipper folder, most likely in `~/klipper`

`make menuconfig` and select the info about the board, the config will be similar to this and is located in `klipper/.config`: 
```
CONFIG_MCU="atmega2560"
CONFIG_AVRDUDE_PROTOCOL="wiring"
CONFIG_CLOCK_FREQ=16000000
CONFIG_AVR_CLKPR=-1
CONFIG_AVR_STACK_SIZE=256
CONFIG_AVR_WATCHDOG=y
CONFIG_SERIAL=y
CONFIG_SERIAL_BAUD_U2X=y
CONFIG_SERIAL_PORT=0
CONFIG_SERIAL_BAUD=250000

```
After that run the kiauh `~/kiauh/kiauh.sh` and select 4 for advanced menu, then build. this will generate a klipper.elf.hex in `~/klipper/out` folder that you can use to flash into the board.


**Klipper Printer Config**
`./klipper/printer.cfg`

**Flashing from this folder:**

```bash
avrdude -v -p atmega2560 -C /home/reza/.platformio/packages/tool-avrdude/avrdude.conf -c wiring -b 115200 -D -P /dev/ttyUSB0 -U flash:w:./klipper/klipper.elf.hex:i
```

##
