# T-Stick 5GW

## Introduction

The T-Stick 5GW consists of a custom ESP32 board which integrates a ESP32-S3 WROOM 2 Module with a ICM20948 IMU and MAX17055 on a single board, and a touch board that has a pinout for the Trill Craft board as well as, two JST-SH 4 pin connectors to daisy chain multiple touch boards together. The T-Stick switches from the Puara framework that the [4GW](./T-Stick%204GW.md) design uses in favor of Sygaldry. Sygaldry is a conceptual frame for developing digital musical instruments that are replicable, readable and reliable. Information about Sygaldry and the implementation of T-Stick Components can be found on their [website](https://enchantedinstruments.com/).

### Read more about Sygaldry

* [Design Concepts](https://enchantedinstruments.com/page-docs-design_concepts.html)
* Implementation Specific Documentation
  * [T-Stick Implementation](https://enchantedinstruments.com/page-sygin-t_stick)
  * [ESP32 Button](https://enchantedinstruments.com/page-sygse-button.html)
  * [Trill Craft Implementation](https://enchantedinstruments.com/page-sygsa-trill_craft)
  * ICM20948 Implementation

## System Architecture

Figure 1 shows the hardware architecture for the new T-Stick design. Most of the power sytem functions such as providing power, charging the instrument and changing the power state is handled by the MCP73871. This IC handles charging the LiPO/Li-ion battery and changing between the USB power and battery power depending on voltage. In addition, two regulators, the NCP167AMX330TBG/NCP167AMX1800TBG series are used to step down the system power to 3.3V and 1.8V respectively. The MAX17055 is used as a fuel gauge. As mentioned previously this fuel gauge is used over its non-current sensing counter parts due to better accuracy.

 ![Figure 1: T-Stick 5GW Architecture](Images/TStick-HardwareArchitecture-Pro.png)

The Trill Craft board is kept as the capacitive sensor solution of choice. A more integrated solution using just the MCU on the Trill Craft board was considered but figuring out how to flash the MCU in a systematic way, would have been more of a hassle than it is worth. The touch board uses a 32 pin FFC connector to connect to a flexible PCB with 30 touch points and two ground points. The IMU is changed to an ICM20948 9-DOF IMU. as mentioned previously this is due to the fact that the LSM9DS1 is no longer actively supported by the company that produces it. It receives the 1.8V power from one of the regulators. Three mosfets are used to convert the 1.8V logic from the ICM20948 to 3.3V to communicate with the ESP32. 

## Gesture Algorithms

Note: Section is still a Work in Progress

Like the fourth generation T-Sticks this 5th generation of T-Sticks also includes embedded gestures. It also uses the Puara Gestures Library for gesture extraction. The table below lists all the properties that are extracted for the high-level gesture.

### Table 1: High Level Gestures

| Address | Data type | Min | Max | Description |
|----|----|----|----|----|
| /instrument/touch/all | float | 0 | 1 | Amount of touch |
| /instrument/touch/top | float | 0 | 1 | Amount of touch on the top region |
| /instrument/touch/middle | float | 0 | 1 | Amount of touch for the middle part |
| /instrument/touch/bottom | float | 0 | 1 | Amount of touch for the bottom part |
| /instrument/touch/frame/position | integer | 0 | Number of touch sensors - 1 | Position of frame start from bottom |
| /instrument/touch/frame/size | integer | 0 | Number of touch sensors - 2 | Size of frame |
| /instrument/touch/frame/touch\[N\] | integer | 0 | 1 | Touch values within frame |
| /instrument/brush/up | float | 0 | 1 | Distance traveled during brush up |
| /instrument/brush/down | float | 0 | 1 | Distance traveled during brush down |
| /instrument/brush/amplitude | float | 0 | 1 | Amplitude of brush |
| /instrument/brush/energy | float | 0 | 1 | Brush energy |
| /instrument/orientation/yaw | float | -1 | 1 | Yaw |
| /instrument/orientation/pitch | float | -1 | 1 | Pitch |
| /instrument/orientation/roll | float | -1 | 1 | Roll |
| /instrument/shake | float | 0 | 1 | TBD |
| /instrument/jerk | float | 0 | 1 | TBD |
| /instrument/thrust/x | float | -1 | 1 | Thrust/jab gesture magnitude |
| /instrument/thrust/y | float | -1 | 1 | Thrust/jab gesture magnitude |
| /instrument/thrust/z | float | -1 | 1 | Thrust/jab gesture magnitude |
| /instrument/squeez | float | 0 | 1 | Same as pressure for now |
| /instrument/rest | float | 0 | 1 | High when interaction activity is low |
| /instrument/effort | float | 0 | 1 | High when interaction activity is high |


