# Lessons Learned

This is going to be a compilation of trials I've done with the Stealthchanger system, particularly in expansion efforts over the original designs.


## SLS Shuttle and Backplates

On a conceptual level, I was very interested in using SLS PA12 nylon processing for the shuttle and toolhead backplates. I ordered these from Xometry, whom I've had good experiences with in the past.

Upon outfitting with pins and magnets, the initial fitup was INCREDIBLY good. I adjusted the tilt screws and got them all installed. 

Unfortunately, in practice, I found that one of my backplates was perfectly usable, but the other had a slight deformation on the OptoTAP mounting screw holes. In SLS processing, there is only really one step where this can happen, and that's in the phase immediately after the printing process where the entire printing chamber is allowed to cool to ambient temperature in order to prevent the parts in the cake from warping during removal. My theory is that my problematic backplate was part of a batch which was pulled out of the chamber without being fully allowed to cool, which introduced around 0.25mm of warp. I attempted to fix this by dremelling out the screw hole location and filling with epoxy, but this was messy and didn't provide good results.

However, the SLS shuttle is working great with both the "good" SLS backplate and my previously-made FDM backplates.

**Lesson learned:** If your FDM shuttle and backplates are working well and are printed from high-quality materials, there is no reason to go with SLS replacements. It may one day be worth it to use CNC'd aluminum components when they are available.


## Piano Wire Umbilical Management

From the first moment I installed the 1mm piano wire for umbilical control, I realized they were too stiff to run all the way to the toolhead, as it would pull the toolhead forward when it was near Y max - throwing off QGL and bed mesh results pretty significantly. There is another option to use 0.3mm x 3mm spring steel, but the most readily-available option for this is to purchase via Aliexpress. If you're like me, waiting 2-3 weeks for your parts to arrive means your printer is going to be essentially unusable for 2-3 weeks. 

Ultimately, the correct solution here is to use Igus ChainFlex cabling to replace your standard umbilical cable. This is quite cheap - if you buy directly from Igus, it's $1.25/ft. I ordered from West3D to ensure that the cable diameter was actually 7mm (same as the original umbilical) and had 6 conductors - Igus offers 5 and 7 conductors, but not 6 for whatever reason.

**Lesson learned:** TBD, haven't received the ChainFlex quite yet.
