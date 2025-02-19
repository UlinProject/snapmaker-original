<div id="header" align="center">

<p align="center"><img src="./img/preview.jpg" width="40%"></img></p>

  <b>[snapmaker-original]</b>
  
  (Information about this 3D printer (Snapmaker original), set of modifications)
  </br></br>
<div id="badges">
  <a href="https://github.com/denisandroid">
    <img src="https://github.com/UlinProject/img/blob/main/short_32/uproject.png?raw=true" alt="uproject"/>
  </a>
</div>
</div>

## Description
I have been developing devices similar to 3D printers for a long time, I even created one self-assembling Cartesian printer based on a clipper (stm32f407, rails, belts) practically from scratch and one fine day, while studying a local trading platform, I came across this small and interesting printer. Initially, I was not interested in the quality of its 3D printing (I thought that if it prints, then it is already good), and I was only interested in its CNC capabilities and 3 in 1 technologies (3D, CNC, LASER).

## Disclaimer
The information presented here is solely my opinion and may be both useful and harmful to the end user. All actions described are solely my experience, the end user can repeat my actions only at their own risk. Damage to your device can occur at any stage of the end user's actions.

Snapmaker is a registered trademark, to which I have no relation, you can always consult using the official contacts listed on the snapmaker.com website.
All rights reserved.

## Specifications

### Technique

| name | value |
| ---- | ----- |
| cpu | stm32f105 (ARM; Flash: 128kB; 72MHz; SRAM: 64kB) |
| feedback | usb: ch340g (only 115200 boud) |
| power unit | 24V 5A (120w) |
| firmware | own firmware based on marlin 1.1.0-RC6 (2016-04-24 12:00) |
| gcode | marlin 1.1.0 + own set of instructions |
| drivers | a4988 |

The processor's performance fully covers the printer's capabilities, but the feedback significantly limits it due to the standard data transfer rate of 115200 baud. This is the first printer I know that prints better from a USB flash drive.

### Physical

A thick aluminum plate on which the modular guides are located. The modular guides are based on a stepper motor + rigid coupling + four-way trapezoidal shaft, on top of the guide there is a thin aluminum plate with a conventional limit switch. The guides used are absolutely identical to the guides along the X, Y, Z axes, the order of connection to the motherboard determines the belonging of the guide to the desired axis. The moving carriage is held by openbuilds rollers.

#### Accuracy
The design features of the printer and the trapezoid shaft in the guides in combination with the "oak" a4988 should have shown good results, the manufacturer himself assures the accuracy of 50-300 microns. When 3D printing with non-factory plastic, measuring with a not very precise tool, I got a deviation of ~ 0.2 mm along the Y axis from the original dimensions of the model, which was generally successfully corrected by software.

#### Power unit
A 24V 5A (120W) power supply is used, the reason is unknown, but from the factory this power supply showed 25.2V, in general, an excess of 0.2V is justified, since it allows you to compensate for losses on the wires, but here the excess is as much as 1.2V, which is very bad for the printer's electronics, since all its components (even just fans, heaters) are designed exclusively for 24V. My possible theory is that this excess is most likely done intentionally, since the printer experiences sagging when the heater and table are simultaneously heated by 1.2V.
You can determine the voltage drop simply by the sound of the fans, which are connected directly to 24 V here.

Also, this power supply does not have any cooling capabilities and heats up with prolonged use, but overall it is bearable.

I had an old Mean Well S-150-24 power supply (24V ~6.5A, ~150W) lying around in the bins, not the best choice, but reliable. I set it to 24.2 V and made a double wire to power the printer. As a result, the drop was 0.2 V at the moment of simultaneous heating of the extruder and the table, which suited me quite well.

#### Cooling
Almost everywhere 24V fans are used, connected directly to 24V. All fans are absolutely tiny and create a lot of noise, the saddest thing is that they are not very productive and I once managed to catch a traffic jam in the extruder due to not very good weather conditions.

#### Extruder
A classic extruder built on the basis of an unknown to me full-size nemo 17 (42HD4414-07 2020/08/19) from mocotech and gears (factory e-steps 92.60), a radiator noticeably larger than its classic versions, a convenient unknown to me thermal barrier, which involves fastening by screwing in one countersunk screw. By selection, it was established that the heating block itself is E3D V5, but with an unknown to me thermal barrier, which does not imply unscrewing from the block.

A significant drawback of the extruder is the use of a "drop" thermistor instead of a "capsule" one, the sensor itself simply dangles in the heating block. The manufacturer also provided a way to easily remove the lid and unscrew the thermal block, but due to the rigid wires of the heater, the extraction method is not the easiest. Also, if you accidentally catch the "plastic plug" in the extruder, you will have to sort out the entire head, and this is a very long and tedious task.

#### Bed (3D)
The textolite is small in size (128x128 mm), heating is exclusively resistive (24V, did not determine the power), heating up to 60 degrees is preferable. The main disadvantage of this table is the lack of insulation and all the heat is directed both to the platform itself and to heating its base (guide). Also, the bolts for fastening the platform to the guide are slightly larger than required, because of this, the screws themselves cut into the sticker glued to the platform a little. Another plus is that this sticker does not require any glue at all when printing PLA / PETG.

