# Technical Requirements and Constraints

This page outline the technical requirements of the T-Stick as well as constraints inherited from previous designs. The goal is that with these technical requirements and constraints someone will be able to build a T-Stick that is functionally identical to the designs that have previously been built.

# Verification Method table

|    | **Verification Method (IADT)** |
|----|----|
| Inspection | Visual inspection of the device |
| Analysis | Simulation, mathematical models and data analysis |
| Demonstration | Demonstrate the functionality for the user |
| Test | More rigorous form of demonstration to show performance |

# Technical Requirements

The technical requirements are split into 5 sections representing each of the major subsystems of the T-Stick and a section for manufacturing and reliability requirements.

## 1. Control and Communication System

Control and Communication System of the T-Stick is the set of hardware and software components that handle the controlling and regulating the instrument which includes: configuring the instrument, communicating with the instrument, communication between subsystems, and managing the main control loop. 

| **ID** | **Requirements** | **Verification Method (IADT)** |
|----|----|----|
| **1** | **Control System** |    |
| 1.1 | The control rate of the system should be at least 1000HZ and will be no slower than 200Hz. | Test |
| 1.2 | Continuous signals should have a wireless signal rate of at least 100Hz and will be no slower than 50Hz. | Test/Analysis |
| 1.3 | Wireless Signal Latency will be below 10ms. | Test/Analysis |
| 1.4 | Wireless Signal Jitter will be below 2ms. | Test/Analysis |
| 1.5 | The communication system will send any errors experienced by other subsystems to the user. | Demonstration |
| 1.5.1 | The communication system will send errors experienced by the sensor system to the user. | Demonstration |
| 1.5.2 | The communication system will send errors experienced by the power system to the user, excluding errors that cause a complete power delivery failure. | Demonstration |
| 1.5.3 | The communication system will send errors experienced by the control and communication system to the user. | Demonstration |

### 1.1: The control rate of the system should be at least 1000HZ and will be no slower than 200Hz..

1000Hz allows responsive control of the T-Stick.

### 1.2: Continuous signals should have a wireless signal rate of at least **100Hz** and will be no slower than 50Hz.

INSERTJUSTIFICATIONHERE

### 1.3: Wireless Signal Latency will be below 10ms.

Wireless latency for signals need to be below 10ms for continuous signals to have a signal rate of 100Hz.

### 1.4: Wireless Signal Jitter will be below 2ms.

Jitter should be reasonably low for a consistent wireless speed.

### 1.5: The communication system will send any errors experienced by other subsystems to the user

The communication system should handle sending any errors to the user wirelessly or wired. This helps the user understand what is going on with their T-Stick when things go wrong.

## 2. Power System Requirements

The Power System of the T-Stick handles delivering power to all components of the T-Stick and measuring the remaining power when the T-Stick is on battery power. Hardware components such as regulators, and fuel gauges, as well as software components such as battery life estimation algorithms. 

| **ID** | **Requirements** | **Verification Method (IADT)** |
|----|----|----|
| **2** | **Power System** |    |
| 2.1 | The device will be able to be powered both wirelessly and wired. | Demonstration |
| 2.2 | The power system will be able to provide continuous power to the T-Stick for at least **2** hours on a single charge. | Test |
| 2.3 | The power system will be able to measure the battery voltage with an average error of less than **1%.** | Test |
| 2.4 | The power system will be able to measure the state of charge of the battery with an average error of less than **10%.** | Analysis |
| 2.5 | The power system will be able to estimate the battery life with an average error of less than **10%.** | Test |

### 2.1: The device will be able to be powered both wirelessly and wired.

The current generation of T-Sticks are both battery and USB powered, we are keeping this feature.

### 2.2: The power system will be able to provide continuous power to the T-Stick for at least **2** hours on a single charge.

Two hours is considered a reasonable amount of time to play and perform with the T-Stick before needing a charge. The number can be increased based on conversations with artist to determine what battery life we should be aiming for.

### 2.3: The power system will be able to measure the battery voltage with an average error of less than 1%.

Accurate battery voltage measurements allow the T-Stick to better estimate when the battery health is starting to decline. This is useful as it can give artist advanced warning of when their batteries need to be replaced.

### 2.4: The power system will be able to estimate the battery capacity of the battery with an average error of less than 10%.

Accurate battery capacity measurements allow the T-Stick to better estimate when the battery health is starting to decline. This is useful as it can give artist advanced warning of when their batteries need to be replaced.

### 2.5: The power system will be able to estimate the battery life with an average error of less than 10%.

Accurate battery life estimation is useful to artist as it gives feedback on when they should charge their T-Sticks

## 3. Sensor System Requirements

The Sensor System of the T-Stick manages the initialization, communication, and analysis of sensors in the T-Stick. This includes all the sensors excluding sensors related to power management and the software components that communicate with the sensors and process their data.

| **ID** | **Requirements** | **Verification Method (IADT)** |
|----|----|----|
| **3** | **Sensor System** |    |
| 3.1 | The sensor system should have a polling rate of at least **1000Hz** for continuous signals. | Test |
| 3.2 | The sensor system will have an average error of less than **1%.** | Analysis/Test |
| 3.3 | The sensor system will be able to detect when sensors are not communicating. | Demonstration |
| 3.4 | The sensor system will be able to identify sensors that are not communicating. | Demonstration |
| 3.5 | The sensor system will continue operating regardless of the states of the sensors | Test |
| 3.6 | The sensor system will have a calibration mode which enables artist to manually calibrate the sensors. | Demonstration/Test |
| 3.7 | The sensor system will be able to measure or approximate the following properties listed in Section 3 of the [T-Stick Design Guidelines](./Technical%20Requirements%20and%20Constraints/T-Stick%20Design%20Guidelines.md). | Demonstration |

