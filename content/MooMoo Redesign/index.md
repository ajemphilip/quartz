---
title: MooMoo Redesign Workbook
date: 2026-07-22
---
%% Draft prepared from the project files on 2026-09-21. %%

# MooMoo Redesign Workbook
This is the second workbook of the Moo Moo project. The first one, steps 0 to 19, followed the device from a single motorised pin in July 2024 to a talking six dot braille cell in January 2025 (start at [[0. Justification and Introduction]]). This workbook picks the device up again in November 2025 and follows its redesign until July 2026 in twelve more steps, 20 to 31.

The redesign had four aims that run through all twelve steps.
- Make each braille dot a module that plugs into the casing and can be pulled out, opened and repaired
- Print every mechanical part, including the lead screw and its nut, so that the device can be rebuilt from files
- Put the computer, the drivers and the power inside one casing and run it from a power bank
- Keep tuning the printed fits one number at a time, and keep every version

In the maker's words the redesigned Moo Moo is more accessible and more modular than the first device.

![[MooMooRedesign_00_device_exploded.png]]
The redesigned device taken apart in OpenSCAD. 1 bottom shell, 2 Raspberry Pi on its sliding plate, 3 the six actuator modules, 4 middle shell, 5 power bank lifted out of its pocket, 6 the two speakers, 7 top shell, 8 key, 9 head. The Pi, the power bank and the speakers are drawn as plain blocks of the size the sources allow for, everything else is rendered from the newest SCAD file of each part

## The device as it stands
The newest file in the folder was saved on 21 May 2026 for the hardware and on 22 July 2026 for the software. Taken together the newest files describe one device, and this section says what that device is and what goes where. The steps below tell how each part got there.

![[MooMooRedesign_00_device_section.png]]
The closed device cut along its near row of dots. 1 bottom shell, 2 middle shell, 3 top shell, 4 an actuator module with its dot down, 5 a module with its dot up, 6 a speaker, drawn as a plain disc, 7 head on its key. The motors are drawn as 6 mm micro gear motors and the push buttons as plain grey cylinders. The power bank pocket is on the side that is cut away

The casing is three shells of 205 by 140 mm that snap onto each other and stand 144 mm tall. The bottom shell lies with its closed face on the table. Six actuator modules stand in its six sockets, the Raspberry Pi stands on a sliding plate against one long wall and the three motor driver boards stand in clips against the other. The middle shell is an open ring around the modules. It carries the power bank in a pocket on the outside of one long wall and the two speakers on its back wall. The top shell closes the casing and has six round openings, one above each socket. The head hangs on a key in the front wall of the top shell.

One module is one braille dot. From the socket upward it is the shaft body with the motor inside, the lead screw and its nut, the lifter that the nut carries, the transfer cube, the split cylinder with the push button, the piston, the presser casing and the soft cap. When the motor turns, everything from the nut upward rises together, and the cap comes up through the opening in the top shell. With the dot down the cap ends about 3 mm below the top face of the shell. The parts allow 24 mm of travel. Pressing the cap pushes the piston onto the button. Step 27 has the same section for a single module with every part numbered.

