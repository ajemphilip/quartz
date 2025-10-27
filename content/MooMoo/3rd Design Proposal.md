Date : 2024-07-21

# Tasks : Design a button which is placed on top of the pin.

# Goals
- Design and materialize the pin click prototype to be attached at the top pin

# Description
The current proposal focuses on the deeper functionality of the pin affordances and still examines the way to avoid the pin block. The process will help to bring further understanding of the prototype possibilities and bring closer more optimal solutions. The click function has also be redesigned from the previous proposal to be usable and stable while clicking.

# Prototyping
![[PENUP_20250425_200136 1.jpg]]
Button Casing Sketch
## Pin Click
To enable for user control over the device as well as a form of learning experience the pin has to be interactive. The best way to merge the device control and interactivity is possibly through pin click function. The pin click functionality was designed to created modularly. it consists of a simple button and a casing.

### Button
The button is regular electronic button but its a little bigger then the standard electronic button. Additionally the button top (clicking surface) is enlarged and rectangular so its easier to attach some future pin surface to it.

![[Pasted image 20240805160323.png]]
Comparison between larger button used and regular electronic button

### Casing
The casing is made out of 3 elements:
#### The bottom tray 
##### Image
![[Pasted image 20250411142949.png]]
##### Code
```
module bottomTrayCube () {
    difference(){
    cube([15,20,5],center=true);
    cube([13,18,10],center=true);
    }
    cube([14,5,2],center=true);
    }
    difference () {
    bottomTrayCube ();
    cube([13,1.5,3],center=true);
        }
```
#### The top holder 
##### Image
![[Pasted image 20250411143032.png]]
##### Code
```
  module cap () {
            difference() {
                cube([12.5,17,9],center=true);
            translate([0,0,-2.5])
            cube([15,13,10],center=        true);
            cube([8,8,12],center=        true);
            }
                }
            cap();
```
#### Pin attachment 
##### Image
![[Pasted image 20250411143113.png]]
##### Code
```
module buttonTransfer() {
    difference (){
    cube([5.6,5.6,5.6],center=true);
    translate([0,0,2])
    cube([4.2,4.2,3.9],center=true);
    translate([0,0,-2])
    cube([4.2,4.2,3.9],center=true);
    }
    }
buttonTransfer();
```

# Creating
The button casing was 3D printed. Due to some measurement flaws some prints especially the top holder walls that hold the construction in place were too thin and were breaking apart even upon placing it in between the bottom tray and the button. After some adjustments the button was correctly 3D printed.

![[Pasted image 20240805155937.png]]
The bottom tray that supports the button

![[Pasted image 20240805160032.png]]
The top holder that holds the button in place

![[Pasted image 20240805160216.png]]
Button to pin attachment 
## Print Settings 
| Setting               | Values Used                  |
|------------------------|-------------------------------|
| Layer Height           | 0.2 mm                        |
| Infill Density         | 15%                           |
| Infill Pattern         | Diamond                          |
| Shells (Wall Lines)    | 2                             |
| Top Layers             | 4                             |
| Bottom Layers          | 3                             |
| Print Speed            | 60 mm/s                       |
| Travel Speed           | 90–120 mm/s                   |
| Extruder Temperature (PLA) | 210°C                    |
| Build Plate Temperature| 60°C                          |
| Supports               | None       |
| Raft                   | Enabled        |
| Cooling Fan            | Enabled after 1–2 layers      |
# Cost
| Item      | Description      | Unit Price (CAD) |
|-----------|------------------|------------------|
| Filament  | Per spool        | 14.00            |
| Button    | Per unit         | 0.0392           |
| **Total** |                  | **14.0392**      |

# Critical Reflection
## Pin Click
The pin click approach and its construction work pretty well. The construction is well matched. The only flaw is that when pressed is a bit out of stability because of lack of constraints or any blockade between the top holder and bottom tray. On the other hand, its too early to determine specific the trade-offs related to click functionality in the big system.

https://youtube.com/shorts/9BuN_N1MnDs
Video