## HOW DO I STEALTHCHANGER?
Complete the following sections in order to replicate my process.

# Table of Contents
- Add-Ons and Updates for Klipper
- Toolhead Print Selection
- Heat-Treating Process for Backplates
- Assembly Notes
- Special Notes on OptoTAP
- Nozzle Offsets - Probe-to-Nozzle and Gcode
- PID, Input Shaper, Extruder Rotation Distance, and Pressure Advance Tuning
- Dock Parking Calibration, Testing, and Safe Zone Specification
- Purge, Preheat, and Other Relevant Orca Slicer Settings
- Machine Start and Machine End Gcode
- Nozzle Offsets - X/Y Offset
- Final Considerations


# Add-Ons and Updates for Klipper

You will need to install the following Klipper add-ons:
- Klipper-Toolchanger: https://github.com/viesturz/klipper-toolchanger/

This includes everything Klipper will need for the actual toolchanging routines, running multiple part fans, managing multiple probes, incorporates some path rounding logic for non-print moves (docking/undocking, ect) and some calibration utilities.

Make sure Klipper is up-to-date before beginning, and if necessary, update Klipper on your Bird's Nest and your Nitehawk toolhead boards. Proper functionality apparently relies upon features updated/added to Klipper around July of 2024, so you need a version that's newer than that. When you buy the Bird's Nest from Isik and the Nitehawks from LDO, they _should_ already be on the latest release of Klipper when you receive them, but it's good to double-check.


# Toolhead Print Selection

As this repo is targeted toward people wanting to use the Stealthburner toolhead, we'll first talk about that.


### ECAS fitting for Clockwork 2

First up: I HIGHLY advise printing a CW2 housing with allowance for an ECAS fitting. I used this one by AlexanderT_Moss on Printables:
- https://www.printables.com/model/433797-clockwork-2-ecas-fitting-for-ercf

The reason for using an ECAS fitting is because the reverse bowden tubes will be flexing around a bit more than usual when constrained to the umbilical, so it will benefit from stronger retention. Make sure to print the modified latch as well since it needs to be able to clear the ECAS fitting.


### Backplates and Shuttles
Next you'll need both the Stealthburner backplates and a shuttle. Here are the backplates from the DraftShift Design repo:
- https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/StealthBurner.stl

As for the shuttle, I have modified DSD's design to allow you to loop the belts back into and out of the housing to prevent cutting the belts too short. It can be found in this repo:
- https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/STLs/MGN12%20Shuttle.stl

YOU WILL NOTICE the "fin" on top of the shuttle is too long for the backplate to sit properly. Leave it this way until the shuttle is installed and you have a backplate outfitted with pins. CAREFULLY trim the fin on top of the shuttle until whichever backplate is going on your T0 sits as flat to the shuttle as it's going to (force it if needed - poor fitup will be adjusted later). I found the default height of the fin to be too short.

It is also worth noting that this will move your Y axis about 5mm toward the "front" of the printer. You may need to adjust how your bed is positioned to accomodate.

You need one backplate per toolhead and only one shuttle.

Additionally, you will need to print the X axis prod included in this repo:
- https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/STLs/x-axis-prod.stl

The X axis prod is secured to the bottom of the shuttle using two M3x8 SHCS. Its job is to touch the X axis endstop when it reaches its minimum distance. This isn't accounted for in the original shuttle design as the intention is to use sensorless homing on X/Y, but we aren't doing that.


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


# Heat-Treating Process for Backplates

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


# Assembly Notes
- Ensure the X-axis dragchain is eliminated. Y-axis dragchain needs to remain in place for the X/Y endstop cable.
- Ensure the Z axis dragchain allows the Z axis to move cleanly through its entire travel to the top. If it's getting caught on the guide stop mounted on the rear of the gantry, move the guide stop.
- When installing the dock crossbar, try to get it as even and square to the frame as possible. You won't get it perfectly but we can adjust for sub-mm variances in the firmware later.
- If you had a nozzle brush in the back-right corner of the printer that you used before, it will probably be offset with the modified shuttle. The bed needs to move forward to accomodate for this - or you need to move the brush to the front of the bed and modify your CLEAN_NOZZLE gcode macro.
- If you have very old X/Y belts, this is a great opportunity to install new ones.
- Also a great opportunity to install Beefy Front Idlers (BFI) if you haven't already: https://github.com/clee/VoronBFI


