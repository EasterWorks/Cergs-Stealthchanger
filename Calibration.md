# Dock Parking Calibration, Testing, and Safe Zone Specification

For setting up your dock positions:
- First, attach the tool you want to calibrate to the shuttle by hand, then home all axiis and QGL.
- Once finished, manually jog the toolhead to the point where it's sitting where you would like it to dock. Do this slowly and carefully!
- Finally, you're going to lower the Z axis until the OptoTAP untriggers, then move it up 1mm.
- Document all axis positions and move the toolhead away.
- Update the fields "params_park_x", "params_park_y", and "params_park_z" in your toolhead's configuration file under the section "[tool tool#]".
- Save config and firmware restart (save config will do that automatically).
- Once restart is complete, re-home and QGL.
- Now we'll _test_ that position. Run the following command: SET_TOOL_PARAMETER PARAMETER='params_path_speed' VALUE=300
- Then run the next command. NOTE: This will attempt to dock and undock your toolhead based on the values you input above for the park params. Keep your finger on the E-stop! TEST_TOOL_DOCKING RESTORE_AXIS=XYZ
- Once finished, run this command to reset path speed. RESET_TOOL_PARAMETER PARAMETER='params_path_speed'

It is normal for the nozzle to impact the printed wiper stand on the dock, that's actually what it's there for.

If during the docking test, you had to E-stop because the tool was going to smash into the dock, redo your positioning.
If during the docking test, your toolhead docked properly but you heard some surface contact, you might need to adjust X or Z just slightly. We're talking values of like 0.1mm-0.5mm, nothing huge. 
If during the docking test, you are positive your position is good but you still heard some surface contact, your dock may have a slight warp. This isn't the end of the world but may impact reliability. Make sure the dock sits as flat as possible!

Now we're going to look at the _Safe Zone_. This is a parameter you can edit in toolchanger.cfg to essentially tell the printer "hey, when you start a docking procedure, get NO CLOSER than x value."
- While homed and QGL'd on any toolhead, jog your toolhead to the point where the tool's dock is about halfway up the cowl, and the cowl is NEARLY touching (give it about 1mm gap). Generally you will probably be at around 50-80mm on the Y axis.
- Back the toolhead off 10mm.
- Now add 20mm.
- Your tool will probably be at around 80mm-100mm on the Y axis now. This is going to be both your params_safe_y and params_close_y. While configuring this, you should be aware that you won't be able to dock your tools if a print gets higher than about 10mm (for safety) lower than your docking height. For me, that's about 180mm on Z. These are the sacrifices we make! Frame extensions are an option with longer Z belts if desired.

Why the Safe Zone? Well, if you don't specify this, your toolhead may get too close to the dock when switching tools and end up ramming the bottom of the cowl into the lip of the dock as it rounds out the movement path. You can adjust these values as you see fit, but be sure to do it in small increments to avoid any unfortunate accidents!


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


# Nozzle Offsets - X/Y Offset

These offsets will entirely be done as gcode offset, particularly gcode_x_offset and gcode_y_offset values under [tool tool#]. My typical approach is to slice a 20mmx4mm cube,
starting with T0, and then insert a filament change to T1 once it reaches 2mm tall. When finished, you should mark which side of the cube was facing you when you pulled it off
of the bed to maintain the orientation.

When finished, the two sections will most likely be offset by a small amount. I use a digital depth gauge to determine just how offset these are and note that for both axiis.
Once noted, enter the information for your gcode_x_offset and gcode_y_offset values as mentioned above. Remember; positive values move TOWARD the axis' travel limit.
