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

**Klipper firmware:** `klipper/klipper.elf.hex`

**Klipper Printer Config**
`./klipper/printer.cfg`

**Flashing from this folder:**

```bash
avrdude -v -p atmega2560 -C /home/reza/.platformio/packages/tool-avrdude/avrdude.conf -c wiring -b 115200 -D -P /dev/ttyUSB0 -U flash:w:./klipper/klipper.elf.hex:i
```

##