# Special Notes on OptoTAP
When you get your toolheads put together, one of the first things you should do is repeatedly run a probe using PROBE_CALIBRATE to help smooth out any rough spots on the contact points. In conjunction with the previously-mentioned heat-treating method, this will help greatly improve your OptoTAP readings.

- Attach the toolhead you want to break in to the shuttle, home all axiis, and QGL.
- Move the toolhead to the center of your bed.
- Run the command PROBE_CALIBRATE SAMPLES=n where n = the number of Z axis probes you'd like to do. As you've already homed on Z successfully by this point, we know the probe is working, so we now want to run it up to as many as 500 probing samples to wear down contact surfaces into smooth operation. For example, PROBE_CALIBRATE SAMPLES=500 will probe the Z axis 500 times.
- Upon completion, run PROBE_CALIBRATE SAMPLES=25 and review the variance results that are reported in the console. You want the variance to be at an absolute maximum 0.025mm (the biggest variance recommended for Klipper), but using the methods described here, I have achieved a variance as low as 0.00028mm. When you achieve good results, edit your QGL macro in printer.cfg to the recommended 0.00750mm tolerance.


# Nozzle Offsets - Probe-to-Nozzle and Gcode

Follow the typical Klipper Z offset calibration procedure on T0 EXCEPT for saving config after the calibration - simply note the offset as it is reported in the console:
https://www.klipper3d.org/Probe_Calibrate.html#calibrating-probe-z-offset

When T0 does its initial homing routine and bed mesh at the start of a print, its nozzle offset is applied to the gantry. Meaning if the T0 offset is, say, -1.23mm, that will 
be the offset applied for the gantry as it is in motion during the print.

If T1 has a substantially different nozzle offset, say -0.23mm, this will result in the nozzle being shoved 1mm too far into the bed when T1 is switched to and begins printing. 
This can lead to stacking tolerance problems when printing parts with embedded color changes (for example: a black circle on the side of a cube).

Because of this, you need to account for that difference in the gcode offset. In this specific example, your gcode Z offset would be 1.

Note: Gcode offsets in positive values move the toolhead toward the "max" position of that axis to compensate. Negative offsets go toward the "min" position.

