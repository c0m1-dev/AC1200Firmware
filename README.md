Xiaomi Extender AC1200 Firmware Migration to OpenWRT
Overview
This project provides a step-by-step guide to replace the stock firmware of the Xiaomi Extender AC1200 with OpenWRT. Due to similarities in chip architecture with other Xiaomi routers, this device is nearly fully supported by OpenWRT, enabling successful modifications for enhanced functionality.

Important Notice
Disclaimer: Modifying your device may void the warranty and carries the risk of bricking your router. I am not responsible for any damage caused during this process. Ensure you possess the necessary skills for soldering and desoldering components.

Supported Models
The Xiaomi Extender AC1200 comes in two variants:

RC04
RC75
The primary difference between these models is the chipset used for the 5GHz Wi-Fi band.

Prerequisites
Before proceeding, ensure you have:

A Xiaomi Extender AC1200 (RC04 or RC75)
CH341A Programmer for EEPROM
Soldering tools
Basic knowledge of networking and firmware flashing
Backup of the current firmware (highly recommended)
Backup Process
Solder the EEPROM Chip: Carefully desolder the EEPROM chip from the device and connect it to the CH341A Programmer.
Create a Dump: Use the CH341A to create a backup of your original firmware, saving it as dump.bin. This file will contain your device’s serial number and MAC address.
Available Firmware
I have uploaded my backup firmware for both RC04 and RC75 models in case your backup is corrupted.

Editing the Firmware (RC04 Only)
If using the RC04 model, you need to modify the following parameters in your firmware:

Change:

bash
Copy code
boot_wait=on
bootdelay=on
Use a hex editor (such as HxD) to edit the dump.bin file and apply these changes.

Flashing the Modified Firmware
Erase the EEPROM Chip: After editing, erase the EEPROM chip using your CH341A programmer.
Reflash the Edited Firmware: Upload the modified dump.bin back to the EEPROM.
UART Setup
To enable serial communication, solder a UART connector to the motherboard and connect the CP2102 as follows:

CP2102	RC04 Board
Rx	Tx
Gnd	Gnd
Tx	Rx
Using Serial Console
Open PuTTY and configure the following settings:

Connection Type: Serial
Serial Line: COM1 (check Device Manager for the correct COM port)
Speed: 115200
Click "Open" to initiate the connection.

Once connected, choose option 2 to proceed with the flashing process.

Uploading the Sysupgrade File
Feed the sysupgrade file for RC75 via TFTP server, log in after installation, and reboot.

Installing Additional Kernel Modules
For the RC04 model, you will need to install additional kernel modules due to the Wi-Fi chip:

kmod-mt7615e
kmod-mt7663-firmware-ap (or -sta)
Summary of the Full Process for RC04
Open the device.
Solder a header for the serial port.
Unsolder the flash ROM (if the test clip does not work).
Change the boot variables as described.
Resolder the flash.
Boot via serial console and select option 2.
Feed the sysupgrade file for RC75 via TFTP.
Log in after installation and reboot.
Install the additional kernel modules.

Additional Resources
For more guidance, check out the following link: OpenWRT Forum Discussion.

