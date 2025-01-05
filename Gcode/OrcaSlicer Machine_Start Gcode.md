# Start Gcode for OrcaSlicer
This is the gcode from the Toolchanger github repo, but I have changed "PRINT_START" to "TOOLCHANGER_PRINT_START" to match the edits made in my toolchanger.cfg file in this repo. This will accomodate for up to 6 toolheads. If you are planning on adding more than 6, you will need to iterate more of these "{if is_extruder_used[#]}T#_TEMP={first_layer_temperature[#]}{endif} " lines. This all needs to be copy and pasted as one line into your Start Gcode field in Orca Slicer. You can omit these comment lines.

```TOOLCHANGER_PRINT_START TOOL_TEMP={first_layer_temperature[initial_tool]} {if is_extruder_used[0]}T0_TEMP={first_layer_temperature[0]}{endif} {if is_extruder_used[1]}T1_TEMP={first_layer_temperature[1]}{endif} {if is_extruder_used[2]}T2_TEMP={first_layer_temperature[2]}{endif} {if is_extruder_used[3]}T3_TEMP={first_layer_temperature[3]}{endif} {if is_extruder_used[4]}T4_TEMP={first_layer_temperature[4]}{endif} {if is_extruder_used[5]}T5_TEMP={first_layer_temperature[5]}{endif}  BED_TEMP=[first_layer_bed_temperature] TOOL=[initial_tool]```

# Change Filament Gcode for OrcaSlicer
I have also found that some specific Change Filament G-code is needed (a few fields beneath the machine_start gcode text field) if you want to be able to print two or more materials on the same first layer. This is what I use:

```M104 S{first_layer_temperature[next_extruder]} T[next_extruder]
T[next_extruder]
M109 S{first_layer_temperature[next_extruder]} T[next_extruder]
```
