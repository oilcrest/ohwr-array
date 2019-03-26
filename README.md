# Overview

ARRAY is a system for silicon sensor testing. It consisting of two Printed Circuit Boards:
* an active 512-to-1 switching matrix,
* a passive probe card to contact the sensor.

All design files are open source:
* The hardware design files for both PCBs can be found [here](https://ohwr.org/project/array/array-hardware)
* The firmware can be found [here](https://ohwr.org/project/array/array-firmware)
* A python interface can be found [here](https://ohwr.org/project/array/array-interface-python)
* A LabVIEW interface can be found [here](https://ohwr.org/project/array/array-interface-labview)


## Hardware

* Initial design can be found [here](https://gitlab.cern.ch/skulis/HGCSensorProbeCard/tree/master/hw)
* Finished design can be found [here](https://edms.cern.ch/ui/#!master/navigator/item?I:1907582863:1907582863:subDocs)
  - [schematic v1](https://edms.cern.ch/ui/file/1727299/1/EDA-03518-V1-0_sch.pdf)
  - [schematic v2](https://edms.cern.ch/ui/file/2026152/1/EDA-03518-V2-0_sch.pdf)
* 136 probe card can be found [here](https://edms.cern.ch/ui/#!master/navigator/item?P:1929548210:1680758176:subDocs)
  - [schematic](https://edms.cern.ch/ui/file/1727170/1/EDA-03517-V1-0_sch.pdf)
  - [layout](https://edms.cern.ch/ui/file/1727172/1/EDA-03517-V1-0_pcb.pdf)

### Known issues
 - capacitor **C176** should be not mounted by default (if it is mounted one can not program the chip with ISP)
 - transistor **T7** has drain interchanged with source. Quick fix: mount upside  down and rotated, as presented below.
 
   ![t7](https://gitlab.cern.ch/skulis/HGCSensorProbeCard/raw/master/hw/documentation/bugs/t7.jpg)

 - pull up resistors are missing on DOUT of all ADG1414 ICs (IC90 - IC153). 
    * Quick fix: add 33kOhm resistor between pins 22 and 23. 
    * In case of PCB redesign: add 33kOhm between pin 22 and +3.3V
 - resistor **R579** should be not mounted

## Firware

* Initial design can be found [here](https://gitlab.cern.ch/skulis/HGCSensorProbeCard/tree/master/fw)

  
## Debugging

* confirm that all LED's are on LD1, LD2 LD9, and LD10
* measure voltages at TP23 - TP28 (they should be within +/- 10%)
  * if voltages are OK -> most likely the short is on the "signal path"
  * if one or more voltages are out of spec (usually lower voltage) -> most likely a short on power pins (os power inputs of one of the chips)
* debugging signal paths, which to IV mode
  * select CHN0
    * for channel 0 resistance between switching card input (left-hand side of the protection resistor) and ground should be high >> MOhms
    * for channel 1 (or any other) resistance between switching card input (left-hand side of the protection resistor) and ground should be around 10KOhm
  * check the impedance between the selected input (S1..S8) and the output (D)
  

## Images

![conectivity](https://gitlab.cern.ch/skulis/HGCSensorProbeCard/raw/master/doc/img/channels.png)

