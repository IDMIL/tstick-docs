# T-Stick 5GW-Trill

The T-Stick 5GW-Trill is a 5th generation T-Stick that uses [Bela's Trill Craft Touch Board](https://bela.io/products/trill/). More details on 5th generation T-Sticks can be found [here](./index.md).

## Guides
For information on how to use the T-Stick 5GW-Trill check out the guides below:
<div class="grid cards" markdown>

- [:material-wrench: __Build Guide__](./build-guide-trill.md)
- [:material-upload: __Flashing Guide__](./flashing-guide.md)
- [:material-wifi: __Connection Guide__](./connection-guide.md)

</div>

## Specifications
| Feature                     | Details                                                                                                                    |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Status                      | Recommended for new builds                                                                                                 |
| Release Year                | 2024                                                                                                                       |
| Communication Type          | Wi-Fi 4, 802.11 b/g/n                                                                                                      |
| Compatible protocols        | Open Sound Control (OSC)/Libmapper                                                                                         |
| Touch Sensing Density       | 1 channel per 1cm                                                                                                          |
| Microcontroller             | ESP32-S3 Series                                                                                                            |
| Gestures Embedded?          | Yes                                                                                                                        |
| Embedded Gestures Libraries | [Puara Gestures](../../engineering/gestures.md)                                                                            |
| Sensors                     | ICM20948 IMU, Trill Craft Capacitive Sensing Board (30 channels), Force Sensitive Resistor 408 Series, MAX17262 Fuel Gauge |

## OSC Signal Namespace

!!! note

    Replace XXX for the T-Stick ID number

### Raw data
| Signal Name              | Type | Range                         | Description                                                         |
|--------------------------|:-----|-------------------------------|---------------------------------------------------------------------|
| /TStick_XXX/raw/capsense | i... | 0 :material-arrow-right: 512  | Raw signal from the touch sensor.                                   |
| /TStick_XXX/raw/fsr      | i    | 0 :material-arrow-right: 4095 | Raw signal from the force sensitive resistor                        |
| /TStick_XXX/raw/accl     | fff  | :material-plus-minus: 24      | Raw signal from the accelerometer in 3-axis (x,y,z)                 |
| /TStick_XXX/raw/gyro     | fff  | :material-plus-minus: 42      | Raw signal from the gyroscope in 3-axis (x,y,z)                     |
| /TStick_XXX/raw/magn     | fff  | :material-plus-minus: 0.001   | Raw signal from the magnetometer in 3-axis (x,y,z)                  |

### Battery Signals
| Signal Name                         | Type | Range                         | Description                                                         |
|-------------------------------------|:-----|-------------------------------|---------------------------------------------------------------------|
| /TStick_XXX/battery/percentage      | f    | 0 :material-arrow-right: 100  | Battery percentage                                                  |
| /TStick_XXX/battery/voltage         | f    | 0 :material-arrow-right: 4.2  | Battery voltage (V)                                                 |
| /TStick_XXX/battery/current         | f    | :material-plus-minus: 2000    | Battery current (mA)                                                |

### Button Signals
| Signal Name                         | Type | Range                      | Description                               |
|-------------------------------------|:-----|----------------------------|-------------------------------------------|
| /TStick_XXX/instrument/button/count | i    | 0 :material-arrow-right: x | Number of times the button was tapped     |
| /TStick_XXX/instrument/button/tap   | i    | 0 or 1                     | Outputs 1 if the button was tapped        |
| /TStick_XXX/instrument/button/dtap  | i    | 0 or 1                     | Outputs 1 if the button was double tapped |
| /TStick_XXX/instrument/button/ttap  | i    | 0 or 1                     | Outputs 1 if the button was triple tapped |

### Touch Gestures
| Signal Name                         | Type | Range                      | Description                                         |
|-------------------------------------|:-----|----------------------------|-----------------------------------------------------|
| /TStick_XXX/instrument/squeeze      | f    | 0 :material-arrow-right: 1 | Normalised signal from the force sensitive resistor |
| /TStick_XXX/instrument/touch/all    | f    | 0 :material-arrow-right: 1 |                                                     |
| /TStick_XXX/instrument/touch/top    | f    | 0 :material-arrow-right: 1 |                                                     |
| /TStick_XXX/instrument/touch/middle | f    | 0 :material-arrow-right: 1 |                                                     |
| /TStick_XXX/instrument/touch/bottom | f    | 0 :material-arrow-right: 1 |                                                     |
| /TStick_XXX/instrument/brush        | f    | 0 :material-arrow-right: x | cm/s                                                |
| /TStick_XXX/instrument/multibrush   | ffff | 0 :material-arrow-right: x | cm/s                                                |
| /TStick_XXX/instrument/rub          | f    | 0 :material-arrow-right: x | cm/s                                                |
| /TStick_XXX/instrument/multirub     | ffff | 0 :material-arrow-right: x | cm/s                                                |

### Inertial Gestures Signals

| Signal Name                     | Type | Range                                                                                                      | Description                               |
|---------------------------------|:----:|------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| /TStick_XXX/orientation         | ffff | N/A                                                                                                        | Quaternions for T-Stick orientation       |
| /TStick_XXX/instrument/ypr      | fff  | :material-plus-minus: 180$^{\circ}$ :material-plus-minus: 90$^{\circ}$ :material-plus-minus: 180$^{\circ}$ | Yaw, pitch, roll of T-Stick               |
| /TStick_XXX/instrument/shakexyz | fff  | 0 :material-arrow-right: x                                                                                 | Shake intensity in 3-axis (x,y,z)         |
| /TStick_XXX/instrument/jabxyz   | fff  | 0 :material-arrow-right: x                                                                                 | Jab intensity in 3-axis (x,y,z)           |