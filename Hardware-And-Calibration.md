# THIS IS A WIP

Complete the following sections in order to replicate my process.

# Table of Contents
1) Print Selection
2) Heat-Treating Process for Backplates
3) Assembly Notes
5) Dock Parking Calibration, Testing, and Safe Zone Specification
6) Nozzle Offsets - Probe-to-Nozzle and Gcode
7) Nozzle Offsets - X/Y Offset

# 1) Print Selection

As this repo is targeted toward people wanting to use the Stealthburner toolhead, we'll first talk about that.


### ECAS fitting for Clockwork 2

First up: I HIGHLY advise printing a CW2 housing with allowance for an ECAS fitting. I used this one by AlexanderT_Moss on Printables:
- https://www.printables.com/model/433797-clockwork-2-ecas-fitting-for-ercf

The reason for using an ECAS fitting is because the reverse bowden tubes will be flexing around a bit more than usual when constrained to the umbilical. Make sure to print the modified latch as well since it needs to be able to clear the ECAS fitting.


### Backplates and Shuttles
Next you'll need both the Stealthburner backplates and a shuttle. Here are the backplates from the DraftShift Design repo:
- https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/StealthBurner.stl

As for the shuttle, I have modified DSD's design to allow you to loop the belts back into and out of the housing to prevent cutting the belts too short. It can be found in this repo:
https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/STLs/MGN12%20Shuttle.stl

YOU WILL NOTICE the "fin" on top of the shuttle is too long for the backplate to sit properly. Leave it this way until the shuttle is installed and you have a backplate outfitted with pins. CAREFULLY trim the fin on top of the shuttle until whichever backplate is going on your T0 sits as flat to the shuttle as it's going to (force it if needed - poor fitup will be adjusted later). I found the default height of the fin to be too short.

It is also worth noting that this will move your Y axis about 5mm toward the "front" of the printer. You may need to adjust how your bed is positioned to accomodate.

You need one backplate per toolhead and only one shuttle.


### PG7 gland mount for Stealthburner
Last part for the toolhead itself - you'll want a PG7 gland mount on the Stealthburners to replace the original X axis dragchain mount. I use this one by CstmCreations_174350 on Printables:
- https://www.printables.com/model/463220-voron-cw2-stealthburner-ebb-sb2240-pg7-umbilical-m


### Umbilical clips
Next up, your umbilical clips. These are largely up to you - I designed ones that would slip over the Nitehawk USB cable, allow a channel for the reverse bowden tube, and use two small zipties to create just enough tension to grip on to the cable and bowden without crushing them. It also has holes to allow for 1mm piano wire as the stiffening component of the umbilical. You can find them here:
- https://www.printables.com/model/1127631-ldo-nitehawk-umbilical-clips-for-stealthchanger-ta

I use four per umbilical.


### Bird's Nest fannypack and Exhaust Plate
Now let's look at making a home for the Bird's Nest and a new exhaust plate to allow the umbilicals into the print chamber. For housing the Bird's Nest, print the fanny pack by Isiks Tech:
- https://github.com/xbst/Birds-Nest/tree/master/Mounts/V2

I used 3M double-sided tape to stick it to the back panel a few inches under the exhaust plate.

Now for the exhaust plate itself - I designed one that would allow you to non-destrucitvely insert and retain the umbilicals. You can find it here on Printables:
- https://www.printables.com/model/1127639-ldo-nitehawk-umbilical-exhaust-plate-for-voron-24


### Docks
Finally, we need to print our docks. I used low-profile docks that secure to a crossbeam rather than to the top of the printer's frame using parts from three sourcess. The first source, cjackson234 on Printables, provides "base minimal.stl":
- https://www.printables.com/model/994635-stealthchanger-stealthburner-minimal-docks-aka-hap

The second source, arthur belanger on Printables, replaces the multi-part front of the dock with a single-part iteration:
- https://www.printables.com/model/1063297-one-piece-docks-remix-of-crabby-docks/files

