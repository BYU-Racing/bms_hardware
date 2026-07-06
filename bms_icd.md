An *Interface Control Document* is a critical tool for systems that interact with users and/or other systems.

A description should be given of every interface of your system. You should discuss voltages and current rating, high voltage isolation, circuit protection, connectors (type of connector, physical location, pinout), communication protocols (baud rate, data types, etc.) and anything else necessary for someone to understand how your system interacts with nearby systems. You should not provide a detailed explanation of how your system works (that should go in a separate doc in your system folder).

# 1. BMS Master
## 1.1. CAN
The BMS Master will have two CAN line pairs.
1. **High Priority CAN:** This will be for communication with the inverter.
2. **Low Priority CAN:** This will be for sending data to be used by telemetry.
## 1.2. Digital Outputs
The BMS Master will have a digital output pin that pulls high for normal and to ground for fault. The digital output will be sent out of the TB through the TB Carrier Board or directly through the TB Bulkhead Connector
## 1.3. isoSPI
The BMS master will communicate with the BMS Slaves through a series isoSPI connection. The LTC6811-1 BMS Slave ICs are already configured for this. A digital isolator will be selected to protect the BMS Master from the HV Section of the TB Carrier Board. The isoSPI connector will be a MOLEX micro fit jr. 
## 1.4. Energy Meter Passthrough
The BMS Master board will pass a connection from the BMS Slaves to the TB Carrier Board. This will have no circuitry nearby in order to prove that the energy meter signal is clean. HV spacing will be used (if required). The energy meter wires will connect through the same MOLEX micro fit jr.
## 1.5. Happy Lights
The BMS Master will have labelled indicator lights that represent each BMS state, the value of the digital output(s), and other indicator lights as deemed necessary.
## 1.6. Power (GLV)
The BMS will receive and tolerate fused 12V-15V power input. The BMS is expected to draw less than 500mA max. 
## 1.7. Connection to TB Carrier Board
The BMS Master may connect to a larger carrier board in the Tractive Battery, using breadboard headers. 


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
