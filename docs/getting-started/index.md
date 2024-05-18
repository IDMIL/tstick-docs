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

<div class="grid cards" markdown>

- __T-Stick 4GW-2018__ 

    ---

    An ESP32 based T-Stick using the LolinD32 Development board and a custom touch board.

    [:octicons-arrow-right-24: Getting started](../designs/tstick-4gw/specs_4gw_2018.md)

- __T-Stick 4GW-2021__ 

    ---

    An ESP32 based T-Stick using the TinyPico Development board and Bela Trill Touch Board.

    [:octicons-arrow-right-24: Getting started](../designs/tstick-4gw/specs_4gw_2021.md)

</div>

### 5th Generation T-Sticks

The T-Stick 5GW consists of a custom ESP32 board which integrates a ESP32-S3 WROOM 2 Module with a ICM20948 IMU and MAX17055 on a single board, and a touch board that has a pinout for the Trill Craft board as well as, two JST-SH 4 pin connectors to daisy chain multiple touch boards together.

[:material-information: Click here for more details on 5th generation T-Sticks](../designs/tstick-5gw/index.md)

<div class="grid cards" markdown>

- __T-Stick 5GW-Trill__ 

    ---
    
    An ESP32-S3 based T-Stick using the custom EnchantiS3 board and Bela's Trill Touch Board.

    [:octicons-arrow-right-24: Getting started](../designs/tstick-5gw/index.md)

- __T-Stick 5GW-Enchanti__ 
  
    ---
    
    An ESP32-S3 based T-Stick using the custom EnchantiS3 board and the Enchanti Touch Board.

    [:octicons-arrow-right-24: Getting started](../designs/tstick-5gw/index.md)

</div>