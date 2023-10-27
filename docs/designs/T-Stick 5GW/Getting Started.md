# Getting Started

## Building a T-Stick 5GW

### Bill of Materials

| Qty | Description |
|----|----|
| 01 | [Trill](https://shop.bela.io/products/trill-craft/) |
| 01 | Custom ESP32 Development Board |
| 01 | 30cm/60cm FSR 408 |
| 01 | [Button](https://www.digikey.ca/product-detail/en/c-k/PTS125SM43-2-LFS/CKN9100-ND/1146743) |
| 01 | Li-Po/Li-ion Battery min 1000mA |
| 01 | ABS/PVC Tube |
| 02 | Sparkfun Qwiic Cable or equivalent (at least 10cm) (longer T-Sticks need additional cables) |
| \~35cm | Heat shrink tube |
| 01 | end-cup with microcontroller base |
| 01 | end-cup with for the ON-OFF switch |
| 01 | 3D printed bases, one of each file, and 4 regular poles |
| 11 | M3 Mounting Screws |
| 01 | foam sheet |

## Flashing Firmware for a T-Stick 5GW

### Option 1: using .bin files and [esptool.py](http://esptool.py)

This method is easier/faster. It uses [esptool.py](https://github.com/espressif/esptool).

#### Download the bin files

* Download the .bin files located at the bin folder

#### Download [esptool.py](https://github.com/espressif/esptool)

* Download the *[esptool.py](http://esptool.py)* from <https://github.com/espressif/esptool>. Use the `Download ZIP` option from Github
* Unzip the *esptool-master.zip* file

#### Connect the T-Stick to the computer and check the USB port

* [Check the T-Stick (ESP32) port in your computer](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/establish-serial-connection.html):
  * For MacOS/Linux:
    * install the [latest drivers from from the SiLabs website](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers).
    * Open a *Terminal* window
    * Execute the command `ls /dev/cu.*`. The command will return a list of ports in your computer.
    * Plug the T-Stick (USB) and run the command `ls /dev/cu.*` one more time. You can now compare the lists and anotate the T-Stick USB port. Should be something similar to `/dev/cu.wchusbserial1410`, probably with a different number
    * Linux users should also give the currently logged user read and write access the serial port over USB. Check [here](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/establish-serial-connection.html) for more information
  * For Windows:
    * Check the list of identified COM ports in the [Windows Device Manager](https://support.microsoft.com/en-ca/help/4026149/windows-open-device-manager)
    * Plug the T-Stick (USB) and check the list of identified COM ports in the [Windows Device Manager](https://support.microsoft.com/en-ca/help/4026149/windows-open-device-manager) again. The T-Stick port should appear on the list. Anotate the T-Stick USB port, it should be something similar to `COM3` or `COM16`

#### Flash the firmware (.bin files)

* Use *Finder*, *Terminal*, or *File Explorer* to copy the contents of the [bin](https://../firmware/bin/) folder (you should copy 3 .bin files) to the *esptool-master* folder
* Navigate to the *esptool-master* folder in *Terminal* or *Command Prompt*
* Run the command (__don't forget to replace the --port (/dev/cu.wchusbserial1410) option for your T-Stick port__): `esptool.py --chip esp32 --port /dev/cu.wchusbserial1410 --baud 115200 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size detect 0xe000 boot_app0.bin 0x1000 bootloader_dio_80m.bin 0x10000 esp32_arduino_FW211124.bin 0x8000 esp32_arduino_FW211124.ino.partitions.bin 2686976 esp32_arduino_FW211124.spiffs.bin`. Wait for the process to be complete. Do not unplug or turn off your T-Stick during the process.

To set the T-Stick info and test if the data is being send correctly:

* Connect the T-Stick to a network (instructions [here](https://./T-Stick_2GW_Connecting_Guide(v1.2).md));
* Open the Pure Data (PD) or Max/MSP patch to receive T-Stick messages (they can be found [here](https://../Test_config/));
* Start receive OSC messages according to the chosen patch.

## Connecting to a T-Stick 5GW

### Option 1: Wireless Connection

#### Get your network details


1. Connect to the network you will be connecting the T-Stick to.
2. Note the SSID (network name) and SSID Password (network password).
3. Get your computers IP address while connected to this network. Below are linked some support articles for Windows, MacOS and Linux on how to find your computers IP address.
   * [Find your IP Address Windows](https://support.microsoft.com/en-us/windows/find-your-ip-address-in-windows-f21a9bbc-c582-55cd-35e0-73431160a1b9)
   * [Find your IP Address MacOS](https://discussions.apple.com/thread/253927735)
   * [Find your IP Address Linux](https://opensource.com/article/18/5/how-find-ip-address-linux)

#### Connect to the T-Stick


 4. Power on your T-Stick and wait until the boot sequence is complete. If your T-Stick does not have a Power switch press the button once and wait for the T-Stick to turn on.
 5. Connect to the T-Stick_XXX wifi network where XXX is the ID of the T-Stick. ie: TStick_001. By default the password is mappings.
 6. Open your browser and go to <http://TStick_XXX.local/> or <http://192.168.4.1>, where XXX is the ID of the T-Stick module. 

    \
     ![T-Stick Setup Page](Images/network-page.png)

    \
 7. In the __Network__ section write the network name and password optained in Step 2 in the __SSID__ and __SSID Password__ fields.
 8. In the __OSC send settings__ put in your computer's IP address optained in Step 3 in the __Primary IP__ field.
 9. Click the green __Save__ button. You will be directed to a page saying that the information was saved successfully.
1.  Click __Config__ on the top of the page to return to the orginal menu.
2.  Click the green __Close and Reboot__ button at the bottom of the page.


