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

## Technical specifications

| name | value |
| ---- | ----- |
| cpu | stm32f105 (ARM; Flash: 128kB; 72MHz; SRAM: 64kB) |
| feedback | usb: ch340g (only 115200 boud) |
| power unit | 24V 5A (120w) |

## Specifications

### Technique

| name | value |
| ---- | ----- |
| cpu | stm32f105 (ARM; Flash: 128kB; 72MHz; SRAM: 64kB) |
| feedback | usb: ch340g (only 115200 boud) |
| power unit | 24V 5A (120w) |
| firmware | own firmware based on marlin 1.1.0-RC6 (2016-04-24 12:00) |
| gcode | marlin 1.1.0 + own set of instructions |

The processor's performance fully covers the printer's capabilities, but the feedback significantly limits it due to the standard data transfer rate of 115200 baud. This is the first printer I know that prints better from a USB flash drive.

#### Power unit
A 24V 5A (120W) power supply is used, the reason is unknown, but from the factory this power supply showed 25.2V, in general, an excess of 0.2V is justified, since it allows you to compensate for losses on the wires, but here the excess is as much as 1.2V, which is very bad for the printer's electronics, since all its components (even just fans, heaters) are designed exclusively for 24V. My possible theory is that this excess is most likely done intentionally, since the printer experiences sagging when the heater and table are simultaneously heated by 1.2V.

Also, this power supply does not have any cooling capabilities and heats up with prolonged use, but overall it is bearable.

I had an old Mean Well S-150-24 power supply (24V ~6.5A, ~150W) lying around in the bins, not the best choice, but reliable. I set it to 24.2 V and made a double wire to power the printer. As a result, the drop was 0.2 V at the moment of simultaneous heating of the extruder and the table, which suited me quite well.

### Physical

A thick aluminum plate on which the modular guides are located. The modular guides are based on a stepper motor + rigid coupling + four-way trapezoidal shaft, on top of the guide there is a thin aluminum plate with a conventional limit switch. The guides used are absolutely identical to the guides along the X, Y, Z axes, the order of connection to the motherboard determines the belonging of the guide to the desired axis. The moving carriage is held by openbuilds rollers.