### 3.1: The sensor system will have a polling rate of at least 1000Hz.

The sensor system needs have a high polling rate of the sensors to allow for fast controls on the T-Stick. See the [control and communication system requirement](./../5th%20Generation%20T-Stick%20Design%20Docs%20%5BARCHIVE%5D/Requirements%20Analysis/Control%20and%20Communication%20System%20Requirements.md).

### 3.2: The sensor system will have an average error of less than **1%.**

Highly accurate sensor measurements increase confidence for the artist that the T-Stick will do what they tell it to do.

### 3.3: The sensor system will be able to detect when sensors are not communicating.

Detecting sensor system errors is useful for troubleshooting problems with the T-Stick

### 3.4: The sensor system will be able to identify sensors that are not communicating.

Identifying which sensors are not communicating is useful as it allows the TY-Stick to disable them, and skip trying to poll them.

### 3.5: The sensor system will continue operating regardless of the states of the sensors

The entire T-Stick should keep working even if some sensors are not communicating. Furthermore, it makes it more obvious for artist as to which sensor is not working.

### 3.6 The sensor system will have a calibration mode which enables artist to manually calibrate the sensors.

Calibration is important, as it improves sensor accuracy and precision, artist should have the option to use a calibration mode to improve the performance of the T-Stick.

## 4. Reliability and Maintainability

As the name suggests this section contains all requirements relating to reliability and availability. This includes a PIR and PMR target for the T-Stick. We use the model defined in INSERTREFERENCEHERE for computing the PIR and PMR of the T-Stick. The robustness requirements are to ensure the T-Stick can handle elevated levels of shaking and jabbing for short periods of time without permanent failures.

| **ID** | **Requirements** | **Verification Method (IADT)** |
|----|----|----|
| **4** | **Reliability and Availability** |    |
| 4.1 | The T-Stick will have a [Practice/Performance Interruption Rate (PIR)](./Availability%20Modelling.md) of 1%. | Analysis |
| 4.2 | The T-Stick will have a [Playing/Maintenance Ratio (PMR)](./Availability%20Modelling.md) of at least 1. | Analysis |
| 4.3 | The T-Stick will be robust to jabs. | Test |
| 4.4 | The T-Stick will be robust to shakes. | Test |

### 4.1: The T-Stick will have a Practice Interruption Rate (PIR) of 1%

Low PIR means that artist can be more confident with using the instrument without having to constantly require maintenance from a technician/luthier.

### 4.2: The T-Stick will have a Performance/Maintenance Ratio (PMR) of at least 1.

A high PMR ratio means that we get a large amount of performance hours per hour of maintenance.

### 4.3:  The T-Stick will be robust to jabs.

Jabs are an important gesture for the T-Stick. Performers should be able to do them freely without worrying about failures.

### 4.4: The T-Stick will be robust to shakes.

Shakes are an important gesture for the T-Stick. Performers should be able to do them freely without worrying about failures.

## 5. Manufacturing Requirements

The manufacturability Requirements are all the requirements related to the manufacturing of T-Sticks including constraints on the Bill of Materials (BOM), required documentation, and time to assemble the T-Stick. 

| **ID** | **Requirements** | **Verification Method (IADT)** |
|----|----|----|
| **5** | **Manufacturability** |    |
| 5.1 | The T-Stick will follow the design guidelines and requirements outlined in sections 1 and 2 of the [T-Stick Design Guidelines](./Technical%20Requirements%20and%20Constraints/T-Stick%20Design%20Guidelines.md). | Demonstration |
| 5.2 | The physical design documentation will include a bill of materials. | Demonstration |
| 5.2.1 | The bill of materials will have fewer than 64 individual parts, including fly wires, screws, nuts, and heat shrink. | Demonstration |
| 5.2.2 | The bill of materials will have fewer than 40 distinct types of parts. | Demonstration |
| 5.3 | The physical design documentation will include a schematic. | Demonstration |
| 5.4 | The physical design documentation will include assembly instructions. | Demonstration |
| 5.5 | The mean time to assemble one T-Stick, not counting the time to gather parts and materials, will be less than 5 hours. | Test |
| 5.6 | The final assembly and repair of the T-Stick will be possible using only a soldering iron, wire stripper/cutter, heat gun, saw, and hex key. | Demonstration |
| 5.7 | The T-Stick will use common readily available parts and materials. | Demonstration |

### 5.1: The T-Stick will follow the design guidelines and requirements outlined in Sections 1 and 2 of the [T-Stick Design Guidelines](./Technical%20Requirements%20and%20Constraints/T-Stick%20Design%20Guidelines.md).

standardisation of design…

### 5.2: The physical design documentation will include a bill of materials.

As an open source project that we want others to replicate, a bill of materials is important. We include this as a requirement to ensure it is done as part of the design cycle and not as an afterthought.

### 5.3: The physical design documentation will include a schematic.

A schematic is useful for builders as it shows them how all the electronics are connected.

### 5.4: The physical design documentation will include assembly instructions.

As an open source project that we want others to replicate, a bill of materials is important. We include this as a requirement to ensure it is done as part of the design cycle and not as an afterthought.

### 5.5: The mean time to assemble one T-Stick, not counting the time to gather parts and materials, will be less than 5 hours.

The T-Stick should not take more than a day to build for new builders.

### 5.6: The final assembly and repair of the T-Stick will be possible using only a soldering iron, wire stripper/cutter, heat gun, saw, and hex key.

The T-Stick should be able to be built using common tools to help facilitate low-cost manufacturing.

### 5.7: The T-Stick will use common readily available parts and materials.

The T-Stick should be able to be built using common components to help facilitate low-cost manufacturing.