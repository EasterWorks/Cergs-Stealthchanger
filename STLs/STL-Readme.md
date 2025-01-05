# Explanation of STL files in this folder


### MGN12-shuttle.stl:
This is a replacement for the shuttle in the Stealthchanger repo that adds channels for excess belt pathing. The intention is that you will thread your belts around the "corner" and into the available channels as far as possible, then trim anything that sticks out of the sides. This both helps install the shuttle without juggling the belts and using strange methods to hold the belts in place and allows for the advisable retention of extra belt length just in case. Actual amount of Y axis travel loss TBD.

### zero_clearance_supports.stl
This is an OPTIONAL part for printing the shuttle with a pre-made zero-clearance support structure. This is intended for you to use _after_ you already have your Stealthchanger assembled in the event you'd like to use a higher quality material, or simply to get a """"better""" shuttle print, but you could feasibly do it with manual filament changes if you're okay with sitting there watching for 64 tool changes. 

Print settings:
- Import this into OrcaSlicer, set it to be printed with your tool that is loaded with PLA, PLA+, or PLA Repid. Set its position to the center of the bed.
- Import MGN12-shuttle.stl and set that to print with your main printing material. Center its position on the build plate so it sits squarely on top of the support structure. Use the sensor probe tab at the "top" of the shuttle to assist with alignment on x/y if needed.
- First layer should be 0.25mm.
- Use the normal 4 walls, 5 tops/bottoms, and 40% infill recommended for the project.
- For the support structure, ensure all top surfaces are ironed.
- Increase your PLA build plate temperature to match the build plate temperature of the material you're using for the shuttle.
- **NOTE**: This is **NOT NECESSARY** for a functioning shuttle! Some people can't resist the urge to print it with a super clean rear face, and some people might want to sell printed parts kits that look visually stunning all around - this will do it. 

### x-axis-prod.stl
Both the default shuttle and my above redesign won't have sufficient width to hit the X axis limit switch without crashing into the gantry. This is a small plate that screws into the bottom of the above shuttle with two M3x8 SHCS screws and sticks out just enough to hit the trigger before the gantry crashes. Actual amount of X axis travel loss TBD.
