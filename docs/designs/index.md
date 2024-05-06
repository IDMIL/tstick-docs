# Current Designs

There are currently 5 generations of T-Sticks. The table below shows the sensors available in each of the T-Stick variants


### Table 1: T-Stick Variants
|                         | 2G | 2GW | 2G | 2GX | 2G-IMU | 2G | 4GW | 5GW          |
|-------------------------|:--:|-----|----|-----|--------|:--:|-----|--------------|
| Touch sensing channels  | 16 | 16  | 48 | 48  | 48     | 96 | 16  | 30/60/90/120 |
| Accelerometer (digital) | -  | -   | 1  | -   | -      | 1  | -   | -            |
| Accelerometer (analog)  | 1  | -   | -  | 1   | -      | -  | -   | -            |
| IMU                     | -  | 1   | -  | -   | 1      | -  | 1   | 1            |
| Piezoelectric           | 1  | -   | 1  | 1   | 1      | 1  | -   | -            |
| FSR                     | -  | 1   | -  | -   | -      | 2  | 1   | 1            |
| Paper force sensor      | 1  | -   | 1  | 1   | 1      | -  | -   | -            |
| IR                      | -  | -   | -  | 1   | -      | -  | -   | -            |
| Air pressure sensor     | -  | -   | -  | 1   | -      | -  | -   | -            |
| Photoresistor           | -  | -   | -  | 1   | -      | -  | -   | -            |

## T-Stick Variants

1. [T-Stick 4GW](../designs/tstick-4gw/index.md): Wi-Fi based T-Stick design, primarily for Sopranino and Soprano T-Stick with limited support for Alto and Tenor T-Stick. Uses the TinyPico ESP32 development board for control and communication along with a FSR for pressure sensing, a Trill Board for touch sensing and a LSM9DS1 for orientation and acceleration measurements.
2. [T-Stick 5GW](../designs/tstick-5gw/index.md): Wi-Fi based T-Stick design featuring a custom ESP32-S3 development board using a WROOM2 Module, alongside a ICM20948 IMU for orientation and acceleration measurements, a MAX17055 for battery management and keeping the Trill Board and FSR from the 4GW design.