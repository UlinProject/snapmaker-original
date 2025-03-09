## Description
A full featured clipper port for this printer, allowing you to overclock and expand the capabilities ("pressure advance", "input shaper", "bl-touch", "nozzle cleaner", "fan control", ...) of this printer using a single board computer and other additional microcontrollers.

## Disclaimer
The firmware presented here is provided as is, I am not responsible for your damaged devices. All information described here is solely my experience and can be both useful and harmful to the end user. You can reflash your printers only at your own risk. Damage to your device can occur at any stage of the end user's actions. All images and firmware presented here are the property of their authors.

Snapmaker is a registered trademark, to which I have no relation, you can always contact the official contacts listed on the website snapmaker.com. All rights reserved.

## Firmware

| name | value | stable |
| ---- | ----- | ----- |
| Klipper_6_2025Demo460800.Bin | Experimental current (as of 2025) demo firmware klipper | +-(only tests) |
| Klipper_7_2025_UART460800.Bin | Relevant for 2025, functionality is not cut, microcontroller frequency is set to factory. UART 460800 connection (via USB or directly). | +(only tests) |
| Klipper_8_2025_UART250000.Bin | Relevant for 2025, functionality is not cut, microcontroller frequency is set to factory. UART 250000 connection (via USB or directly). | +(only tests) |

## How to reflash?
1. Copy any file and rename it to Update.Bin to a USB disk formatted in Fat32.
2. Turn off the printer and insert the USB disk into the USB port.
3. Turn on the printer. If the LED changes as below, the update is successful.
- The blue LED blinks slowly for about 5 seconds.
- Then the LED turns off for about 2 seconds.
- The LED starts blinking quickly.
4. The flashing process is complete.

## Don't forget to remove the flash drive
The "klipper" firmware does not delete the "Update.Bin" file after flashing, so you can constantly reflash the device when you turn it on (even if you don't want to). It is better to either remove the flash drive or delete the "Update.Bin" file on it. In the Marlin firmware, this is done automatically.

## Is it possible to return to the factory firmware?
At any time, in the same way, by dropping the original Update.bin onto a flash drive.

## 460800 or 250000?
I can't give you an exact answer, but this printer works fine at 500000 baud, but officially klipper recommends 250000 and according to official statements this should be enough.

## How do I know if the firmware has loaded and is working?
When the microcontroller is turned on, the red LED on the "brains" lights up, after activating the "clipper" on the single-board computer, the LED on the "brains" stops lighting up (or continues to light up, if you did not specify this in the configuration).

## Run "printer.cfg"
Here I can't give exact recommendations what your "ideal" and correct configuration should be, it may differ, since my device is not so original. Speed ​​settings, acceleration, extruder steps, everything was adapted to the factory ones from the factory firmware. Just use it as a starter!

```toml
[include fluidd.cfg]

[virtual_sdcard]
path: /home/alarm/printer_data/gcodes
on_error_gcode: CANCEL_PRINT

[mcu]
serial: /dev/ttyS0 # or usb device
baud: 250000 # or 460800
restart_method: command

[printer]
kinematics: cartesian
max_velocity: 300 # test 140
max_accel: 1000 # test 3000
max_z_velocity: 5 # test 20
max_z_accel: 100 #  test 500
square_corner_velocity: 12.0 # test 4

[stepper_x]
step_pin: PB5
dir_pin: !PB6
enable_pin: !PB7
microsteps: 16
rotation_distance: 8 # 200 * 16 / 400.00
endstop_pin: ^!PC11
#position_endstop: -4.50
position_endstop: -10
position_min: -10
position_max: 120
homing_speed: 12

[stepper_y]
step_pin: PB8
dir_pin: !PB9
enable_pin: !PB4
microsteps: 16
rotation_distance: 8 # 200 * 16 / 400.00
endstop_pin: ^!PC10
#position_endstop: -3.50
position_endstop: -10
position_min: -10
position_max: 120
homing_speed: 12

[stepper_z]
step_pin: PB3
dir_pin: !PD2
enable_pin: !PC12
microsteps: 16
rotation_distance: 8 # 200 * 16 / 400.00
endstop_pin: ^!PA8
position_endstop: -3.25
position_min: -3.25
position_max: 125.5
homing_speed: 9

[extruder]
step_pin: PA4
dir_pin: !PA1
enable_pin: !PA0
microsteps: 16
rotation_distance: 34.7826086957 # 200 * 16 / 92.60 for default e-steps 92.60
heater_pin: !PB10
sensor_type: ATC Semitec 104GT-2 # default
# sensor_type: ATC Semitec 104NT-4-R025H42G # trianglelab
sensor_pin: PC5
min_temp: 0
max_temp: 280
control = pid
pid_kp = 36.524
pid_ki = 2.387
pid_kd = 139.704
max_power: 1.0
pwm_cycle_time: 0.1

nozzle_diameter: 0.4
filament_diameter: 1.75
#pressure_advance: 0.05 # only test


[output_pin LED_R]
pin: mcu:PC7
value:0

[output_pin LED_B]
pin: mcu:PC8
value:0

[output_pin GATE_CTRL]
pin: mcu:PB0
value:1

[output_pin MAIN_POWER]
pin: mcu:PF2
value:1

[output_pin STEPPER_POWER]
pin: mcu:PF1
value:1

[heater_bed]
heater_pin: PA7
sensor_pin: PC4
sensor_type: EPCOS 100K B57560G104F
min_temp: 0
max_temp: 85
control: pid
pid_kp: 65.934
pid_ki: 2.730
pid_kd: 398.078
pwm_cycle_time: 0.1
max_power: 1.0

[bed_mesh]
speed: 80
horizontal_move_z: 1
mesh_min: 10, 10
mesh_max: 115, 115
probe_count: 3, 3
algorithm: lagrange
bicubic_tension: 0.2

[bed_mesh default]
version = 1
points =
 	  -0.500000, -0.100000, 0.200000
 	  -0.400000, -0.100000, 0.200000
 	  -0.400000, -0.100000, 0.300000
x_count = 3
y_count = 3
mesh_x_pps = 2
mesh_y_pps = 2
algo = lagrange
tension = 0.2
min_x = 10.0
max_x = 115.0
min_y = 10.0
max_y = 115.0

[firmware_retraction]
retract_length: 5.0
retract_speed: 60
unretract_extra_length: 0.0
unretract_speed: 60

[gcode_arcs]
#resolution: 1.0

[gcode_macro T0]
gcode:

[gcode_macro M1005]
gcode:

[homing_override]
gcode:
    G28 X
    G28 Y
    G28 Z
    
    G1 Z-2 F1000

#[stepper_z2]
#step_pin: PC2
#dir_pin: !PC1
#enable_pin: !PC3
#microsteps: 16
#rotation_distance: 8 # 200 * 16 / 400.00
#endstop_pin: ^!PC0
#position_endstop: -3.25
#pposition_min: -3.25
#position_max: 125.5
#homing_speed: 9
```
Don't forget to check the sensors on your device before printing, PID calibration (extruder and bed), manual bed height calibration, ... and only then the print itself.

## Can Luban be used?
Most likely not, Luban does rollbacks strangely and I don't even know why, no oddities with rollbacks to gcode from Cura or similar slicers were noticed. But for starters, you can try to print test prints on Luban (on large models such oddities are less noticeable).

## Weird initial positions that limit the useful area
After switching to Cura or other slicers, you can experiment and set the correct initial values. These values ​​were made so that gcode would work on Luban, otherwise you would constantly hit your head on the printer's borders.
