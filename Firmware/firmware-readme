TBD - this document is to describe needed edits to printer.cfg and describe what other included CFG files do. also to list plugins needed like multi-fan, toolchanger, etc

# Nozzle Offsets - probe-to-nozzle and gcode

When T0 does its initial homing routine and bed mesh at the start of a print, its nozzle offset is applied to the gantry. Meaning if the T0 offset is, say, -1.23, that will 
be the offset applied for the gantry as it is in motion during the print.

If T1 has a substantially different nozzle offset, say -0.23, this will result in the nozzle being shoved 1mm too far into the bed when T1 is switched to and begins printing. 
This can lead to stacking tolerance problems when printing parts with embedded color changes (for example: a black circle in the side of a square).

Because of this, you need to account for that difference in the gcode offset. In this specific example, your gcode Z offset would be 1.

Note: Gcode offsets and nozzle-to-probe offsets are read differently. A negative value for a nozzle-to-probe offset will increase the distance between the nozzle and the bed; 
a positive gcode offset will move the tool "further" on its given axis (toward its movement limit).

In your toolhead config, set the real nozzle offset (the result you get when running PROBE_CALIBRATE) as the z_offset value under [tool_probe tool#]. When you have determined
the needed gcode offset per the above information, set that as the gcode_z_offset value under [tool tool#].
