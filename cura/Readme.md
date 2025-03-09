#### Cura
In general, you can use Luban, it has good settings for this printer on the old Cura engine, but it has a simpler setup interface and in some places even more thought out than Cura, but very limited in functionality. Or a completely different slicer, but I adapted specifically Cura.

| name | value |
| ---- | ----- |
| X (width) | 125.0 |
| Y (width) | 125.0 |
| Z (height) | 125.0 |
| Build plate shape | Rectangler |
| Origin at center |  |
| Heated bed | + |
| Heated build volume |  |
| G-code flavor | Marlin |
| X min | -20 |
| Y min | -10 |
| X max | 10 |
| Y max | 10 |
| Gantry Height | 125.0 |
| Number of Extruders | 1 |
| Apply Extruder offsets to gcode | + |

Start G-code
```gcode
M1005

T0
M82 ;absolute extrusion mode
;Start GCode begin
M104 S{material_print_temperature_layer_0} ;Set Hotend Temperature
M140 S{material_bed_temperature_layer_0} ;Set Bed Temperature
G28 ;home
M400 ; WAIT END G0/G1
M109 S{material_print_temperature_layer_0} ;Wait for Hotend Temperature
M190 S{material_bed_temperature_layer_0} ;Wait for Bed Temperature
G90 ;absolute positioning
G0 X-10 Y-10 F3000
G0 Z0 F1800
G92 E0
G1 E25 F190 ; Extrusion
G92 E0

G0 X0 Y0 F3000 ;Move to origin
G0 Z1 F1800 ;Move up to avoid scraping against heated bed

;Start GCode end
```

End G-code
```gcode
M140 S0
M107
;End GCode begin
M400 ; WAIT END G0/G1
M104 S0 ;extruder heater off
M140 S0 ;heated bed heater off (if you have it)
G90 ;absolute positioning
G92 E0
G1 E-1 F300 ;retract the filament a bit before lifting the nozzle, to release some of the pressure
G1 Z125 E-1 F3000 ;move Z up a bit and retract filament even more
G1 X0 F3000 ;move X to min endstops, so the head is out of the way
G1 Y125 F3000 ;so the head is out of the way and Plate is moved forward
;End GCode end
M82 ;absolute extrusion mode
M104 S0
;End of Gcode
```

| name | value |
| ---- | ----- |
| Nozzle size | 0.4 |
| Compatible material diametr | 1.75 |
| Nozzle offset X | 0.0 |
| Nozzle offset Y | 0.0 |
| Cooling Fan Number | 0.0 |
| Extruder Start G-code duration | 0.0 |
| Extruder End G-code duration | 0.0 |

Next, I recommend installing `Cura-MaterialSettingsPlugin` or a similar plugin to distribute settings between the filament and the printer profile.

In the files I will attach a print profile adapted for this printer (but I have a "volcano") and an example of settings for one of the types of plastic.

<b>The section is not finished yet.</b>
