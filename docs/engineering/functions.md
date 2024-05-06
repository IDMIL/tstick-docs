# T-Stick Functions

## Introduction

This page outlines the high level functions the T-Stick does and links previous designs of the T-Stick for inspiration of how the functions were accomplished.

## Functional Analysis

As shown in figure below the T-Stick has a relatively straight forward functional flow block diagram. 


 ![functional flow block diagram of T-Stick](../Images/ffbd-tstick.png)

The sensors must be initialised, and then regularly polled for their raw sensor data. Any sensor errors must be processed and then converted to error messages to be sent to the user. In the fourth generation of T-Sticks this function is not fully developed but still exists, as most errors are at least printed to the serial monitor. The power system of the T-Stick handles charging the instrument, providing power to all components and changing the power state between active operation and deep sleep. The control and communication system output signals and interpret any user inputs/signals such as using the serial monitor to reboot the T-Stick.


