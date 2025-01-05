Explanation of STL files in this folder:


### MGN12-shuttle.stl:
This is a replacement for the shuttle in the Stealthchanger repo that adds channels for excess belt pathing. The intention is that you will thread your belts around the "corner" and into the available channels as far as possible, then trim anything that sticks out of the sides. This both helps install the shuttle without juggling the belts and using strange methods to hold the belts in place and allows for the advisable retention of extra belt length just in case. Actual amount of Y axis travel loss TBD.

### zero_clearance_supports.stl
This is an OPTIONAL part for printing the shuttle with a pre-made zero-clearance support structure. Import this into OrcaSlicer, set it to your tool loaded with PLA, PLA+, or PLA Repid, then import MGN12-shuttle.stl and set that to your main printing material. For the support piece, ensure all top surfaces are ironed. Ensure the X/Y positions of each part are the same. Increase your PLA build plate temperature to match the build plate temperature of the material you're using for the shuttle. This is NOT NECESSARY for a functioning shuttle, but some people want to print the back part really clean, and this will do it. 

### x-axis-prod.stl
Both the default shuttle and my above redesign won't have sufficient width to hit the X axis limit switch without crashing into the gantry. This is a small plate that screws into the bottom of the above shuttle with two M3x8 SHCS screws and sticks out just enough to hit the trigger before the gantry crashes. Actual amount of X axis travel loss TBD.
