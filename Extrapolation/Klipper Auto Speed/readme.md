Once your Stealthchanger is functioning reliably, I have found it valuable to run Kilpper Auto Speed by Anonoei, which you can find here:

https://github.com/Anonoei/klipper_auto_speed

For improving clarity, here is the entire process:

### Ensure Klippy-env is up to date:

```
sudo apt install python3
sudo apt install python3-numpy
sudo systemctl stop klipper
python3 -m venv --update ~/klippy-env
~/klippy-env/bin/pip install -r "~/klipper/scripts/klippy-requirements.txt"
```

### Install Klipper Auto Speed:

```
cd ~
git clone https://github.com/Anonoei/klipper_auto_speed.git
cd klipper_auto_speed
./install.sh
```

Note: Make sure you copy and paste the second line including the repo link into your SSH terminal. I initially typed it by hand and it prompted me to enter Github user credentials. If you copy and paste it, however, it doesn't do that. (shrug)

### Update Printer.cfg:

Copy and paste this to the bottom of your printer.cfg file (don't uncomment the commented-out lines):

```
[auto_speed]
#axis: diag_x, diag_y  ; One or multiple of `x`, `y`, `diag_x`, `diag_y`, `z`

#margin: 20            ; How far away from your axes to perform movements

#settling_home: 1      ; Perform settling home before starting Auto Speed
#max_missed: 1.0       ; Maximum full steps that can be missed
#endstop_samples: 3    ; How many endstop samples to take for endstop variance

#accel_min: 1000.0     ; Minimum acceleration test may try
#accel_max: 50000.0    ; Maximum acceleration test may try
#accel_accu: 0.05      ; Keep binary searching until the result is within this percentage

#velocity_min: 50.0    ; Minimum velocity test may try
#velocity_max: 5000.0  ; Maximum velocity test may try
#velocity_accu: 0.05   ; Keep binary searching until the result is within this percentage

#derate: 0.8           ; Derate discovered results by this amount

#validate_margin: Unset      ; Margin for VALIDATE, Defaults to margin
#validate_inner_margin: 20.0 ; Margin for VALIDATE inner pattern
#validate_iterations: 50     ; Perform VALIDATE pattern this many times

#results_dir: ~/printer_data/config ; Destination directory for graphs
```

Note: Technically you only need to include "[auto_speed]", but I advise grabbing the params as well so you can adjust if needed.


### Running Auto Speed:

Klipper Auto Speed has several macros you can utilize, though the fast way to do this is to just use AUTO_SPEED. You can append AXIS=[axis] to specify the axis you want to test. Example:

You want to test the Z axis.
```
AUTO_SPEED AXIS=Z
```

If you DON'T specify an axis, the X and Y axes will be tested.

Of incredible importance: Ensure your X/Y/Z max positions are accurate. My Voron 2.4 on paper has a 300mm max Z position, but in practice, it actually runs into hardware limitations at 280mm. I had never edited this parameter to be accurate to reality, so it was still set to 300mm, and my gantry tried to go to heaven when I first tried to test the Z axis. 


### What it does and how it works:

AUTO_SPEED will take around 5-10 minutes to run for each axis. It will home many times during this process.

For its testing procedure, Auto Speed will home the gantry to measure zero position, then do a short, quick move on the axis/axes being tested. Once done with the quick move, it will re-home and compare the home position to where the tool believed it was after the quick move. This determines step loss.

As the procedure continues, the short, quick moves will become more and more aggressive until Klipper Auto Speed sees a more than acceptable number of steps are being lost. It will then present max speeds and accelerations in the following format over the console:

```
AUTO SPEED found recommended acceleration and velocity after 243.31s
| DIAG X max: a23487 v421
| DIAG Y max: a23487 v421
Recommended accel: 23487
Recommended velocity: 421
```

### What to do with the results:

The results that Klipper Auto Speed will present are essentially the maximum acceptable **travel moves** for your printer. You don't want to run the printer at its absolute max all the time, so take about 20% off the top and use those as your new speed and acceleration maxes for the relevant axes.

After doing this and restarting firmware, I advise running a QGL with your finger on the E-stop. QGL will use the max X/Y/Z speeds and accelerations for travel moves. If you hear groaning, belt skipping, or anything else concerning, dial back the speed by another 10%. Repeat until expensive sounds stop happening, then slowly increase it until they start again. Then decrease slightly below that level, and you have your max X/Y/Z travel movements.


### Use case:

The default speeds and accelerations for the Z axis in the Voron 2.4 printer.cfg are :

```
max_z_velocity: 15 			#Max 15 for 12V TMC Drivers, can increase for 24V
max_z_accel: 350
```

In my experience, even doubling that default speed to 30 since Vorons run on 24v, this results in a 24-second toolchange procedure. It could be worse, but it could also be a whole lot better.

After running Klipper Auto Speed, I found the physical limitations of the Z axis were actually quite a lot higher:

```
AUTO SPEED found recommended acceleration and velocity after 619.64s
| Z max: a65974 v3917
Recommended accel: 65974
Recommended velocity: 3917
```

In practice, these were far too high. But using them to understand that my Z axis had very limited mechanical fluctuation helped me feel that I could safely increase speeds. 

My speed and acceleration for the Z axis are now:

```
max_z_velocity: 150
max_z_accel: 400
```

... which has resulted in toolchanges taking 9 seconds.

On top of just simply making toolchanges faster so prints don't take as long, this also helps reduce the ooze that happens when a tool is travelling from the dock to the print. On 24s toolchanges, my tools can ooze around 3-4mm of material, necessitating the use of a purge tower. At 9s, they barely have any time to ooze, meaning a purge tower is no longer mandatory. So not only cutting down toolchange times and reducing ooze, but also eliminating the purge tower, all contribute greatly to overall print speed and reduce the potential for failed prints.

Stats for nerds using the two-color Panda for reference, which has 151 tool changes:

**24-second toolchanges with a purge tower:**
- Total print time: 3h47m
- Time spent on toolchanges: 1h24s
- Time spent actually printing the Panda: 2h46m36s
- Filament used total: 51.81g
- Filament used on purge tower: 2.97g
- Filament used on actual print: 47.84g
- Total filament cost (for Elegoo PLA+ on both colors): $0.83 USD
- Cost of purge tower filament: $0.06 USD
- Cost of actual print filament: $0.77 USD

**9-second toolchanges with no purge tower:**
- Total print time: 2h54m
- Time spent on toolchanges: 22m39s
- Time spent actually printing the Panda: 2h31m21s
- Filament used total: 47.84g
- Filament used on purge tower: 0g
- Filament used on actual print: 47.84g
- Cost (for Elegoo PLA+ on both colors): $0.76 USD
- Cost of purge tower filament: $0 USD
- Cost of actual print filament: $0.76 USD

**Differences**
Prints with optimized toolchange speed and no purge tower vs without speed optimization using purge tower:
- ~23.5% less total print time.
- ~9.5% less total materials cost.
- ~5.7% less material waste on purge tower.
