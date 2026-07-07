An *Interface Control Document* is a critical tool for systems that interact with users and/or other systems.

A description should be given of every interface of your system. You should discuss voltages and current rating, high voltage isolation, circuit protection, connectors (type of connector, physical location, pinout), communication protocols (baud rate, data types, etc.) and anything else necessary for someone to understand how your system interacts with nearby systems. You should not provide a detailed explanation of how your system works (that should go in a separate doc in your system folder).

# 1. BMS Master
## 1.1. CAN
##### CAN Protocol
The BMS has two CAN interfaces, or two independent CAN busses (named CAN A and CAN B)
1. **High Priority CAN (CAN A):** This will be for communication with the inverter.
2. **Low Priority CAN (CAN B):** This will be for sending data to be used by telemetry.

| Baud rate | CAN ID offset | CAN Message ID format |
| --------- | ------------- | --------------------- |
| 250Kbps | 0x12C | Standard (11-bit identifiers) |

Each of these default parameters can be configured as necessary, for example, the BMS will send an extended CAN ID frame for communication to the ELCON charger.
##### CAN Format
All messages have a length of 8 bytes and are in little-endian format, thus messages with less than 8 bytes of information will still have a length of 8 bytes. 

Each data frame is 108 bits (or 126 bits with an extended ID), and so at 250Kbps the bus can handle a maximum of 1984 to 2314 messages per second.
##### CAN Data Formats
Message data is formatted and scaled as follows:
| Data | Description | Type | Range | Factor 
| ---- | ----------- | ---- | ----- | ------ |
| Boolean | 1=true/on; 0=false/off | unsigned byte | 0 or 1 | 0 |
| Cell Voltage | Voltage (in mV) times 10 | unsigned 16-bit integer | 0 to 6553.5 mV | 0.1 |
| Low Voltage | Voltage (in V) times 100 | signed 16-bit integer | -327.68 to 327.67 V | 0.01
| High Voltage | Voltage (in V) times 10 | signed 16-bit integer | -3276.8 to 3276.7 V | 0.1
| Temperature | Temperature in °C times 10 | signed 16-bit integer | -3276.8 to 3276.7 °C | 0.1

##### CAN Database File
*a link will be placed here to access a .dbc file of the CAN network*
## 1.2. Digital Outputs
## 1.3. isoSPI
## 1.4. Energy Meter Passthrough
## 1.5. Happy Lights
## 1.6. Power (GLV)
## 1.7. Connection to TB Carrier Board


# 2. BMS Slave
## 2.1. isoSPI
## 2.2. Power (Buck Converter)
## 2.3. Flex PCB Connector
Also something to indicate whether the flex PCB is plugged in properly.
## 2.4. Happy Lights
## 2.5. Energy Meter Passthrough


# 3. Flex PCB
## 3.1. Connection with Slave Boards
## 3.2. Connection to Voltage Taps
## 3.3. Thermistors
## 3.4. Fusing
## 3.5. Mounting & Mechanical Interface
