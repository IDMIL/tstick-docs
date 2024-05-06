# T-Stick 4GW

## Introduction

The T-Stick 4GW was designed by Eduardo Meneses and Alex Nieva with the first revision being completed in 2018. This generation of T-Sticks is a Wi-Fi based system using Open Sound Control and later Libmapper for sending signals. It uses the ESP32 microcontroller for controlling the T-Stick. Multiple development boards such as the Lolin D32 and TinyPico have been used with this design. Although the design is modular and can in theory support T-Sticks up to the length of a Tenor T-Stick. Limitations due to how the T-Stick is constructed and firmware makes this design appropriate only for Sopranino and Soprano T-Sticks.

Note that as the TinyPico is now discontinued it can be replaced with the TinyS3, but changes to the 3D skeleton may need to be done.

## System Architecture

The T-Stick can be split into four subsystems: a control system, power system, sensor system, and mapping system.

The control system interprets the outputs of the sensor system, identifies gestures, and manages the power state of the T-Stick (on/sleep/off). The power system delivers power to the rest of the subsystems as well as handling the charging and discharging of batteries. The sensor system handles the input of the user as well as basic signal processing. The raw and processed signals are sent to the control system to be interpreted. The mapping system handles the T-Stick’s connections with external devices. This is handled by either libmapper or OSC. The system handles sending and receiving signals.

## Technical Details

### Summary

| Feature | Details |
|----|----|
| Status | Not recommended for new builds |
| Communication Type | Wi-Fi, 802.11 b/g/n |
| Compatible protocols | Open Sound Control (OSC)/Libmapper |
| Touch Sensing Density | 1 channel per 2cm |
| Microcontroller | ESP32 Series |
| Gestures Embedded? | Yes |
| Embedded Gestures Libraries | [Puara Gestures](../../engineering/gestures.md) |
| Sensors | LSM9DS1 IMU, Trill Craft Capacitive Sensing Board (30 channels), Force Sensitive Resistor 408 Series |


## OSC Signal Namespace

### firmware 231031

**Replace XXX for the T-Stick ID number**

#### Raw data

/TStick_XXX/raw/capsense, i..., 0--4095,

/TStick_XXX/raw/fsr, i, 0--4095

/TStick_XXX/raw/accl, fff, +/-24 (floats)

/TStick_XXX/raw/gyro, fff, +/-42 (floats)

/TStick_XXX/raw/magn, iii, +/-0.001 (floats)

#### Instrument data

/TStick_XXX/instrument/button/count, i, 0--i

/TStick_XXX/instrument/button/tap, i, 0 or 1

/TStick_XXX/instrument/button/dtap, i, 0 or 1

/TStick_XXX/instrument/button/ttap, i, 0 or 1

/TStick_XXX/instrument/squeeze, f, 0--1

/TStick_XXX/orientation, ffff, ?, ? ,? ,?

/TStick_XXX/instrument/ypr, fff, +/-180, +/-90 ,+/-180 (degrees)

/TStick_XXX/instrument/touch/discrete, i, i..., 0 or 1

/TStick_XXX/instrument/touch/normalised, i, i..., 0--100

/TStick_XXX/instrument/touch/all, f, 0--1

/TStick_XXX/instrument/touch/all, f, 0--1

/TStick_XXX/instrument/touch/top, f, 0--1

/TStick_XXX/instrument/touch/middle, f, 0--1

/TStick_XXX/instrument/touch/bottom, f, 0--1

/TStick_XXX/instrument/brush, f, 0--? (\~cm/s)

/TStick_XXX/instrument/multibrush, ffff, 0--? (\~cm/s)

/TStick_XXX/instrument/rub, f, 0--? (\~cm/s)

/TStick_XXX/instrument/multirub, ffff, 0--? (\~cm/s)

/TStick_XXX/instrument/shakexyz, fff, 0--?

/TStick_XXX/instrument/jabxyz, fff, 0--?

/TStick_XXX/battery/percentage, f, 0--100

/TStick_XXX/battery/voltage, f, 0--?
