#### Power unit
<img src="../img/power.JPG" width="11%"></img>

A 24V 5A (120W) power supply is used, the reason is unknown, but from the factory this power supply showed 25.2V, in general, an excess of 0.2V is justified, since it allows you to compensate for losses on the wires, but here the excess is as much as 1.2V, which is very bad for the printer's electronics, since all its components (even just fans, heaters) are designed exclusively for 24V. My possible theory is that this excess is most likely done intentionally, since the printer experiences sagging when the heater and table are simultaneously heated by 1.2V.
You can determine the voltage drop simply by the sound of the fans, which are connected directly to 24 V here.

Also, this power supply does not have any cooling capabilities and heats up with prolonged use, but overall it is bearable.

I had an old Mean Well S-150-24 power supply (24V ~6.5A, ~150W) lying around in the bins, not the best choice, but reliable. I set it to 24.2 V and made a double wire to power the printer. As a result, the drop was 0.2 V at the moment of simultaneous heating of the extruder and the table, which suited me quite well.
