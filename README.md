<div id="header" align="center">

<p align="center"><img src="./img/main.jpg" width="40%"></img> <img src="./img/main2.jpg" width="21%"></img></p>

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
I have been developing devices similar to 3D printers for a long time, I even created one self-assembling Cartesian printer based on a klipper (stm32f407, rails, belts) practically from scratch and one fine day, while studying a local trading platform, I came across this small and interesting printer. Initially, I was not interested in the quality of its 3D printing (I thought that if it prints, then it is already good), and I was only interested in its CNC capabilities and 3 in 1 technologies (3D, CNC, LASER).

My specific printer was manufactured in 2020-2021, and the printer model itself was first manufactured even earlier, around 2017-2018.

## Disclaimer
| :boom: Disclaimer |
|:------------------|
| :warning: Snapmaker is a registered trademark. The author has no affiliation with Snapmaker and does not provide hardware advice. For official support, please refer to the contacts listed on snapmaker. |
| :warning: Your actions and the information described here are entirely at your own risk. The author is not responsible for any damage to your devices. |
| :warning: All information provided is based on personal research and may contain errors. |
| :warning: This material is for informational purposes only. |

## Specifications

### Technique

#### Brain

| name | value |
| ---- | ----- |
| cpu | gd32f105rc6 (ARM; Flash: 256kB; 72-108MHz; external 16Mhz clock; SRAM: 96kB) |
| feedback | usb: ch340g (only 115200 baudrate, or 250000_baudrate/500000_baudrate in custom firmware, stable 921600 baudrate!) |
| power unit | 24V 5A (120w) |
| factory firmware | own firmware 2.11 based on marlin 1.1.0-RC6 (2016-04-24 12:00), gcode: marlin 1.1.0 + own set of instructions |
| firmware | ... <a href="./firmware/README.md">See all</a> |
| drivers | a4988 |

About factory firmware: The processor's performance fully covers the printer's capabilities, but the feedback significantly limits it due to the standard data transfer rate of 115200 baud. This is the first printer I know that prints better from a USB flash drive.

#### Factory Firmware Values ​​and Limitations

| name | value |
| ---- | ----- |
| steps per unit | X 400.00, Y 400.00, Z400.00, E92.60 |
| microsteps | 16 |
| maximum feedrates (mm/s) | X 300.00, Y 300.00, Z 5.00, E 25.00 |
| 3d maximum acceleration (mm/s2) | X 1000, Y 1000, Z 100, E 10000 |
| cnc maximum acceleration (mm/s2) | X 100, Y 100, Z 100, E 100 |
| laser maximum acceleration (mm/s2) | X 3600, Y 3600, Z 3600 |
| accelerations printing | 1000.00 |
| accelerations retract | 1000.00 |
| accelerations travel| 1000.00 |
| min feedrate (mm/s) | S0 |
| min travel feedrate (mm/s) | T0 |
| minimum segment time (ms) | B20000 |
| maximum XY jerk (mm/s) | X20.00 |
| maximum Z jerk (mm/s) | Z0.40 |
| maximum E jerk (mm/s) | E5.00 |
| 3d work area | 125x125x125 mm |
| laser work area | 125x125 mm |
| cnc work area | 90x90x50 mm |

The printer manufacturer recommends a default head movement speed of 100 mm/s during printing, and a print speed of 40/50/60 mm/s and a retraction speed of 60 mm/s (at a distance of 5 mm).

The printer has one bad feature in the factory firmware, namely if you forgot to move the carriage home after printing, and it is in the maximum position (and after printing it is always in the maximum position), then after turning the printer off and on and pressing the home button, you will get a short-term impact of the head on the Z-axis limiter. The impact itself on the Z-axis limiter is not very critical, but very unpleasant and can lead to self-unscrewing.

### Physical
A thick aluminum plate on which the modular guides are located. The modular guides are based on a stepper motor + rigid coupling + four-way trapezoidal shaft, on top of the guide there is a thin aluminum plate with a conventional limit switch. The guides used are absolutely identical to the guides along the X, Y, Z axes, the order of connection to the motherboard determines the belonging of the guide to the desired axis. The moving carriage is held by openbuilds rollers.

