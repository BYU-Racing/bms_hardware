An *Interface Control Document* is a critical tool for systems that interact with users and/or other systems.

A description should be given of every interface of your system. You should discuss voltages and current rating, high voltage isolation, circuit protection, connectors (type of connector, physical location, pinout), communication protocols (baud rate, data types, etc.) and anything else necessary for someone to understand how your system interacts with nearby systems. You should not provide a detailed explanation of how your system works (that should go in a separate doc in your system folder).

# 1. BMS Master
## 1.1. CAN
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