| Part | For one device | Newest source | Newest export | Step |
|---|---|---|---|---|
| Bottom shell | 1 | `bottomCasingAdjustedCubesandTrianglesSlidablePi.scad`, 21 May, with `PART = "base"` | `...SlidablePiBase.stl`, 14 May | 21, 28 |
| Pi plate | 1 | The same file with `PART = "plate"` | `...SlidablePiSliderShorterScews.stl`, 15 May | 28 |
| Shaft body | 6 | `ShaftBodyAdjustedKraweznik.scad`, 11 May | `ShaftBodyAdjustedKraweznik.stl`, 11 May | 24 |
| Detachable half of the shaft body | 6 | The same file with `detachableHalf()` | `ShaftBodySm.stl`, 11 May | 24 |
| Clamp ring | 6 | `clamp ring bigger - different mechanism .scad`, 14 May | `clampsmallerStronger .stl`, 8 May | 24 |
| Lead screw | 6 | `screwReducedDshaftCylninder.scad`, 12 May | `screwReducedDshaftCylninderv5.stl`, 12 May | 26 |
| Elevator nut | 6 | `elevator.scad`, 14 May | `elevatorBiggerSlop.stl`, 12 May | 26 |
| Lifter | 6 | `elevatorLifterWButtonCube.scad`, 28 February | `elevatorLifterWButtonCube.stl`, 6 May | 23 |
| Transfer cube | 6 | `buttonTransferWCubeAdjustedGripandBelka.scad`, 11 May | `buttonTransferWCubeAdjustedGripAndBelka.stl`, 11 May | 27 |
| Split button cylinder, two halves | 12 | `buttonCylinderTriangleSplitShorterTry.scad`, 14 May | `...ShorterTry.stl` and `...ShorterTry1.stl`, 12 May | 27 |
| Piston | 6 | `buttonPresserPistonShorter.scad`, 11 May | `buttonPresserPistonShorter.stl`, 11 May | 27 |
| Presser casing | 6 | `buttonPresserCasing.scad`, 19 May | `buttonPresserCasing05MMAdjusted.stl`, 16 May | 27 |
| Braille cap, air TPU | 6 | `topBraillelowerAttachement.scad`, 11 May | `topBrailleLowerAttachement.stl`, 11 May | 27 |
| Middle shell | 1 | `middleCasingHooksPowerPocketandZipSpeakers.scad`, 21 May | `...PowerPocketandZipSpeakersAdjusted.stl`, 19 May | 21, 29 |
| Top shell | 1 | `topCasingSmallerDots.scad`, 12 May | None. `topCasing.stl` of 11 May has the larger grip dots | 21 |
| Key | 1 | `keyMooHeadSmallerDots.scad`, 12 May | None. `keyMooMooHeadAdjustedCube9mm.stl` of 11 May has the cube of 9 mm | 25 |
| Head | 1 | `moomooHeadAdjustedRowek.scad`, 21 April, in the folder casingFixed | `moomooHeadAdjustedRowek.stl`, 21 April | 25 |
| Pi code and setup app | | Folder `RaspberryAndPython`, last saved 22 July, on GitHub as `moo-moo-dashboard` since 20 November 2026 | | 28 to 33 |

All files are in the folder finalMooMoo unless the table says otherwise. For every row that names an export, the newest source was rendered again and compared with the mesh in the folder, and the two agree. The top shell and the key are the two parts whose newest source was never exported into the folder. One module needs one motor, one push button and one bolt in addition to its twelve printed parts. The device also needs a Raspberry Pi Zero 2 W, three TB6612FNG boards, a USB sound card with a microphone, two speakers and a power bank.

Two things are not fixed by the files. The snap fit of the bottom shell is the same on all four sides, so it can sit either way round under the middle shell (steps 21 and 29). And the slots for the speakers pass through the back wall without saying on which side of it the speakers sit (step 29).

## The order of the redesign in the maker's words
On 3 November 2026 the maker described the order in which the redesign was done. The steps of this workbook are numbered by the dates of their files, and the list below gives the order of the work as the maker tells it.
1. **The pin and its elevator.** A printed screw and its nut, and a rectangular elevator that moves up and down on rails inside its casing. Rebuilding that casing was the first move towards a better way of raising and lowering the pin (steps 20, 22 and 26)
2. **The mounts for the braille cap and the button.** Several variants. A cylinder with teeth was meant to hold the button and let it click, and it failed. A hollow cylinder with grip dots replaced it (steps 22 and 23)
3. **The threaded button mount.** The mount became the current threaded model and was split in two for better accessibility (steps 23 and 27)
4. **The casing.** Several sizes of triangle and several modular sections were tried. The top was printed against the bed plate so that it came out very smooth, and the Original Prusa MK4S helped with this far more than the MakerBot Replicator+ of the first workbook (steps 21 and 25)
5. **Cable management and the Pi mount.** Once the triangles fitted, holes and attachments in the bottom were designed to hold the cables, and the Pi got a plate that slides along the side wall (steps 28 and 29)
6. **The electronics.** The Pi alone, without the ESP32, with the TB6612FNG boards wired to it. The Pi is set up through a separate wifi network of its own or over Bluetooth and calls the cloud ChatGPT model itself, with a local model planned as a second quality preset and not implemented yet (step 30)
7. **Pin calibration.** The last step, a way to match each motor and each button to its dot (step 31)

## What was kept after testing
Every step tried several versions before one was kept. This table gives the version each part of the device keeps, and the steps tell how it was reached.