#### Accuracy
The design features of the printer and the trapezoid shaft in the guides in combination with the "oak" a4988 should have shown good results, the manufacturer himself assures the accuracy of 50-300 microns. I calibrate each thread for accuracy and enter the data into the slicer, measuring with a caliper with a resolution of 0.01 mm and an error of 0.02 mm. In general, I get:

|                 NAME                      | PETG (default firmware)  | PLA (default firmware)  | PLA(klipper firmware +pa+is) |
| ----------------------------------------- | ------------------------ | ----------------------- | ---------------------------- |
| min absolute deviation (X and Y axes)     |         ~0.02mm          |         ~0.02mm         |            ~0.01mm           |
| average absolute deviation (X and Y axes) |         ~0.08mm          |         ~0.12mm         |            ~0.07mm           |
| max absolute deviation (X and Y axes)     |         ~0.17mm          |         ~0.20mm         |            ~0.09mm           |

In general, I have summarized many results of different filaments under the general one and described the general deviation of the two axes. I would also like to note that this printer gives more accurate results on the X-axis than on the Y-axis.

<b>The section is not finished yet.</b>

#### Cooling
Almost all of them use 24V fans, connected directly to 24V, i.e. they are uncontrollable. All fans are absolutely tiny and create a lot of noise, the saddest thing is that they are not very productive and I once managed to catch a traffic jam in the extruder due to not very good weather conditions.

It is recommended to replace almost all fans with larger ones.

#### Display
A very good solution, you can just take it as a phone and control the printer, a display with good resolution and more or less high-quality color gamut, not requiring a stylus. The solution is a ready-made purchased uart solution with its own microcontroller and program. The display is poorly compatible with the standard gcode for text displays and, for example, does not allow much under octoprint. I repeat that this display does not receive an image from the main microcontroller, but is independent.

### 3 In one

#### Extruder (3D)
A classic extruder built on the basis of an unknown to me full-size nemo 17 (1.8°(200), 42HD4414-07, 2020/08/19) from mocotech and gears (1:1, factory e-steps 92.60), a radiator noticeably larger than its classic versions, a convenient unknown to me thermal barrier, which involves fastening by screwing in one countersunk screw. By selection, it was established that the heating block itself is E3D V5, but with an unknown to me thermal barrier, which does not imply unscrewing from the block.

##### Bad design #1 (3D)
Instead of a capsule thermistor, a "droplet" type is used; the sensor itself is simply suspended inside the heating block and can move freely within it.

##### Bad design #2 (3D)
The manufacturer has provided a way to easily remove the cover and unscrew the fuser unit, but the rigid heating wires make it somewhat difficult to remove. Furthermore, if the "plastic plug" accidentally gets into the extruder during printing, the entire print head must be disassembled, a very time-consuming and tedious task.

##### Bad design #3 (3D)
The heating block itself is not insulated and, combined with an ineffective PID controller, the temperature fluctuates constantly.

##### Bad design #4 (3D)
While twisted pair cable is certainly an interesting and attractive solution when combined with a classic RJ45 connector, the cable cross-section from the "brain" to the extruder head proved unsatisfactory. Significant heating was observed, and the cable at best delivers 1.49 A with a voltage drop of 1.5 V (using an extruder with an output power of ~40 W will only deliver ~35 W, and even then, the resistance will fluctuate as the heater heats up. Using more powerful heaters of 50-60-80 W is impossible. Switching to an external MOSFET with a higher-quality cable resulted in a voltage drop of 0.1-0.2 V and an output power of approximately ~38 W using the same heater block, as well as the possibility of using more powerful extruders).

#### Bed (3D)
The textolite is small in size (128x128 mm), heating is exclusively resistive (24V, did not determine the power), heating up to 60-65 degrees is preferable (It is believed that temperatures above 80 degrees can damage the sticker coating). The main disadvantage of this table is the lack of insulation and all the heat is directed both to the platform itself and to heating its base (guide). Also, the bolts for fastening the platform to the guide are slightly larger than required, because of this, the screws themselves cut into the sticker glued to the platform a little (it is recommended to simply add a washer between the screw and the carriage, and then the screw will never damage the coating.). Another plus is that this sticker does not require any glue at all when printing PLA / PETG.