In your toolhead config, set the real nozzle offset (the result you get in the console after finishing the PROBE_CALIBRATE procedure) as the z_offset value under [tool_probe tool#]. Ideally, do a test print with that value on that tool to verify that your first layer is good. When you have determined the needed gcode offset per the above information, set that as the gcode_z_offset value under [tool tool#].

### Note: When you do your nozzle offset calibration, before saving config and restarting firmware, check the bottom of printer.cfg to see if it's going to try to insert new nozzle offset parameters. DELETE THIS before saving config and restarting firmware. These params need to be updated per toolhead, NOT in printer.cfg!


# PID, Input Shaper, Extruder Rotation Distance, and Pressure Advance Tuning
PID, Input Shaper, extruder rotation distance, and pressure advance need to be done _per toolhead_. Simply attach whatever tool you wish to calibrate to the shuttle, home and QGL, and then run the standard tests as outline in the Klipper wiki:

 - PID tuning: https://www.klipper3d.org/Config_checks.html#calibrate-pid-settings
 - Input shaper: https://www.klipper3d.org/Measuring_Resonances.html#measuring-the-resonances
 - Extruder rotation distance (courtesy of Ellis' print tuning guide): https://ellis3dp.com/Print-Tuning-Guide/articles/extruder_calibration.html
 - Pressure advance tuning (again, courtesy of Ellis): https://ellis3dp.com/Print-Tuning-Guide/articles/index_pressure_advance.html

The only difference here is that instead of inputting these values to printer.cfg, you're going to input them in the relevant toolhead's cfg file. For example, if you have your results for input shaper when measuring on T0, you need to input those figures into t0.cfg.


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


# Purge, Preheat, and Other Relevant Orca Slicer Settings

So first, you actually need to enable multi-material printing in Orca Slicer. Open your printer settings and switch to the "Multimaterial" tab. Under "Single extruder multi-material setup", ensure "Single Extruder Multi Material" is unticked, then enter "2" (or whatever number of toolheads you have) for "Extruders". At the very bottom of this page, you can enter a value in seconds for "Tool Change Time" - this is how long it takes your printer to depart from the print, switch tools, and return to the print. You should time and update this after dialling in your idle and preheat temperatures to ensure you get useful print time estimates.

After specifying that you have two extruders, a new tab called "Extruder 2" will appear alongside Extruder 1. You can enter retraction values and all the other fun per-toolhead settings you wish here, but leave the offset positions for the toolhead .cfg file.

I highly advise still using a purge tower despite no real need to flush the nozzle. Using a purge tower accomplishes two things:
- It allows the filament in the active tool to fully un-retract before reaching the print. If not accounted for and your retraction settings aren't perfect, your first layer after the tool change will be ratty.
- It catches nearly all of the ooze and whisps that accumulate on the nozzle in the brief travel from undocking to reaching the print.

You may omit the purge tower if your retraction settings are perfect and your toolchanges are super rapid, but a purge tower makes both of those much less of an issue and is still only fractionally wasteful compared to systems like the AMS. As of now, purge tower ("prime tower") settings in Orca Slicer are located in the global Multimaterial settings tab.

In addition, you will want to implement preheating and idle temp settings. Preheating does what you'd think; it fires off gcode at an estimated time to the next toolhead to be used to get it up to printing temperature, making the toolchange occur much faster. Preheating settings can also be found in the global Multimaterial settings tab in Orca Slicer. Leave the temperature variation delta at 0c because we're going to use per-material settings for that later. What you should then do is get your hotend up to 150-160c, where filament will be hot but not oozing yet, and then time how long it takes for the hotend to reach the printing temperature of the material you want to use. Add 10 seconds to this time and enter that for the "preheat time". Note that when you first start a print, the inactive toolhead won't be preheated to the idle temperature, so your first tool change will always be a little longer - you don't need to accomodate for that in the slicer settings, that's just how it is, so be aware.

Next we need to actually input the idle temperature we want to use. Next to the filament you have selected for the toolhead under "Filament", click the edit button. Under "Basic Information", near the bottom of that section, you'll see "Idle Temperature". Set that to the idle temperature you wish (I use 160C for Elegoo PLA+, for example). 

Finally, and this is more of a quality of life note - your print should always start on T0 so the offsets on your other toolheads apply correctly. Orca Slicer will start with whatever toolhead has the most volume on the first layer. So if you're printing something that starts mostly with the material you have loaded in T1, you can add a primitive cube with only one layer of height and just enough surface area to print with the material in T0 to trick Orca Slicer into thinking T0 needs to be the start nozzle. I'm still looking for a better way around this, but it's better than a print failing.


# Machine Start and Machine End Gcode

I have supplied the needed start and end print gcodes in the Gcode folder for Orca Slicer, as Orca Slicer currently has the friendliest functionality and most up to date features in my opinion:
- Machine start: https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Gcode/OrcaSlicer%20Start%20Gcode
- Machine end: https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Gcode/Orca%20Slicer%20end%20gcode

These will work with the other example CFG's I've provided here. The only special consideration is that, in order to differentiate toolchange starts/ends from non-toolchanger starts/ends, I have renamed the toolchanger print start and print end gcodes both in toolchanger.cfg and in the print start/end gcodes that need to be input to Orca Slicer. 

Otherwise, make sure the Change Filament Gcode field has the following comment:
- ;Leave blank

This will prevent Orca Slicer from inserting its default filament change gcode. No other gcode settings are needed in Orca Slicer other than our start and end print gcode.

If you are utilizing an existing Stealthburner LED configurations, make sure to insert the right gcode macros where needed in TOOLCHANGER_PRINT_START and TOOLCHANGER_PRINT_END.


# Nozzle Offsets - X/Y Offset

These offsets will entirely be done as gcode offset, particularly gcode_x_offset and gcode_y_offset values under [tool tool#]. My typical approach is to slice a 20mmx4mm cube,
starting with T0, and then insert a filament change to T1 once it reaches 2mm tall. When finished, you should mark which side of the cube was facing you when you pulled it off
of the bed to maintain the orientation.

When finished, the two sections will most likely be offset by a small amount. I use a digital depth gauge to determine just how offset these are and note that for both axiis.
Once noted, enter the information for your gcode_x_offset and gcode_y_offset values as mentioned above. Remember; positive values move TOWARD the axis' travel limit.


# Final Considerations

Once you have achieved reliable toolchanging capabilities, you should get your extrusion multiplier dialled in and revise PID, Input Shaper, PA, retraction, etc. settings if needed. Otherwise, congratulations - you _should_ have a working Stealthchanger now.

Make sure to go to the Stealthchanger Discord and request a serial! https://discord.gg/kXuEYBsa