The third source is back with DraftShift for their modular docks, particularly the blocker. I used the spring steel body approach to use hobby blades with a molded silicone pad; if you prefer to use the cup style, you can go with that as well:
- https://github.com/DraftShift/ModularDock/tree/main/STLs/Blockers


# 2) Heat-Treating Process for Backplates

I have seen this documented both in the Stealthchanger Discord server as well as in the Stealthchanger repo wiki. This is intended to improve the fitup between your backplates and the shuttle. The shuttle should already be installed on the gantry at this point. Here is the process I did:

- Install pins in the backplates.
- Place ONE backplate on the bed on its flat face, set bed temperature to 110c, and close the door.
- Wait around one hour. To check if it's been long enough, touch the metal pins - they should be hot.
- Turn off the bed heater and open the enclosure door.
- While still hot, install the backplate on the shuttle firmly. If it tries to lift itself, secure it only as much as is needed for it to seat properly with a ziptie.
- Allow this to sit for 4-5 hours or until the backplate is entirely cool to the touch.
- Once cooled, remove/insert the backplate into the shuttle a few times to see how fitup feels. If it's still bad, repeat. If it's still bad after repeating, you may need to reprint the backplate or shuttle.
- Repeat for each backplate.

This sounds a bit annoying, and it is - but this is how you get really accurate results with the OptoTAP in my experience.


# 3) Assembly Notes
- Ensure the X-axis dragchain is eliminated. Y-axis dragchain needs to remain in place for the X/Y endstop cable.
- Ensure the Z axis dragchain allows the Z axis to move cleanly through its entire travel to the top. If it's getting caught on the guide stop mounted on the rear of the gantry, move the guide stop.
- When installing the dock crossbar, try to get it as even and square to the frame as possible. You won't get it perfectly but we can adjust for sub-mm variances in the firmware later.
- If you had a nozzle brush in the back-right corner of the printer that you used before, it will probably be offset with the modified shuttle. The bed needs to move forward to accomodate for this - or you need to move the brush to the front of the bed and modify your CLEAN_NOZZLE gcode macro.


# 4) Dock Parking Calibration, Testing, and Safe Zone Specification

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


# 5) Nozzle Offsets - Probe-to-Nozzle and Gcode

When T0 does its initial homing routine and bed mesh at the start of a print, its nozzle offset is applied to the gantry. Meaning if the T0 offset is, say, -1.23, that will 
be the offset applied for the gantry as it is in motion during the print.

If T1 has a substantially different nozzle offset, say -0.23, this will result in the nozzle being shoved 1mm too far into the bed when T1 is switched to and begins printing. 
This can lead to stacking tolerance problems when printing parts with embedded color changes (for example: a black circle in the side of a square).

Because of this, you need to account for that difference in the gcode offset. In this specific example, your gcode Z offset would be 1.

Note: Gcode offsets and nozzle-to-probe offsets are read differently. A negative value for a nozzle-to-probe offset will increase the distance between the nozzle and the bed; 
a positive gcode offset will move the tool "further" on its given axis (toward its movement limit).

In your toolhead config, set the real nozzle offset (the result you get when running PROBE_CALIBRATE) as the z_offset value under [tool_probe tool#]. When you have determined
the needed gcode offset per the above information, set that as the gcode_z_offset value under [tool tool#].


# 6) Nozzle Offsets - X/Y Offset

These offsets will entirely be done as gcode offset, particularly gcode_x_offset and gcode_y_offset values under [tool tool#]. My typical approach is to slice a 20mmx4mm cube,
starting with T0, and then insert a filament change to T1 once it reaches 2mm tall. When finished, you should mark which side of the cube was facing you when you pulled it off
of the bed to maintain the orientation.

When finished, the two sections will most likely be offset by a small amount. I use a digital depth gauge to determine just how offset these are and note that for both axiis.
Once noted, enter the information for your gcode_x_offset and gcode_y_offset values as mentioned above. Remember; positive values move TOWARD the axis' travel limit.