The first layer is calibrated in the printer very poorly, the calibration of the first layer is more truthful only at the moments of full heating of the platform, which the manufacturer did not provide for in the firmware. After calibrating the surface, you can more clearly evaluate the first layer on the model https://www.thingiverse.com/thing:3797458 (I am not the author of this model, it is simply in the public domain), and then perform the final calibration based on the model.

#### Spindle (CNC)
<img src="./img/cnc.JPG" width="11%"></img>
<img src="./img/cnc2.JPG" width="11%"></img>

Uses a weak spindle 30W RBI-365024 24V, the main software assumes the use and configuration of specific cutters, the ability to perform drilling was not found. There are many shortcomings, no automatic centering, no speed control, a lot of noise during operation. The spindle control board is supposedly designed for control, but in the copy that I had, the board actually consisted of two resistors that do not assume speed control, there is only on / off control, carried out by the main brain board.

Also one of the minuses - the fastening of cutters / drills is not very good.

The spindle itself consists of a BLDC DC motor, MOSFET transistors, and a 4931ET driver (the electronics are hidden inside the spindle). The following pins are used for connection: AR, FG, FR, PWM, GND, and VCC (interestingly, there is a thick layer of solder between the PWM and GND pins from the factory).

#### Laser
<img src="./img/laser.JPG" width="11%"></img>

I have hardly used it and have not tested it. There is a dc/dc converter board inside and presumably the feedback and dc/dc regulation works. (will be added).

### Mods

#### Cooling of the thread (3D)
Cooling of the filament during printing is arranged in the strangest way, in general it is enough for someone, but for beginners I recommend printing and using https://www.thingiverse.com/thing:3403426 (I am not the author of this model, it is simply in the public domain)

#### Spool holder (3D)
<a href="./mods/SpoolHolder.md">See</a>

#### Thread Spool Holder (3D)
The thread holder allows you to correctly position the thread flow at a certain height, together with the modification of the holder, this is a comprehensive solution. Also, one of the advantages of this holder is that it allows you to easily move the engine control screen to the very top. https://www.thingiverse.com/thing:2757715 (I am not the author of this model, it is simply in the public domain)

#### Power unit
<a href="./mods/PowerUnit.md">See</a>

#### Strange Y-axis settings (settings for factory firmware only)
Initially, one oddity was noticed in the printer: if the X and Z axes were correctly limited by software and did not reach the limit, then the Y axis at the possible maximum slightly crashed into an obstacle. In general, this is not critical, since it crashed only one step and there is such a possibility that this is only me, but here is the fix:

```gcode
M1025 X131.00 Y128.00 Z128.00
M500
```
This g-code will determine the maximums for the axes and save the changes.

#### Brain cooling (cooling)
<a href="./mods/BrainCooling.md">See</a>

#### Octoprint (3D)
<a href="./mods/BrainCooling.md">See</a>

#### UART (feedback)
<a href="./mods/Uart.md">See</a>

#### Volcano (3D)
<a href="./mods/Volcano.md">See</a>

#### Gaps in the guides
The Y-guide design is not very good and involves large gaps through which debris can get in and affect the trapezoid screws; from time to time, various debris can get in there, including bolts or nuts (which, by the way, once happened to me), and especially considering that the manufacturer also assumes milling on this printer, the issue of debris is very acute.

There was a solution on the Internet using a paper accordion filter, which in theory can be made by yourself and the necessary parts can be printed for it https://www.thingiverse.com/thing:2828419 (I am not the author of this model, it is simply in the public domain), at the moment I have not used this modification.

#### TMC2209? (stepper motor drivers)
In general, it would be possible to simply desolder the a4988 with a hair dryer and replace them with tmc2209, since they have similar pinout, and also change the harness a little and maybe even run the setup via uart and sensorless pointing, but at the moment I decided not to do this. The reason for using tmc2209 is simple, it is the ability to greatly reduce the noise of the stepper motors, but the StealthChop algorithm can also cause problems with circular geometry, and because of the a4988, the stepper motors are very noisy even in standby mode.

