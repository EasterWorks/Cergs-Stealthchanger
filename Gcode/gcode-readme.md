## THE SUPPLIED MACHINE_START AND MACHINE_END GCODE ARE TAILORED FOR ORCASLICER. Not guaranteed to work in Bambu Studio. Will not work in SuperSlicer forks.

## Both the Start and End gcodes reference my renamed "TOOLCHANGER_PRINT_START" and "TOOLCHANGER_PRINT_END" macros from toolchanger_macros.cfg.

# Machine Start
Enter this in the Machine Start field in OrcaSlicer under Machine Settings in the Machine Gcode tab. This gcode is identical to the start gcode provided in the Stealthchanger and Tapchanger repos, simply has the PRINT_START macro renamed.

# Change Filament Gcode
Enter this into the Change Filament Gcode field in OrcaSlicer under Machine Settings in the Machine Gcode tab. 

I was running into a problem where in the following two instances:
- Multiple toolheads would be working on the first layer
- A toolhead other than T0 was being used for the first layer after T0 completed the bed mesh

... that any tool other than T0 would not heat after being picked up, causing Klipper to throw an "extrude below minimum temp" error and cancel the print as part of its thermal runaway protection. 

The Change Filament Gcode I have provided handles this by throwing the first layer temperature value from the filament settings at the next toolhead explicitly on every change. This is a bit of a WIP because it's only piping through the first layer temp (not the "other layers temp"), but I'm working on a fix for that. For now - it's totally usable, but suboptimal.

# Machine End
Enter this in the Machine End field in OrcaSlicer under Machine Settings in the Machine Gcode tab. This is identical to the end gcode provided in the Stealthchanger and Tapchanger repos, simply has the PRINT_START macro renamed.
