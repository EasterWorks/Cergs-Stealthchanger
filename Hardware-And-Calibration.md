This page is a WIP kinda but should be full of hopefully helpful information.

# First: USE CAUTION!

![image](https://github.com/user-attachments/assets/2537ca83-9b23-44e5-9c15-589599770e9b)


### I am not responsible for any silly little mistakes you make during the following process. You need to read this document, think about the parts you don't understand, and do research before starting this project. Hot robots can poke you, prod you, burn you, cut you, scrape you, break their own parts, break YOUR own parts, electocute you, and even burn your house down if you aren't careful. Tinker responsibly!

# HOW DO I STEALTHCHANGER?
Complete the following sections in order to replicate my process.

# Table of Contents
- [Add-Ons and Updates for Klipper](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#add-ons-and-updates-for-klipper)
- [Bill of Materials](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#bill-of-materials)
- [Printed Part Selection](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#printed-part-selection)
- [Preparing, Assembling, and Installing the Shuttle](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#preparing-printing-and-installing-the-shuttle)
- [Preparing, Assembling, and Installing the Backplates](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#preparing-printing-and-installing-the-backplates)
- [Heat-Treating Process for Backplates](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#heat-treating-process-for-backplates)
- [The Dock Crossbar and Bulking Out the Front of the Printer (not in the BOM!)](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#the-dock-crossbar-and-bulking-out-the-front-of-the-printer-not-in-the-bom)
- [Other Assembly Notes](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#other-assembly-notes)
- [Special Notes on OptoTAP](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#special-notes-on-optotap)
- [Nozzle Offsets - Probe-to-Nozzle and Gcode](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#nozzle-offsets-probe-to-nozzle-and-gcode) 
- [PID, Input Shaper, Extruder Rotation Distance, and Pressure Advance Tuning](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#pid-input-shaper-extruder-rotation-distance-and-pressure-advance-tuning)
- [Dock Parking Calibration, Testing, and Safe Zone Specification](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#dock-parking-calibration-testing-and-safe-zone-specification)
- [Purge, Preheat, and Other Relevant OrcaSlicer Settings](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#purge-preheat-and-other-relevant-orcaslicer-settings) 
- [Machine Start and Machine End Gcode](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#machine-start-and-machine-end-gcode) 
- [Nozzle Offsets - X/Y Offset](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#nozzle-offsets-x-y-offset) 
- [Final Considerations](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md#final-considerations) 


# Add-Ons and Updates for Klipper

**First: BACK UP YOUR CURRENT CFG'S!!!!!**

You will need to install the following Klipper add-ons:
- Klipper-Toolchanger: https://github.com/viesturz/klipper-toolchanger/

This includes everything Klipper will need for the actual toolchanging routines, running multiple part fans, managing multiple probes, incorporates some path rounding logic for non-print moves (docking/undocking, ect) and some calibration utilities. You will need to edit some of these files: Check in the "Firmware" folder in this repo for comments pointing out where.

Make sure Klipper is up-to-date before beginning, and if necessary, update Klipper on your Bird's Nest and your Nitehawk toolhead boards. Proper functionality apparently relies upon features updated/added to Klipper around July of 2024, so you need a version that's newer than that. When you buy the Bird's Nest from Isik and the Nitehawks from LDO, they _should_ already be on the latest release of Klipper when you receive them, but it's good to double-check.


# Bill of Materials

Remember that this repo is centered around the concept of implementing the Stealthchanger with two Stealthburner+Revo toolheads using LDO Nitehawk-SB toolhead boards and an Isiks Tech Birds' Nest for toolhead networking. If you are using CAN or different toolhead designs, this won't be entirely accurate.

### Stealthburner:
- [LDO Nitehawk-SB](https://west3d.com/products/nitehawk-stealthburner-toolboard-sb-pcb-by-ldo-motors) (one per toolhead) 
- [E3D Revo hotend](https://www.filastruder.com/products/e3d-revo-voron?variant=39567818981447) (one per toolhead)
- All other commercial parts needed for the Stealthburner can be found [here](https://vorondesign.com/voron_stealthburner), with the exception of the Cables and Optional - ADXL345 Sensor sections.

The main difference between the standard Stealthburner and the Stealthchanger adaptation is that instead of putting heat sets and screws into the original Voron 2.4 shuttle, you'll instead be putting those parts into the backplates.

### Shuttle
- 6x3mm N52 neodymium magnet (x3)
- 4x6x6mm oilless sleeve bushing (x3)
- M3x8 SHCS (x4)
- M3x5x4mm heat-set inserts (x2)

### Backplate (each):
- OptoTAP optical sensor (x1)
- 6x3mm N52 neodymium magnet (x1)
- M3x6 FHCS (x2)
- M3x6 BHCS (x2, used to retain the OptoTAPs - may also use M3x8, just screw them in slowly)
- M3x8 SHCS (2x)
- M4x12mm round-head dowel pins (x3)
- M3x5x4mm heat-set inserts (4x)

### Dock (each):
- M5x8 BHCS (2x)
- M5 T-nut/hammer nut (2x)
- M3x8 SHCS (x2)
- M3x8 BHCS (x4)
- M3x30 SHCS (4x)
- M3x60 SHCS (x2)
- M3 heat-set inserts (x10)

If you would like to print any of the wiper options, ensure you instead print the "Stubby" spring steel body and pay attention to the changes therein.


# Printed Part Selection

As this repo is targeted toward people wanting to use the Stealthburner toolhead, we'll first talk about that.


### ECAS fitting for Clockwork 2
![image](https://github.com/user-attachments/assets/5e780455-8488-4c18-b081-8a3cac1e9d99)

First up: I HIGHLY advise printing a CW2 housing with allowance for an ECAS fitting. I used this one by AlexanderT_Moss on Printables:
- https://www.printables.com/model/433797-clockwork-2-ecas-fitting-for-ercf

The reason for using an ECAS fitting is because the reverse bowden tubes will be flexing around a bit more than usual when constrained to the umbilical, so it will benefit from stronger retention. Make sure to print the modified latch as well since it needs to be able to clear the ECAS fitting.


### Backplates and Shuttles
![image](https://github.com/user-attachments/assets/18141c80-02cf-48d9-a749-e7e6a0d2e9f5)

Next you'll need both the Stealthburner backplates and a shuttle. Here are the backplates from the DraftShift Design repo:
- https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/StealthBurner.stl

As for the shuttle, I have modified DSD's design to allow you to loop the belts back into and out of the housing to prevent cutting the belts too short. It can be found in this repo:
- https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/STLs/MGN12%20Shuttle.stl

Of course you may also use the DSD version of the shuttle without those channels to minimize Y axis travel loss, though routing the belts will be more difficult **and my X axis endstop prod will NOT work with their design**:
- https://github.com/DraftShift/StealthChanger/blob/main/STLs/Shuttle%20MGN12%20(With%20belt%20grooves).stl

DSD also provides a version of the shuttle without the grooves if you prefer that.

YOU WILL NOTICE the "fin" on top of my shuttle redesign is too long for the backplate to sit properly with both parts straight off of the printer. Leave it this way until the shuttle is installed and you have a backplate outfitted with pins. CAREFULLY trim the fin on top of the shuttle until whichever backplate is going on your T0 sits as flat to the shuttle as it's going to (force it if needed - poor fitup will be adjusted later). I found the default height of the fin to be too short.

It is also worth noting that this will move your Y axis about 5mm toward the "front" of the printer. You may need to adjust how your bed is positioned to accomodate.

You also need one backplate per toolhead and only one shuttle. Those can be found on DSD's repo. The link below is for the Stealthburner, but they support many toolheads and the list is growing:
- https://github.com/DraftShift/StealthChanger/blob/main/STLs/Backplates/StealthBurner.stl

Additionally, since we're going to use the X axis endstop on the X/Y intersection joint, you will need to print the X axis prod included in this repo:
- https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/STLs/x-axis-prod.stl

The X axis prod is secured to the bottom of the shuttle using two M3x8 SHCS that screw into two M3 hot-sets you'll need to embed into either shuttle design in the provided holes. Its job is to touch the X axis endstop when it reaches its maximum travel. This isn't accounted for in either of the presented shuttle designs as the original intention was to use sensorless homing on X/Y.


### PG7 gland mount for Stealthburner
![image](https://github.com/user-attachments/assets/3bd0a084-98f6-4e07-a211-87b29cfe814f)

Last part for the toolhead itself - you'll want a PG7 gland mount on the Stealthburners to replace the original X axis dragchain mount. I use this one by CstmCreations_174350 on Printables:
- https://www.printables.com/model/463220-voron-cw2-stealthburner-ebb-sb2240-pg7-umbilical-m


### Umbilical clips
![image](https://github.com/user-attachments/assets/2dbc249b-14ea-437f-8b84-088906a17283)

Next up, your umbilical clips. These are largely up to you - I designed ones that would slip over the Nitehawk USB cable, allow a channel for the reverse bowden tube, and use two small zipties to create just enough tension to grip on to the cable and bowden without crushing them. It also has holes to allow for 1mm piano wire as the stiffening component of the umbilical. You can find them here:
- https://www.printables.com/model/1127631-ldo-nitehawk-umbilical-clips-for-stealthchanger-ta

I use four per umbilical.


### Bird's Nest fannypack
![image](https://github.com/user-attachments/assets/c48290af-dd03-4322-92ac-a3fa0aaf14c0)

Now let's look at making a home for the Bird's Nest and a new exhaust plate to allow the umbilicals into the print chamber. For housing the Bird's Nest, print the fanny pack by Isiks Tech (or another enclosure if you prefer - the fanny pack isn't very space efficient):
- https://github.com/xbst/Birds-Nest/tree/master/Mounts/V2

I used 3M double-sided tape to stick it to the back panel a few inches under the exhaust plate.

### Exhaust Plate / Umbilical Guide
![image](https://github.com/user-attachments/assets/ddef0ad0-37c9-4702-b937-171afb3ba4eb)

Now for the exhaust plate itself - I designed one that would allow you to non-destrucitvely insert and retain the umbilicals. You can find it here on Printables:
- https://www.printables.com/model/1127639-ldo-nitehawk-umbilical-exhaust-plate-for-voron-24


### Docks
Finally, we need to print our docks. I used low-profile docks that secure to a crossbeam rather than to the top of the printer's frame using parts from three sourcess. The first source, cjackson234 on Printables, provides "base minimal.stl":
- https://www.printables.com/model/994635-stealthchanger-stealthburner-minimal-docks-aka-hap

The second source, arthur belanger on Printables, replaces the multi-part front of the dock with a single-part iteration:
- https://www.printables.com/model/1063297-one-piece-docks-remix-of-crabby-docks/files

The third source is back with DraftShift for their modular docks, particularly the blocker. I used the spring steel body approach to use hobby blades with a molded silicone pad; if you prefer to use the cup style, you can go with that as well:
- https://github.com/DraftShift/ModularDock/tree/main/STLs/Blockers

Finally, back in DSD's repo, you'll need a Stealthburner dock backplate:
- https://github.com/DraftShift/ModularDock/blob/main/STLs/Stealthburner/Back.stl


# Preparing, Assembling, and Installing the Shuttle
All Stealthchanger shuttle designs need to have bushings installed in the corresponding hex-slot holes. Some people glue them in, but the intention is for them to be a near-pressfit. You can find details on the specific bushings in the Bill of Materials section above.

There is a hole for an M3 heat set insert that can go into the bottom center of the shuttle along where the MGN rail shuttle connects - I have yet to see anyone use this hole for anything, so skip adding a heat set there

Below the above-mentioned hole, there are two more holes for M3 heat set inserts. Those are to connect the X axis endstop prod in my design, but are absent in the original design. To use the prod, you will also need to print my redesigned shuttle, then secure it to the shuttle with two M3x8 SHCS.

Next, you need 3 6x2mm neodymium magnets. The ones you want to get are N52 with a working temperature rating of 80c. N52 magnets are very strong variants of neodymium and 80c will put you far and beyond the temperature your magnets should ever hit. If you just buy a generic unlabelled pack of neodymium magnets, you will probably get N42s - not as strong, and usually max working temp rating of 60c. These can still work, but I like the strength and safety margins of the N52's, and it's worth a few more dollars for a lifetime supply.

In my redesign of the shuttle, I extended the "fin" at the top so you can trim it only as low as is needed for the backplate to seat fully using some flush cutters. I suggest taking off 1mm of material from that fin at a time until you get the backplate almost fully seated to the shuttle, then file or sand down the rest until your backplate is fully there. The original design has this fin already designed to match up "perfectly" with the backplates - however, in my experience, stacking tolerances lead to that fin sometimes being just slightly too short. 

Finally, you'll notice that the bottom side of the shuttle where the grooves for the 6mm 2GT X/Y axis belts probably printed really ugly. That's fine, realistically all we need here is some surface disruption to grip into the belts. In the STLs folder of this repo, I have added a zero-clearance support structure with some instructions you may use if you wish, but I don't recommend it - this isn't necessary and is only really useful to you if you already have a functional Stealthchanger or other filament-changing printer. On my redesign of the shuttle, just around the corner from those grooves, I have added some channels that you can use to slip excess length of the X/Y belts into - this helps get your belts tensioned properly by giving you somewhere to tug on them while preventing you from cutting your belts too short in case something goes wrong and you need to switch back to your original setup temporarily in an emergency. You DO lose about 4-5mm of Y axis travel because of the needed additional thickness and may therefore need to shift your bed forward that much if you use a nozzle cleaning brush in the rear corner, so be aware of that. If you don't care about having this in a compact one-piece package, there are also belt tensioning guides in the Stealthchanger repo, but I find using additional tools for what should be a fairly simple install to be a bit too much.

To install the shuttle:
- You'll first of course need to fully disengage the X/Y idlers on your gantry to give us some available room for tensioning once the new shuttle is installed.
- Remove the shuttle from your original toolhead. You should be stripping off everything so that your mounting surface is the four tips of the X/Y belts and the MGN12 shuttle.
- Insert the belts into the shuttle in the correct orientation and wrap them back around and into the previously-mentioned channels.
- Insert the 4x M3x8 SHCS screws used to mount the Stealthchanger shuttle on the MGN12 shuttle, but don't tighten them fully - you want to still be able to pull the belts through.
- Pull on both sets of belts with roughly equal tension (the more accurate you are here, the easier tensioning will be). 
- Once you are happy with the tension on the belts, screw the Stealthchanger shuttle down securely to the MGN12 shuttle.
- Returning to the X/Y idlers, apply proper and equal tension to each belt at the X/Y tensioners. Use your favorite trick for tensioning Voron 2.4 X/Y belts, just primarily make sure that it's even and you aren't over-tightening them. This can always be fine-tuned down the line.


# Preparing, Assembling, and Installing the Backplates
Each backplate will require one N52 6x2mm magnet, two M3x6 FHCS, two M3x8 SHCS, four M3 heat-set inserts, and three dowel pins as mentioned in the Bill of Materials section above. Once you install the parts to the backplate and have installed your shuttle on the X axis, skip down to the next section (Heat-Treating Process for Backplates), then return here.

After assembly and heat-treating, attach the backplate to the rear of the Stealthburner using the same screws that were previously used to secure it to the default Voron 2.4 shuttle design. Install the OptoTAP in its position on the rear of the backplate and verify fitup with the shuttle is still solid and snappy. If you notice your backplates are slightly tilted along the X axis, you can back out the two FHCS screws in the backplate to force its alignment with the shuttle, or re-do the heat treating process until the fitup is better. This isn't super commonly needed, but if your backplates didn't come out perfectly, you may experience slight tilting once the entire Stealthburner toolhead is loaded on the shuttle. Some advocate using a "paper test" to check screw alignment - get both screws roughly in the position you'd like and then try to shove a strip of generic A4 printer paper in between the magnet and screw. If both screws are adjusted equally, the paper shouldn't slide under either of them.


# Heat-Treating Process for Backplates

I have seen this documented both in the Stealthchanger Discord server by several people as well as in the Stealthchanger repo wiki. This is intended to improve the fitup between your backplates and the shuttle. The shuttle should already be installed on the gantry at this point. Here is the process I did:

- Install pins in the backplates.
- Place ONE backplate on the bed on its flat face, set bed temperature to 110c, and close the door.
- Wait around one hour. To check if it's been long enough, touch the metal pins - they should be hot.
- Turn off the bed heater and open the enclosure door.
- While still hot, install the backplate on the shuttle firmly. If it tries to lift itself, secure it only as much as is needed for it to seat properly with a ziptie.
- Close the enclosure door (we want to let the heat in the chamber SLOWLY drop).
- Allow this to sit for 4-5 hours or until the backplate is entirely cool to the touch.
- Once cooled, remove/insert the backplate into the shuttle a few times to see how fitup feels. If it's still bad, repeat. If it's still bad after repeating, you may need to reprint the backplate or shuttle.
- Repeat for each backplate.

This sounds a bit annoying, and it is - but this is how you get really accurate results with the OptoTAP in my experience.


# The Dock Crossbar and Bulking Out the Front of the Printer (not in the BOM!)

Now you may be thinking, "where are these docks supposed to go? If I just bolt a crossbar in here, I won't be able to move the Z axis up enough to change tools!" You are correct. There are two common approaches to this:
- Replace the front loop of 2020 extrusions in the Voron 2.4 frame with 2040's. This requires installing compatible joints with whichever style your frame uses.
- Cut down some 2020 extrusions the exact same size of the front extrusion loop of your printer's frame and stick it on to the front using your preferred method.

I went with the latter, as I had already done so for installing the Fridge Door/Klacky Door mod. I simply made another loop the exact same size and printed one of the thousands of designs of flat joining plates for 2020 extrusions. So, in total, the front frame loop of my Voron is THREE loops of 2020 extrusions. You only need two, or one loop of 2040 extrusions.

When you have handled this the way you see fit, you'll want your crossbar to fit between the first loop of T-slots after the ones that are part of the original frame. This crossbar needs to span side-to-side across the frame extension you've added and it'll need to be held in place with corner brackets (or internal corner brackets, which I like more). DO YOUR BEST to ensure it's as flat to the frame as possible - use a machinist's square and a bubble level if you need to. It doesn't have to be perfect, but it should be as close as you can get it.

The crossbar should be as HIGH UP as you can get it while still being reachable for your Z travel and allowing proper space for toolheads to dock and for the umbilical and bowden tube to not impact the top of the frame.

The third option here is to build what's called the Liftbar. I have no expertise or experience to share with this as it involves adding another axis to your 3D printer specifically for tools and is more at home on something like a Trident where the gantry doesn't travel along the Z axis. You can find more details about this in the Tapchanger repo if you wish to go that route, but I have no further/supplemental information about that and it will likely conflict with other information presented later in this document:
- https://github.com/viesturz/tapchanger/blob/main/Dock/Liftbar/Liftbar.md


# Other Assembly Notes
- In each Stealthburner you assemble, insert a 5x2mm magnet in front of the bottom two cowl screws. These will help secure the toolheads in their docks by magnetizing to the ends of the screws specified in the design documents for the dock parts linked above. Contrary to common opinion at the start, these DON'T get stuck in there forever - you can remove them just by magnetizing them to a piece of metal (ie. a machine screw head) from the outside and pulling them straight out. You may need to adjust the two M3x8 screws that get installed in the front of the dock to ensure they just kiss the magnets when the toolhead is fully docked - if they aren't long enough, that's weird, but you can substitute the M3x8's for a longer screw if needed.
- Ensure the X-axis dragchain is eliminated. Y-axis dragchain needs to remain in place for the X/Y endstop cable. All toolhead cabling is handled by the Nitehawk umbilical.
- Ensure the Z axis dragchain allows the Z axis to move cleanly through its entire travel to the top. If it's getting caught on the guide stop mounted on the rear of the gantry, move the guide stop. If it isn't long enough, extend it.
- When installing the dock crossbar, try to get it as even and square to the frame as possible. You won't get it perfectly but we can adjust for sub-mm variances in the firmware later.
- If you had a nozzle brush in the back-right corner of the printer that you used before, it will probably be offset with the modified shuttle. The bed needs to move forward to accomodate for this - or you need to move the brush to the front of the bed and modify your CLEAN_NOZZLE gcode macro.
- If you have very old X/Y belts, this is a great opportunity to install new ones.
- Also a great opportunity to install Beefy Front Idlers (BFI) if you haven't already: https://github.com/clee/VoronBFI


# Special Notes on OptoTAP
When you get your toolheads put together, one of the first things you should do is repeatedly run a probe using PROBE_CALIBRATE to help smooth out any rough spots on the contact points. In conjunction with the previously-mentioned heat-treating method, this will help greatly improve your OptoTAP readings.

Make sure your umbilical isn't too tight or too loose that it messes with your probing results! It's normal to adjust the length a few times in the PG7 connectors to ensure they aren't interfering. I advise not trimming and re-plugging the toolhead umbilical cable until you have locked in the positions for everything.

- Attach the toolhead you want to break in to the shuttle, home all axiis, and QGL.
- Move the toolhead to the center of your bed.
- Run the command PROBE_CALIBRATE SAMPLES=n where n = the number of Z axis probes you'd like to do. As you've already homed on Z successfully by this point, we know the probe is working, so we now want to run it up to as many as 500 probing samples to wear down contact surfaces into smooth operation. For example, PROBE_CALIBRATE SAMPLES=500 will probe the Z axis 500 times.
- Upon completion, run PROBE_CALIBRATE SAMPLES=25 and review the variance results that are reported in the console. You want the variance to be at an absolute maximum 0.025mm (the biggest variance recommended for Klipper), but using the methods described here, I have achieved a variance as low as 0.00028mm. When you achieve good results, edit your QGL macro in printer.cfg to the recommended 0.00750mm tolerance.


# Nozzle Offsets - Probe-to-Nozzle and Gcode

Follow the typical Klipper Z offset calibration procedure on T0 EXCEPT for saving config after the calibration - simply note the offset as it is reported in the console:
https://www.klipper3d.org/Probe_Calibrate.html#calibrating-probe-z-offset

You do not need to calibrate the probe-to-nozzle offset for the other tools, you simply need to ensure all prints start with T0 loaded on the shuttle (manually if needed0.

When the first tool loaded during a print does its initial homing routine and bed mesh at the start of a print, its nozzle offset is applied to the gantry. Meaning if the T0 is the first tool, and its offset is, say, -1.23mm, that will 
be the offset applied for the gantry as it is in motion during the print.

If T1 has a substantially different nozzle offset, say -0.23mm, and you start a print with T1 loaded on the shuttle, this will cause the following problems:
- Because all gcode offsets are calculated _against_ T0 and no other toolheads, your gcode offsets will be off.
- Because T1 in this instance is not the tool you applied a probe-to-nozzle offset to, its offset will be incorrect and this will proliferate to all other toolheads during the print. This may damage the bed and/or nozzle and/or toolhead.
- This WILL also lead to stacking tolerance problems when printing parts with embedded color changes (for example: a black circle on the side of a white cube).

Because of this, you need to compare the nozzle offsets of all tools against T0 and account for those differences in the gcode offset. In the specific example above, your gcode Z offset on T1 would be 1.

Note: Gcode offsets in positive values move the toolhead toward the "max" position of that axis to compensate, while offsets go toward the "min" position. This is in contrast to the normal probe-to-nozzle Z offset, where lower numbers INCREASE the offset.

In your toolhead config, set the real nozzle offset (the result you get in the console after finishing the PROBE_CALIBRATE procedure) as the z_offset value under [tool_probe tool0]. Ideally, do a test print with that value on that tool to verify that your first layer is good. When you have determined your needed gcode offsets for Z, set that as the gcode_z_offset value under [tool tool#]. More info about calibrating your X/Y offsets in section "Nozzle Gcode Offsets - X/Y Offset".

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
- Once finished, manually jog the toolhead to the point where it's sitting where you would like it to dock. Do this slowly and carefully, and start on the Z axis so you don't accidentally crash into your docks!
- Note that you MIGHT need to decrease your Y axis' minimum travel. I had to decrease the minimum travel to -10.
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
- Your tool will probably be at around 80mm-100mm on the Y axis now. This is going to be both your params_safe_y and params_close_y. While configuring this, you should be aware that you won't be able to dock your tools if a print gets higher than about 10mm (for safety) lower than your docking height. For me, that's about 180mm on Z. These are the sacrifices we make! Frame extensions are an option with longer Z belts and rails if desired.

Why the Safe Zone? Well, if you don't specify this, your toolhead may get too close to the dock when switching tools and end up ramming the bottom of the cowl into the lip of the dock as it rounds out the movement path. You can adjust these values as you see fit, but be sure to do it in small increments to avoid any unfortunate accidents!


# Purge, Preheat, and Other Relevant OrcaSlicer Settings

So first, you actually need to enable multi-material printing in Orca Slicer. Open your printer settings and switch to the "Multimaterial" tab. Under "Single extruder multi-material setup", ensure "Single Extruder Multi Material" is unticked, then enter "2" (or whatever number of toolheads you have) for "Extruders". At the very bottom of this page, you can enter a value in seconds for "Tool Change Time" - this is how long it takes your printer to depart from the print, switch tools, and return to the print. You should time and update this after dialling in your idle and preheat temperatures to ensure you get useful print time estimates.

After specifying that you have two extruders, a new tab called "Extruder 2" will appear alongside Extruder 1. You can enter retraction values and all the other fun per-toolhead settings you wish here, but leave the offset positions for the toolhead .cfg file.

I highly advise still using a purge tower despite no real need to flush the nozzle. Using a purge tower accomplishes two things:
- It allows the filament in the active tool to fully un-retract before reaching the print. If not accounted for and your retraction settings aren't perfect, your first layer after the tool change will be ratty.
- It catches nearly all of the ooze and whisps that accumulate on the nozzle in the brief travel from undocking to reaching the print.

When you generate a purge tower, I suggest placing it between the dock crossbar and your print so it can catch any ooze that happens during docking/undocking travel. You may also find that your **purge tower is bigger or smaller than you want it to be**. In order to change this, there are two things to change - first, you can adjust the width of the purge tower in the multimaterial settings on the left-side toolbar. This will still purge the same amount of material, but it will get less wide on the X axis but thicker on the Y axis. Second, you can change the actual volume of filament in the tower as a per-filament setting in the Purge Table. In order to access this, you will need to tick the "Single extruder multimaterial" box in the Multimaterial tab under Machine Settings - this will allow the Purge Table option to appear on the left-side toolbar just above filament selection. Once finished, untick the "Single extruder multimaterial" box in the Multimaterial tab under Machine Settings, which will keep the purge settings you've configured, but will make the Purge Table option disappear. This is an idiosyncrasy with OrcaSlicer that I hope gets fixed in a future release. I have each material purging 15mm^3 of filament and my purge tower width is 60mm. This results in a purge tower that's 60mm wide on the X axis and about 3mm thick on the Y axis.

You may omit the purge tower if your retraction settings are perfect and your toolchanges are super rapid, but a purge tower makes both of those much less of an issue and is still only fractionally wasteful compared to systems like the AMS. As of now, purge tower ("prime tower") settings in Orca Slicer are located in the global Multimaterial settings tab.

In addition, you will want to implement preheating and idle temp settings. Preheating does what you'd think; it fires off gcode at an estimated time to the next toolhead to be used to get it up to printing temperature, making the toolchange occur much faster. Preheating settings can also be found in the global Multimaterial settings tab in Orca Slicer. Leave the temperature variation delta at 0c because we're going to use per-material settings for that later. What you should then do is get your hotend up to 150-160c, where filament will be hot but not oozing yet, and then time how long it takes for the hotend to reach the printing temperature of the material you want to use. Add 10 seconds to this time and enter that for the "preheat time". Note that when you first start a print, the inactive toolhead won't be preheated to the idle temperature, so your first tool change will always be a little longer - you don't need to accomodate for that in the slicer settings, that's just how it is, so be aware.

Next we need to actually input the idle temperature we want to use. Next to the filament you have selected for the toolhead under "Filament", click the edit button. Under "Basic Information", near the bottom of that section, you'll see "Idle Temperature". Set that to the idle temperature you wish (I use 160C for Elegoo PLA+, for example). 

Finally, and this is more of a quality of life note - your print should always start on T0 so the offsets on your other toolheads apply correctly. With the Machine_Start gcode in the Stealthchanger repo, Orca Slicer will start with whatever toolhead has the most volume on the first layer. So if you're printing something that starts mostly with the material you have loaded in T1, you can add a primitive cube with only one layer of height and just enough surface area to print with the material in T0 to trick Orca Slicer into thinking T0 needs to be the start nozzle. I'm still looking for a better way around this, but it's better than a print failing. **You can avoid this** by using my Machine_Start and Change Filament Gcode, as well as the TOOLCHANGER_PRINT_START gcode macro I've edited - the slicer gcodes are in the Gcode folder, the TOOLCHANGER_PRINT_START macro is in this repo under Firmware in the toolchanger_macros.cfg file.


# Machine Start, Change Filament and Machine End Gcode

I have supplied the needed start and end print gcodes in the Gcode folder for Orca Slicer, as Orca Slicer currently has the friendliest functionality and most up to date features in my opinion:
- Machine Start and Change Filament Gcode: https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Gcode/OrcaSlicer%20Machine_Start%20Gcode.md
- Machine End Gcode: https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Gcode/OrcaSlicer%20Machine_End%20gcode.md

These will work with the other example CFG's I've provided here. The only special consideration is that, in order to differentiate toolchange starts/ends from non-toolchanger starts/ends, I have renamed the toolchanger print start and print end gcodes both in toolchanger.cfg and in the print start/end gcodes that need to be input to Orca Slicer. 

Otherwise, if you're just going to use the Stealchanger/Tapchanger defaults, make sure the Change Filament Gcode field has the following comment:
- ;Leave blank

This will prevent Orca Slicer from inserting its default filament change gcode. No other gcode settings are needed in Orca Slicer other than our start and end print gcode, unless you want to use my Change Filament Gcode.

If you are utilizing an existing Stealthburner LED configurations, make sure to insert the right gcode macros where needed in TOOLCHANGER_PRINT_START and TOOLCHANGER_PRINT_END.


# Nozzle Gcode Offsets - X/Y Offset

These offsets will entirely be done as gcode offset, particularly gcode_x_offset and gcode_y_offset values under [tool tool#]. My typical approach is to slice a 20mmx4mm cube,
starting with T0, and then insert a filament change to T1 once it reaches 2mm tall. When finished, you should mark which side of the cube was facing you when you pulled it off
of the bed to maintain the orientation.

When the print has completed, the two sections will most likely be offset by a small amount. I use a digital depth gauge to determine just how offset these are and note that for both axiis.
Once noted, enter the information for your gcode_x_offset and gcode_y_offset values in the tool you're calibrating as mentioned above. Remember; positive values move TOWARD the axis' travel limit.


# Final Considerations

Once you have achieved reliable toolchanging capabilities, you should get your extrusion multiplier dialled in and revise PID, Input Shaper, PA, retraction, etc. settings if needed. Otherwise, congratulations - you _should_ have a working Stealthchanger now.

Make sure to go to the Stealthchanger Discord and request a serial! https://discord.gg/kXuEYBsa



