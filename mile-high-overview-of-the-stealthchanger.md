# Mile-High Overview of the Stealthchanger

Want a more consise description of the Stealthchanger and don't want to scroll through a ton of Github pages, YouTube videos that only cover fractions of the overall picture, or my huge Hardware and Calibration document? Start here!

### What is Stealthchanger?
[Stealthchanger](https://github.com/DraftShift/StealthChanger) is a toolchanging system by DraftShift Design based on Viesturs Zariņš' [Tapchanger](https://github.com/viesturz/tapchanger) project. Stealthchanger uses a different shuttle design than the Tapchanger and supports a wide array of toolheads.

DraftShift Design's toolchanger project will _eventually_ be a hollistic overhaul of Tapchanger and Klipper-Toolchanger, but their firmware scripts are still in the prototype stage as of this writing, so they are currently leaning on Viesturs' framework - this will _eventually_ change, but for now, you can't have Stealthchanger without Tapchanger.


### How does Stealthchanger work?
On the hardware side, the original Voron 2.4 toolhead shuttle is replaced with one that has embedded magnets and sleeve bearings. Instead of mounting directly to the shuttle, toolheads now mount to a backplate, which is equipped with a magnet, some screws for adjusting interface angle, and some pins to match the sleeve bushings in the new shuttle.

On the software side, Stealthchanger relies upon an add-on package called [klipper-toolchanger](https://github.com/viesturz/klipper-toolchanger). This includes routines, functions, and macros that are used to dynamically equip different toolheads as they are called from customized gcode in your slicer software.


### What printers is it compatible with?
Stealthchanger and Tapchanger are both configured to work with Voron 2 printers, specifically the [Voron 2.4r2](https://vorondesign.com/voron2.4) (the current iteration of the Voron 2.4 at the time of this writing), but some compatability is present with the design prior to revision 2 which used MGN-9 rails instead of MGN-12 rails. DSD is currently working internally on making a compatible version for the Voron Trident as well.

Ultimately, the shuttle, backplates, dock, and add-ons/scripts may be able to function with any Klipper-based 3D printer, but if you're installing it on any printer than the Voron 2 series, significant adaptation/customization will be required.


### How hard is it to build and set up?
Setting up the Stealthchanger is only going to be difficult in the following scenarios:
- You have difficulty customizing .cfg files due to lack of understanding how Klipper works.
- You aren't familiar with gcode macros and variables.
- Your printer is not calibrated well.

I'd say you only need a basic comprehension of Klipper programming and gcode writing to get things working, as long as your printer is calibrated well and producing good-quality and accurate prints. I have done my best to write my [Hardware and Calibration document](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md) as if the reader didn't know anything about the configuration options and installation/calibration process, and I'm constantly updating it to clarify wording, add little things I didn't consider including initially, and so on.


### What kind of tools do I need to have?
Just the normal stuff!
- A computer with SSH connectivity capabilities.
- Wire cutters.
- Hobby knife.
- Files/sandpaper.
- Wire strippers.
- Crimping tool.
- Soldering iron, ideally with an M3 heat-set insert tip.
- Zipties
- Pliers.

Basically just the normal tools you'd need for maintaining a 3D printer.


### What print settings should I use?
DSD recommends printing Stealthchanger components to Voron specifications. These are as follows:
- Layer height: 0.2mm
- Extrusion width: 0.4mm (forced)
- Infill density: 40%
- Infill type: Grid, gyroid, honeycomb, triangle, or cubic
- Wall count: 4
- Top/bottom layers: 5

The one exception is that you WILL need to use supports for the Stealthchanger shuttle, but backplates and most of the dock parts are designed to print unsupported.


### Is there a guide on how to do this project from start to finish?

I have written a [Hardware and Calibration](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Hardware-And-Calibration.md) document that covers everything from bill of materials and print selection to installation, calibration, and customized slicer gcode settings. It is fairly comprehensive, but still a work-in-progress. It should have enough information to at least fill in gaps and help figure out what you need to research further.

Otherwise, DSD has a Discord channel specifically for the Stealthchanger project, and there are a lot of helpful folks there willing to help where you get stuck. Be polite and respectful. Invite link: https://discord.gg/kXuEYBsa 
