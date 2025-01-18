# Lessons Learned

This is going to be a compilation of trials I've done with the Stealthchanger system, particularly in expansion efforts over the original designs.


## Redesigning Parts

I didn't like the idea of cutting my belts exactly to length for the shuttle, so I designed a version of the shuttle which has integrated pathing for looping the belt around, so around 3-4cm of extra belth length can be retained. I found that this was resolved by a part from the SC repo called the shuttle keeper. This does basically the exact same thing, though it's a separate part instead of being integrated directly to the shuttle, so I do still personally prefer my design.

In addition, I designed an X axis endstop trigger as a separate part for the shuttle. The SC repo does have an option for this as well, but it's a much larger part overall. I prefer mine for being lower profile while still doing the same work.

**Lesson learned:** Check the Stealthchanger repo thoroghly before designing your own parts to solve problems. However, don't be afraid to make your own anyway if you have what you feel is a better idea for your setup and needs.


## SLS Shuttle and Backplates

On a conceptual level, I was very interested in using SLS PA12 nylon processing for the shuttle and toolhead backplates. I ordered these from Xometry, whom I've had good experiences with in the past.

Upon outfitting with pins and magnets, the initial fitup was INCREDIBLY good. I adjusted the tilt screws and got them all installed. 

Unfortunately, in practice, I found that one of my backplates was perfectly usable, but the other had a slight deformation on the OptoTAP mounting screw holes. In SLS processing, there is only really one step where this can happen, and that's in the phase immediately after the printing process where the entire printing chamber is allowed to cool to ambient temperature in order to prevent the parts in the cake from warping during removal. My theory is that my problematic backplate was part of a batch which was pulled out of the chamber without being fully allowed to cool, which introduced around 0.25mm of warp. I attempted to fix this by dremelling out the screw hole location and filling with epoxy, but this was messy and didn't provide good results.

However, the SLS shuttle is working great with both the "good" SLS backplate and my previously-made FDM backplates.

**Lesson learned:** If your FDM shuttle and backplates are working well and are printed from high-quality materials, there is no reason to go with SLS replacements. It may one day be worth it to use CNC'd aluminum components when they are available.


## Piano Wire Umbilical Management

From the first moment I installed the 1mm piano wire for umbilical control, I realized they were too stiff to run all the way to the toolhead, as it would pull the toolhead forward when it was near Y max - throwing off QGL and bed mesh results pretty significantly. There is another option to use 0.3mm x 3mm spring steel, but the most readily-available option for this is to purchase via Aliexpress. If you're like me, waiting 2-3 weeks for your parts to arrive means your printer is going to be essentially unusable for 2-3 weeks. 

Using closer to a 0.6mm-0.8mm piano wire so it can be constrained on the toolhead would help with this, 1mm is just seemingly too stiff.

Ultimately, the correct solution here is to use Igus ChainFlex cabling to replace your standard umbilical cable. This is quite cheap - if you buy directly from Igus, it's $1.25/ft. I ordered from West3D to ensure that the cable diameter was actually 7mm (same as the original umbilical) and had 6 conductors - Igus offers 5 and 7 conductors, but not 6 for whatever reason.

**Lesson learned:** TBD, haven't received the ChainFlex quite yet.


## Combatting Ooze

Every toolhead is going to ooze a little bit. When tools are travelling from the docks to the print, there will usually be at least a few MM of ooze. This boils down to the following factors:
- Retraction
- Filament printing temperature
- Tool change times

First, go through your firmware and slicer settings to find what your retraction settings are. I have found a ton of spots in OrcaSlicer and in Toolchanger where retraction is set to 2mm, and many of them stack. At one point, my extruders were trying to pull back 8mm of filament when a print was paused and then cancelled. Other times, it would retract 4-8mm during tool changes, and when unretracting, the remaining filament in the nozzle would get rapidly shoved out and create an ooze trail.

Second, if you haven't done one in a while, print temperature towers with each filament you want to use and the tools you want to use it on. Pick the temperature that looks the best, has the best bridging, and is cold as possible. Add 5-10C to it if you intent to print at rapid speeds (or possibly more if you use HF nozzles). This should help minimize how much the filament will ooze just from melting in the nozzle as the tool travels.

Third, your tool change times. You should get these as fast as possible without introducing unreliability. Run [Klipper Auto Speed](https://github.com/EasterWorks/Cergs-Stealthchanger/blob/main/Extrapolation/Klipper%20Auto%20Speed/readme.md) to determine your X, Y, and Z max travel sppeds and accelerations.

With these three factors dialed in, your ooze should be reduced significantly.