| Part or feature | Tried | Kept | Step |
|---|---|---|---|
| Socket positions | Printed alone on 3 February | The six positions of December, never changed | 21 |
| Snap fit | Several triangle sizes and modular sections | Triangle ridges of 2 and 2.25 mm in grooves of 2.7 mm | 21 |
| Top face | MakerBot Replicator+ | Printed against the bed plate of the Original Prusa MK4S | 21 |
| Thread pitch | 1.5 mm, then 4.5 and 3 mm | 3 mm | 22, 26 |
| Nut | Slop of 0.05 and 0.08, nuts 6.3 to 6.5 mm tall | A square nut 5 mm tall with a slop of 0.11 | 22, 26 |
| D shaft hole | Radius 1.05 to 1.1 mm | Radius 1.21 mm with the flat 0.55 mm from the axis | 22, 26 |
| Button holder | A cylinder with teeth, then a hollow cylinder with grip dots | The threaded cylinder split in two, shortened to 18 mm | 23, 27 |
| Motor casing | A closed tube | A main casing, a detachable half and a clamp ring | 24 |
| Stack height | Taller cap post, piston and split cylinder | All three shortened on 11 and 12 May | 27 |
| Braille top pin | A hard print with a long post | A short post, printed in air TPU | 22, 27 |
| Pi mount | Four posts on the wall | A plate that slides into rails | 28 |
| Computers | ESP32 and Pi | The Pi alone | 30 |
| Wiring order | Fixed in the code | Calibrated from a phone | 31 |

## How this workbook was written
The steps were reconstructed from the project folder and not from a diary. Every dimension comes from an OpenSCAD source file, every print setting from a PrusaSlicer project, every electrical rule from the Pi code, and every date from the time a file was last saved, converted to Toronto time. The folder holds 175 design files, 47 OpenSCAD sources, 123 STL exports and 5 slicer projects, and 77 source files of Pi code and setup app. The images were rendered in OpenSCAD 2021.01 with the BOSL2 library from the same sources at a lower resolution. The views that show parts assembled were rendered again on 10 October 2026, after every part had been placed against its neighbours in OpenSCAD and each pair checked for overlap. No file in the folder holds the assembly, so the place of each part is worked out from its fits, and steps 25 to 27 say how. Parts are coloured orange and blue because those are the filament colours stored in the slicer projects. Where an image contains something that is not in the source files, such as the outline of a Raspberry Pi or a block standing in for the power bank, the caption says so.

What a folder cannot hold is what happened at the bench. Photos, measurements and how the parts felt in the hand are still to be added to these steps. On 3 November 2026 the maker added the order of the work and what failed at the bench, which the front page and steps 20, 21, 23, 27 and 28 now carry, and the Pi code got two steps of its own, 30 and 31.

## Timeline of the files
![[MooMooRedesign_00_file_timeline.png]]
Every design file in the redesign folder by the day it was last saved, grouped by part family. The last row counts source files of the Pi code and the setup app

| Month | Design files saved |
|---|---|
| November 2025 | 11, of which five pin exports belong to the spike, three parts to a clay printer and two files to no project, which leaves the thread test of 2 November |
| December 2025 | 17 |
| January 2026 | 20 |
| February 2026 | 14 |
| March 2026 | 6 |
| April 2026 | 20 |
| May 2026 | 87 |

Reading the whole timeline back, the redesign did not move at an even pace. It moved in six bursts with quiet weeks between them. The casing was drawn over Christmas week. The button stack followed in the first half of January. One long day on 3 February was spent on thread and shaft tests. 3 March split the button holder. 20 to 22 April brought the split motor casing, seven clamp ring exports and the head. Then half of all files in the folder were saved in the eighteen days between 4 and 21 May, when every part was brought into one folder, shortened, loosened or tightened, laid out on print plates and finally given a computer mount and a power bank pocket. The order inside that last burst is worth noticing. The actuator was finished first, then the Pi plate, then the pocket. The design grew from the moving part outward to the wall plug that it no longer needs.

Two habits show up in every burst. When a fit is in doubt, only that feature is printed (six sockets without a shell in step 21, a disc with a D shaped hole in step 22, the post of the cap without the cap in step 22). And when a number changes, the old file stays and the new one gets a name that says what changed (step 25 lists them).

