# Description of CFG files:

As a forenote here: most people leave the folder for all of the Toolchanger and Stealthchanger-specific cfg's in a folder called "Tapchanger" because that's how the original configs are built. I have changed this folder to be named "Stealthchanger" as that's more fitting. This is a personal choice, do what you prefer but pay attention if you name it something other than "Stealthchanger"!

### printer.cfg
Naturally, this is your printer's config file. It's where the baseline definitions for where hardware is connected to on your mainboard lives. Note that things like the probe section and extruder config have been removed - those are now in t0 and t1 CFG's. Also note the includes and their order. This is a modification of the default Voron V2.4r2 printer.cfg example from Klipper.

### toolchanger.cfg
This is where almost everything Toolchanger-specific is going to live. All you really need to change here are "params_safe_y" and "params_close_y". More info on that in "Docking Calibration" in the calibration manual linked below. This is from the Klipper-Toolchanger repo.

### toolchanger_macros.cfg
This is where the Toolchanger-specific macros go. Note that I have changed the PRINT_START and PRINT_END macro names to "TOOLCHANGER_PRINT_START" and "TOOLCHANGER_PRINT_END", and commented out a few lines that only seemingly exist to report errors. I may uncomment those eventually but when I see "unknown command" in the terminal and the command doesn't appear to do anything, it will get excluded. This is from the Klipper-Toolchanger repo.

### stealthchanger_macros.cfg
This includes some additional and entirely optional macros. You don't have to use this. This is from LDO's documentation.

### t#.cfg
This is the cfg for your toolhead! I have added a few notes to the CFG's provided in this repo where you need to pay extra attention. This is a combination of the tool examples in the Tapchanger repo and from LDO's documentation.

### tool_detection.cfg
This cfg includes the crash detection functionality and is important for avoiding accidents. I'm not super sure why it's seprate from the main toolchanger.cfg file, but as presented it shall stay on my printer. This is from the klipper-toolchanger repo.

### calibrate_offsets.cfg
This cfg includes some functionality for calibrating the nozzle offsets between different toolheads using probes like Sexball. I do adjustments with a test print and a digital depth gauge, which I cover under "Nozzle Offsets - probe-to-nozzle and gcode" in the calibration manual linked below. This is from the klipper-toolchanger repo.

### homing.cfg
This cfg includes the new homing override you'll want to use, sensorless homing functionality (which I have commented out because we're using physical endstops here), and some tool offset functionality for homing, gcode, and meshing. The latter three aren't called in my config but are there for testing if needed. This is from the klipper-toolchanger repo.


# Calibration manual:
https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md
