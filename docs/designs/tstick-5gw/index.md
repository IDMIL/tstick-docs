# General Information

The T-Stick 5GW consists of a custom ESP32 board which integrates a ESP32-S3 WROOM 2 Module with a ICM20948 IMU and MAX17055 on a single board, and a touch board that has a pinout for the Trill Craft board as well as, two JST-SH 4 pin connectors to daisy chain multiple touch boards together.

## System Architecture

The image below shows the hardware architecture for the new T-Stick design. Most of the power sytem functions such as providing power, charging the instrument and changing the power state is handled by the MCP73871. This IC handles charging the LiPO/Li-ion battery and changing between the USB power and battery power depending on voltage. In addition, two regulators, the NCP167AMX330TBG/NCP167AMX1800TBG series are used to step down the system power to 3.3V and 1.8V respectively. The MAX17055 is used as a fuel gauge. This fuel gauge is used over its non-current sensing counter parts such as the MAX17048 due to better accuracy.

 ![Figure 1: T-Stick 5GW Architecture](../Images/TStick-HardwareArchitecture-Pro.png)

The Trill Craft board is kept as the capacitive sensor solution of choice. A more integrated solution using just the MCU on the Trill Craft board was considered but figuring out how to flash the MCU in a systematic way, would have been more of a hassle than it is worth. The touch board uses a 32 pin FFC connector to connect to a flexible PCB with 30 touch points and two ground points. The IMU is changed to an ICM20948 9-DOF IMU. as mentioned previously this is due to the fact that the LSM9DS1 is no longer actively supported by the company that produces it. It receives the 1.8V power from one of the regulators. Three mosfets are used to convert the 1.8V logic from the ICM20948 to 3.3V to communicate with the ESP32. 

### 5th Generation T-Sticks
Click each box to get more information on each variant of the T-Stick 4GW

<div class="grid cards" markdown>

- __T-Stick 5GW-Trill__ 

    ---

    An ESP32-S3 based T-Stick using the Bela Trill Touch Board.

    [:octicons-arrow-right-24: More Details](./specs_5gw_trill.md)

- __T-Stick 5GW-Enchanti__ 

    ---

    An ESP32-S3 based T-Stick using a custom touch board.

    [:octicons-arrow-right-24: More Details](./specs_5gw_enchanti.md)

</div>

### Diagrams

 ![ESP32 Board Diagram](./Images/pcb_layout_components.png)

 ![Touch Board Diagram](./Images/touch-board-schematic-view.png)

### Schematic

 ![Custom ESP32 Board Schematics](./Images/tstick-5GW-schematic.png)

 ![Touch Board Schematic](./Images/tstick-touch-board-schematic.png)