## The twelve steps
- [[20. Return to the pin. From a metal screw to a printed lead screw]]. November and December 2025. A thread test in November, then a parametric actuator with a printed screw and a square nut that replaces the metal screw and nut of the first workbook
- [[21. Three part casing with snap fit tabs and triangle ridges]]. December 2025 to February 2026. Three flat shells of 205 by 140 mm with shared pin positions and a printed snap fit
- [[22. Fit tests for the thread, the nut, the D shaft and the braille cap]]. January and February 2026. Pitch, nut clearance, shaft hole and cap seat are each printed alone
- [[23. Button stack on the moving pin. Lifter, threaded holder, transfer cube and presser]]. January to March 2026. A push button rides on every dot, held by its own thread
- [[24. Splitting the motor casing. Detachable half, clamp ring and a plug in base]]. March to May 2026. The motor becomes removable and the actuator becomes a module with a fixed depth in its socket
- [[25. Character head with an angle key and a round of small print adjustments]]. April and May 2026. The cow head returns on a key with a twist lock, and thirteen single number adjustments are listed
- [[26. Printed lead screw v1 to v5 and the elevator nut]]. May 2026. Ten screw exports in one day, a 3 mm pitch and a looser nut
- [[27. One actuator module as a print set. Shorter piston, split button cylinder and a TPU braille cap]]. May 2026. Twelve printed parts for one dot, nine of them on one plate, and a soft cap
- [[28. Sliding Raspberry Pi plate and motor driver clips in the bottom shell]]. April and May 2026. The Pi moves from four posts on the wall to a plate that slides and clicks
- [[29. Power bank pocket, speaker mounts and the shared 5 V rail]]. May to July 2026. A pocket for the power bank, zip tie mounts for two speakers, and the rules in the Pi code that keep six motors from browning out the computer
- [[30. The Pi without the ESP32. Motor drivers on GPIO, setup over wifi or Bluetooth and the model presets]]. May to July 2026. The Pi drives the dots and reads the buttons by itself, is set up from a phone over its own wifi or Bluetooth, and calls the models itself
- [[31. Pin calibration. Matching each motor and button to its dot]]. May 2026. A wizard on the phone matches each motor and button to its dot and corrects a reversed motor in software

## After the redesign
From November 2026 each day of new work gets its own step, written on the day.
- [[32. Working on the Pi from the Mac. SSH over the home wifi and the Pi code under version control]]. 20 November 2026. The Pi is reached over the home wifi, its installed code is found identical to the copy on the Mac, and that copy is committed to git and pushed to GitHub before anything is changed
- [[33. Building a Moo from a blank SD card. The installer, the three services and the two command line tools]]. Written on 20 November 2026 from the code of May to July 2026. How a fresh Raspberry Pi OS becomes a Moo, what runs on it, and how a finished card is cleaned for copying
- [[34. A computer for Moo in one line. Moo Local installed from the Moo itself and three choices on the AI engine screen]]. 21 November 2026. A Mac installs Moo Local with one line that the Moo hands out, and the AI engine screen is reduced to three choices with all computers in one list
- [[35. This device on a phone. The first run on the iPhone 16 Pro]]. 21 November 2026. The website crashes when the phone is asked to do the AI work, a crash now leaves a trace, and each device chooses its own models
- [[36. The Moo app on iPhone and Android. Models that fit each phone, the Moo's remote and a list of devices]]. 21 November 2026. What a phone browser and the Pi can carry is measured, one app for iPhone and Android becomes the Moo's remote and its AI, five faults of the first stories are fixed on the Moo, and five newer story models are ranked

## What changed since the first workbook
| | First workbook, 2024 to 2025 | Redesign, 2025 to 2026 |
|---|---|---|
| Drive of a dot | Geared DC motor with a metal screw and nut | A 6 mm micro gear motor, 3 V and 60 mA, with a printed screw of 3 mm pitch and a printed square nut |
| End stop | Aluminium foil touch sensor on the ESP32 | Time limit of 1.5 s in the Pi code |
| Motor mount | Closed printed casing | Split casing with a detachable half, a clamp ring and one bolt |
| How a dot sits in the device | Pin holder tray | Square base of 8.1 mm in a socket of 8.45 mm with grip dots and a stopper plate |
| Button | In a holder on top of the pin | In a split threaded cylinder, pressed by a guided piston |
| Braille cap, the braille top pin | Hard print | Air TPU, held on a 5.4 mm post by four bumps |
| Casing | One rounded body with a top tray, second box for electronics | Three flat shells that snap together, electronics inside |
| Computers | ESP32 for the motors and buttons, Raspberry Pi for the voice, joined over UART | The Pi alone, with three TB6612FNG boards on its GPIO |
| Network and key | Written into the code | Entered from a phone over the Pi's own network or Bluetooth, and kept in one file on the Pi |
| Which motor drives which dot | Set in the code | Calibrated from a phone, with a reversed motor corrected in software |
| Motor control | ESP32 over UART from the Pi | Raspberry Pi Zero 2 W directly over GPIO to three TB6612FNG boards |
| Power | Wall supply and cables to a computer | One USB power bank in a pocket on the casing |
| Printer and material | MakerBot Replicator+, PLA | Prusa CORE One and Original Prusa MK4S, PETG and TPU |
| Setup | Monitor, keyboard and mouse on the Pi | Setup app over the device's own wifi hotspot or Bluetooth |
