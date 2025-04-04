# Cergs-Stealthchanger

Repo status: READY (ready for public reference)  

This repo contains my configurations and customizations for my Stealthchanger build.  

This repo may be useful to you if you have similar design constraints and requirements to my own:

- You have a 300mm Voron 2.4r2.
- Your mainboard is a BTT Octopus Pro or board with similar capabilities.
- You want to use Stealthburner toolheads with the E3D Revo hotend ecosystem.
- You are using LDO's Nitehawk-SB or Nitehawk-36 toolhead boards and Isik Tech's Birds' Nest for toolhead board networking.
- You are using the standard X/Y endstops that are located on the intersection of the X and Y axiis rather than the toolhead-mounted endstops or sensorless homing.
- You are want to use OptoTAP v2.4.1 for your Z axis probe and endstop trigger.
- You are me in the future and nuked your config files again or forgot how to calibrate something.


In addition, I have edited and provided a few STL's that improve upon the original design and/or make it more suitable for the above considerations.  

This repo is under construction. The top line of this readme document says "Repo status" - I will keep this up to date as I update my progress on the toolchanger project.

If you have any questions about necessary plugins or part designs, please reach out to the original creators (whom will be listed and credited when their content is used). I also HIGHLY recommend joining the public Stealthchanger Discord channel, link here: https://discord.gg/kXuEYBsa


## Mile-High Overview of the Stealthchanger

[This](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/mile-high-overview-of-the-stealthchanger.md) is a shorter document than the Hardware and Calibration document which is going to cover the basic concepts as a toe-dip. 


## How to Stealthchanger

I have created a guide in this repo that covers all the steps I took from day 1 to fully-functional. You can find it here: https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md


## Extrapolation

You will notice that there is a folder named "Extrapolation". This includes experiments I've done with the Stealthchanger ecosystem to try to make it more approachable, more reliable, and overall improved. It primarily has a focus on lessons learned for now, but I will include files and information for anything that I tried that I found particularly valuable as well.


## Credits:  
Viesturz, "tapchanger"  
- https://github.com/viesturz/tapchanger  

DraftShift Design, "StealthChanger"  
- https://github.com/DraftShift/StealthChanger  

DraftShift Design & Viesturz "klipper-toolchanger"  
- https://github.com/viesturz/klipper-toolchanger (use this one until DraftShift greenlights their version for public use!)
- https://github.com/DraftShift/klipper-toolchanger  

Thiessen with DraftShift Design for being INCREDIBLY helpful and patient with helping the community find answers when needed.

The Stealthchanger community for being encouraging and offering guidance.

All the people I've linked under printed part recommendations in the above guide.


## Updates:

12/13/2024:  
- Added my initial configs assortment. Some are incomplete.  

12/24/2024:
- Added OrcaSlicer start gcode.

12/29/2024:
- Updated all CFG files as the project is now functional (in testing)

12/30/2024:
- Final touches on cfg examples.
- Refined and added a ton of info to the guide document.
- Updated repo status from "IN TESTING" to "READY".