#### Klipper (firmware)
Yes, this printer and this motherboard can be updated with Klipper, you can find the firmware in the firmwares called Klipper, you can simply follow the instructions and update the firmware without using JTAG or other means, just drop the file on a flash drive. Future updates of Klipper can be just as easy, also you can revert to the factory firmware at any time or to any other firmware.

| name | version | mcu | rate |
| ---- | ----- | ----- | ----- |
| Klipper_6_2025Demo460800.Bin | 121 commands, v0.12.0-452-g75a10bfca-dirty-20250308_020116-r510 / gcc: (Arch Repository) 14.2.0 binutils: (GNU Binutils) 2.43) | GD32F105RC6 | uart 480600 baudrate |

<a href="./firmware/Klipper.md">See</a>

#### Resonance compensation (only for klipper firmware)
<a href="./resonances/Readme.md">See</a>

#### Cura (slicer)
<a href="./cura/Readme.md">See</a>

#### My configuration (2025)

| name | value |
| ---- | ----- |
| heat block | volcano Plated Copper with insulator (TriangleLab) |
| heater | 24V 40W (TriangleLab), factory power limitation for the wires is approximately ~35W |
| sensor | 104NT-4 R025H42G in the sleeve (TriangleLab) |
| nozzle | E3D Volcano 0.4 (TriangleLab) |
| thermal barrier | unknown (the factory hole diameter was used, the thread was cut without additional drilling, and the heat break was simply selected and is unknown to me (the modifications to the heatsink suggest compatibility with factory heat breaks)). |
| lighting | ws2812b ribbon (5V, RP2040) |
| fan | 50mmX50mm 12V extruder (always on), DEFAULT CONFIGURATION |
| firmware | brain: klipper (v0.12.0, UART 921600baudrate), rp2040: klipper (v0.12.0, USB) |

#### My configuration (2026)

| name | value |
| ---- | ----- |
| heat block | volcano Plated Copper with insulator (TriangleLab) |
| heater | 24V 40W (TriangleLab), external MOSFET LR7843+new_wiring (support: 40,50,60,80..~120W) |
| sensor | 104NT-4 R025H42G in the sleeve (TriangleLab) |
| nozzle | E3D Volcano 0.4 (TriangleLab) |
| thermal barrier | titanium V6 (TriangleLab) (the heatsink was drilled out to a new, larger diameter, a new thread was cut, and an additional hole was made in the heatsink for installing another mounting screw for the heat break.) |
| wiring | general protection of all grounded wires, general grounding |
| lighting | ws2812b ribbon (5V, RP2040) |
| fan | 50x50mm 12V cooling extruder (only ON/OFF, always enabled by default if there is no control from the MCU, dc-dc LM2596S, PCA9685+LinuxMcu), default print_fan 24V (PWM 0-100%, module mosfet LR7843, PCA9685+LinuxMcu), 80x80mm 5V power unit (only ON/OFF, always enabled by default if there is no control from the MCU, dc-dc LM2596S, PCA9685+LinuxMcu+DS18B20), 80x80mm brain 5V cooling fan (PWM 0-100%, module mosfet LR7843, PCA9685+LinuxMcu+GD32F105InternalADCSensor)|
| firmware | klipper (v0.13.0, UART 460800baudrate), rp2040: klipper (v0.13.0, USB), linux_mcu: klipper (v0.13.0, internal process) |

## General impressions
<img src="./img/imprint2.JPG" width="11%"></img>
<img src="./img/imprint3.JPG" width="11%"></img>

I liked the printer first of all for its assembly, it is completely aluminum, there are very few plastic parts, the printer creators even used thread locks and the idea of ​​3 in one is very catchy, but it has a very strong drawback, namely NOISE, which can be reduced by modifying the fans and ultimately the drivers, spindle...

As for the price, it turned out that this printer did not cost me that much, since the authors cut it out of their line, but at the same time, if I needed 3D printing, I could have initially bought something similar fast on "klipper".
