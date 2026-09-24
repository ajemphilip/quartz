---
title: MooMoo Redesign Workbook
date: 2026-07-22
---
%% Draft prepared from the project files on 2026-09-21. Blocks marked TO FILL in the steps need Philip. %%

# MooMoo Redesign Workbook
This is the second workbook of the Moo Moo project. The first one, steps 0 to 19, followed the device from a single motorised pin in July 2024 to a talking six dot braille cell in January 2025 (start at [[0. Justification and Introduction]]). This workbook picks the device up again in November 2025 and follows its redesign until July 2026 in ten more steps, 20 to 29.

The redesign had four aims that run through all ten steps.
- Make each braille dot a module that plugs into the casing and can be pulled out, opened and repaired
- Print every mechanical part, including the lead screw and its nut, so that the device can be rebuilt from files
- Put the computer, the drivers and the power inside one casing and run it from a power bank
- Keep tuning the printed fits one number at a time, and keep every version

## How this workbook was written
The steps were reconstructed from the project folder and not from a diary. Every dimension comes from an OpenSCAD source file, every print setting from a PrusaSlicer project, every electrical rule from the Pi code, and every date from the time a file was last saved, converted to Toronto time. The folder holds 175 design files, 47 OpenSCAD sources, 123 STL exports and 5 slicer projects, and 77 source files of Pi code and setup app. The images were rendered in OpenSCAD 2021.01 with the BOSL2 library from the same sources at a lower resolution. Parts are coloured orange and blue because those are the filament colours stored in the slicer projects. Where an image contains something that is not in the source files, such as the outline of a Raspberry Pi or a block standing in for the power bank, the caption says so.

What a folder cannot hold is what happened at the bench. Each step therefore has blocks marked TO FILL for photos, measurements and what the parts felt like in the hand.

## Timeline of the files
![[MooMooRedesign_00_file_timeline.png]]
Every design file in the redesign folder by the day it was last saved, grouped by part family. The last row counts source files of the Pi code and the setup app

| Month | Design files saved |
|---|---|
| November 2025 | 11 |
| December 2025 | 17 |
| January 2026 | 20 |
| February 2026 | 14 |
| March 2026 | 6 |
| April 2026 | 20 |
| May 2026 | 87 |

Reading the whole timeline back, the redesign did not move at an even pace. It moved in six bursts with quiet weeks between them. The casing was drawn over Christmas week. The button stack followed in the first half of January. One long day on 3 February was spent on thread and shaft tests. 3 March split the button holder. 20 to 22 April brought the split motor casing, seven clamp ring exports and the head. Then half of all files in the folder were saved in the eighteen days between 4 and 21 May, when every part was brought into one folder, shortened, loosened or tightened, laid out on print plates and finally given a computer mount and a power bank pocket. The order inside that last burst is worth noticing. The actuator was finished first, then the Pi plate, then the pocket. The design grew from the moving part outward to the wall plug that it no longer needs.

Two habits show up in every burst. When a fit is in doubt, only that feature is printed (six sockets without a shell in step 21, a disc with a D shaped hole in step 22, the post of the cap without the cap in step 22). And when a number changes, the old file stays and the new one gets a name that says what changed (step 25 lists them).

## The ten steps
- [[20. Return to the pin. From a two part pin to a printed lead screw]]. November and December 2025. The old two part pin is exported one last time and is replaced by a parametric actuator with a printed screw and a square nut
- [[21. Three part casing with snap fit tabs and triangle ridges]]. December 2025 to February 2026. Three flat shells of 205 by 140 mm with shared pin positions and a printed snap fit
- [[22. Fit tests for the thread, the nut, the D shaft and the braille cap]]. January and February 2026. Pitch, nut clearance, shaft hole and cap seat are each printed alone
- [[23. Button stack on the moving pin. Lifter, threaded holder, transfer cube and presser]]. January to March 2026. A push button rides on every dot, held by its own thread
- [[24. Splitting the motor casing. Detachable half, clamp ring and a plug in base]]. March to May 2026. The motor becomes removable and the actuator becomes a module with a fixed depth in its socket
- [[25. Character head with an angle key and a round of small print adjustments]]. April and May 2026. The cow head returns on a key with four angles, and twelve single number adjustments are listed
- [[26. Printed lead screw v1 to v5 and the elevator nut]]. May 2026. Ten screw exports in one day, a 3 mm pitch and a looser nut
- [[27. One actuator module as a print set. Shorter piston, split button cylinder and a TPU braille cap]]. May 2026. Twelve printed parts for one dot, nine of them on one plate, and a soft cap
- [[28. Sliding Raspberry Pi plate and motor driver clips in the bottom shell]]. April and May 2026. The Pi moves from four posts on the wall to a plate that slides and clicks
- [[29. Power bank pocket, speaker mounts and the shared 5 V rail]]. May to July 2026. A pocket for the power bank, zip tie mounts for two speakers, and the rules in the Pi code that keep six motors from browning out the computer

## What changed since the first workbook
| | First workbook, 2024 to 2025 | Redesign, 2025 to 2026 |
|---|---|---|
| Drive of a dot | Geared DC motor with a metal screw and nut | Small geared motor with a printed screw of 3 mm pitch and a printed square nut |
| End stop | Aluminium foil touch sensor on the ESP32 | Time limit of 1.5 s in the Pi code |
| Motor mount | Closed printed casing | Split casing with a detachable half, a clamp ring and one bolt |
| How a dot sits in the device | Pin holder tray | Square base of 8.1 mm in a socket of 8.45 mm with grip dots and a stopper plate |
| Button | In a holder on top of the pin | In a split threaded cylinder, pressed by a guided piston |
| Braille cap | Hard print | Ultrafuse TPU 64D, held on a 5.4 mm post by four bumps |
| Casing | One rounded body with a top tray, second box for electronics | Three flat shells that snap together, electronics inside |
| Motor control | ESP32 over UART from the Pi | Raspberry Pi Zero 2 W directly over GPIO to three TB6612FNG boards |
| Power | Wall supply and cables to a computer | One USB power bank in a pocket on the casing |
| Printer and material | MakerBot Replicator+, PLA | Prusa CORE One and Original Prusa MK4S, PETG and TPU |
| Setup | Monitor, keyboard and mouse on the Pi | Setup app over the device's own wifi hotspot or Bluetooth |
