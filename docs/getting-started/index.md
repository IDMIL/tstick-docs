# Getting Started with your T-Stick

## T-Stick Variants
| Generation |          Model            | Variations                 | Platform                                |
|------------|:-------------------------:|----------------------------|-----------------------------------------|
| 1G         | Alto, Tenor               | None                       | Atmega8                                 |
| 2G         | Sopranino, Soprano, Tenor | 2G, 2GX, 2GG, 2G-IMU, 2GW  | Arduino, ESP8266                        |
| 3G         | Soprano                   | None                       | Arduino                                 |
| 4G         | Sopranino, Soprano        | 4GW-2018, 4GW-2021         | ESP32                                   |
| 5G         | Sopranino, Soprano        | 5GW-Trill, 5GW-Enchanti    | ESP32-S3                                |

## Building, Flashing and Connecting to your T-Stick
Guides for building, flashing and connectiong to various T-Sticks.

### 4th Generation T-Sticks

The 4th Generation of T-Sticks is the first generation of Wi-Fi based T-Sticks. The serial protocol and signal namespace used in the 1st and 2nd generation T-Sticks is not carried over to the 4th generation of T-Sticks. These T-Sticks used the ESP32 SoC from [Espressif](https://www.espressif.com/en/products/socs/esp32), a successor to the ESP8266. There are two variants of 4G T-Sticks. The T-Stick 4GW-2018 and the T-Stick 4GW-2021.

[:material-information: Click here for more details on 4th generation T-Sticks](../designs/tstick-4gw/index.md)

### 5th Generation T-Sticks

The 5th Generation T-Sticks consists of a custom ESP32 board which integrates a ESP32-S3 WROOM 2 Module with a ICM20948 IMU and MAX17262 on a single board, and a touch board that has a pinout for the Trill Craft board as well as, two JST-SH 4 pin connectors to daisy chain multiple touch boards together.

[:material-information: Click here for more details on 5th generation T-Sticks](../designs/tstick-5gw/index.md)