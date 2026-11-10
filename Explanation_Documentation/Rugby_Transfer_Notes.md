# Rugby's BMS Transfer Notes 
11/10/2026

## Cell Monitor PCB TODOs/Notes:
- do math to prove Fuse ratings
	> for both 250mA fuses AND 500mA fuses
- fix CODE (hw.h file) to accurately reflect the new (V2.01) pinout for thermistors
- fix/adjust/decide on what connectors to use for thermistors
- fix the schematic symbol and footprint for the transformer
- Power rail (VREG) jumper is there so you can test and oscilloscope the current output from the buck converter
- I would suggest you to put the VREG LED close to the isoSPI connector so you can see the LED while the modules are in the tractive battery enclosure
- NEED to do ASAP: verify the old voltage tap THT footprints shape/size and verify that they are in the correct layout positions so that they line up with the module.
	> along with that, you will need to verify the PCB dimensions line up with the module correctly and the mounting hole positions are in the correct position
- fix/adjust/decide on how you are doing the daisy chain (1 connector with 4 pins, 2 connectors with 2 pins, or separate wires/connectors for a potential thermistor CAN bus?)
- Something to consider on the temperature sensing schematic (page 3): do you need the op-amp buffer? do you need the RC from the buffer into the GPIO pins on the LTC6811-1? do you need any other pull-ups/pull-downs for the MUX chips? I would suggest that you look at the MUX datasheet in more detail to find recommended layout and suggestions on the buffer thing to see if its necessary
- maybe find a new/better fuse block (cartridge style or something?). The current option is NOT automotive rated so maybe find a solution to that or at a minimum do some vibration testing to see if they stay in the cartridge
- FINISH PCB routing
	> no traces or components around the isolation transformer and connector (4mm isolation)
	> I would suggest that you test a couple options for copper pours around the balance resistors
	> follow the LT3990 layout recommendations when doing the power rail layout
	> follow the LTC6820 layout recommendations when doing layout for the isolation transformers


## Cell Monitor PCB Testing Recommendations:
- test full cell balancing
	> watch for heat on 33 ohm resistor (change resistance? change to dual 67 ohm parallel?)
- test different footprints for the voltage sense leads?

***

## Main Control PCB TODOs/Notes:
- change the flash chip schematic symbol and footprint to be not a 
- update/verify that you have a dedicated BMS SD OUPUT (HAPPY) signal decided and selected.
- I would suggest you include a GPIO expander and then use it for happy lights on this BMS Main Control PCB each respective light corresponding to an individual module
- CAN bus termination? should the CAN bus be terminated on this PCB or is it terminated elsewhere?
- FIX USB-C lines!! Someone needs to figure it out. Coordinate with the Inverter capstone team to see if we figured it out. We should get this working for the BMS, ECU, Sensor Hub, and Inverter.
- Verify isoSPI terminating caps and resistors (R205, R206, C202, and C201) are identical to the cell monitor PCB (or if they should intentionally be different?) Look at LTC6820 and LTC6811-1 datasheets and figure it out.
	> also remember to match IBIAS and ICMP resistor dividers (R203, R207, R204, and R208) to the cell monitor PCB as well
- need to select and order a USB-C waterproof panel mount connector to flash outside of tractive battery enclosure
- fix the connector that goes to the TB Main PCB connector/GLV plug. Just need consistency across all connectors with pinouts
- Harrison is very sensitive about the LED brightness so make sure the inline resistors with the LEDs are >4.7k ohm
- find a new footprint and package for the LMR33620 ?? Its really hard to solder to find a better automotive rated component and follow the layout guidelines
- talk to Harrison about this, but you might want to consider adding BOOT and RST btns to the STM32
- FINISH PCB ROUTING
	> fix isoSPI connector to be like the Cell Monitor PCBs (1 connector with 4 pins, 2 connectors with 2 pins)
	> fix and route USB-C connector with slot in PCB to join and mount the waterproof panel connector (ask Harrison about this and which orientation to put the USB-C on the PCB)
	> follow LMR33620CQ5RNXRQ1 datasheet layout recommendations or whatever IC you decide
	> follow AP2112k-3.3 datasheet layout recommendations
	> follow CAN transceiver datasheet layout recommendations
	> FOLLOW LTC6820 datasheet layout recommendations when doing the isolation transformer
	> KEEP THE ISOLATION RULES with the isoSPI connector and isolation transformer
	> fix J104 connector footprint and position


## Main Control PCB Testing Recommendations:
- get USB-C to work!! talk to inverter capstone about this
- different LED setups for visual module indicators

***

Other Notes/Links:
- DONT FORGET TO CONFORMAL COAT THE PCBS WHEN READY TO BE MOUNTED TO MODULES
- Transformer that Harrison suggested (HM0068ANLT): https://www.digikey.com/en/products/detail/pulse-electronics/HM0068ANLT/6148254
- Flash chip that seemed good (SST26VF064B-104I/SM): https://www.digikey.com/en/products/detail/microchip-technology/SST26VF064B-104I-SM/5033662
