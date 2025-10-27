Date : 2024-08-12

# Tasks : Entry Prototype of entire exterior casing

# Goals
- Design the exterior casing of the device as well as means of assembly of such casing
- Design a pin according to the braille standards

# Description
The current design proposal visualizes shape of the device. There are multiple things to consider while designing an exterior casing such as usability, general shape, durability and safety which will be taken into account while creating device.

# Prototyping
The early sketch was created to visualize the casing: 
![[PENUP_20250425_200018.jpg]]
Casing Compartment Sketch

The usability of the device suppose to bring comfort of interaction to the user. The parts especially the top pins suppose to be easily identifiable and well articulated whether they are up or down. 
The casing in general suppose to be durable to be able to hold some degree of more intense usage. Because of that the walls of the device has been made thicker to withstand some degree of regular use wearing. 
To address haptic cognition as well as safety the corners and edges of the devices has been rounded. That ensures that there aren't any sharp surfaces but also improve haptic recognition and centers focus only on the pins which have sharp edges. 
Because of the printing time of one piece (~30h) and modularity considerations the casing was divided into 3 pieces: 
- Top Cover
- Middle Cover
- Pin Holder Tray
- Bottom Cover

To accommodate the casing requirements connected with pin tray the following diagram was created: 
IMAGE

## Top Cover
Top casing function is to provide a socket (opening hole) for the braille pin. Considering pin design both top surface of the casing and flat surface of the braille pin suppose form a flat surface. Through the holes the braille pin will move up and down according the the braille symbol requirements. 
### Image
![[Pasted image 20240829204824.png]]
### Code
```
module topSuface () {
    minkowski() {
    translate([0,0,100])
    cube([185,120,100],center=true);
    sphere(10,$fn=20);
   }
}

module holes () {
translate([0,32.5,15])
cylinder(35,22,22,center=true);
translate([0,-32.5,15])
cylinder(35,22,22,center=true);
translate([-65,-32.5,15])
cylinder(35,22,22,center=true);
translate([-65,32.5,15])
cylinder(35,22,22,center=true);
translate([65,32.5,15])
cylinder(35,22,22,center=true);
translate([65,-32.5,15])
cylinder(35,22,22,center=true);
}
    
module main () {
difference() {
cube([185,120,5],center=true); 
cube([180,115,10],center=true);
    }
}

 module differenceCube () {
         translate([0,0,80])
         difference(){
         cube([210,140,100],center=true);
         translate([0,0,46])
         difference(){
         cube([211,141,10],center=true);
         cube([190,122,10],center=true);
        }
    }
}
      
minkowski() {
       difference() {
       topSuface();
       translate([0,0,31])
       main();
       differenceCube();
       translate([0,0,150])
       holes();
       translate([0,0,84])
       cube([180,115,141],center=true);
       translate([0,0,-22])
       cube([300,300,105],center=true); 
        }   
    }

```
## Middle Cover
Because of the device modularity the middle part of the casing acts like a connector between top and bottom cover. The division was done to divide the printing time and give modular possibilities to adjust height in case of different electronic parts or alternative design.
### Image
![[Pasted image 20240829201842.png]]
### Code
```
module topSuface () {
    minkowski() {
    translate([0,0,100])
    cube([185,120,141],center=true);
    sphere(10,$fn=20);
    }}
 
module main () {
    difference() {
  cube([185,120,5],center=true); 
  cube([180,115,10],center=true);
}}

 module differenceCube () {
     translate([0,0,-200])
     difference(){
         cube([210,140,110],center=true);
         translate([0,0,50])
         cube([192,124,13],center=true);
         }
     }
module screwHoles () {
           translate([93,-62,30])
       cylinder(30,3.55,3.55);
       translate([93,62,30])
       cylinder(30,3.55,3.55);
       translate([-93,62,30])
       cylinder(30,3.55,3.55);
       translate([-93,-62,30])
       cylinder(30,3.55,3.55);
    }
    
minkowski() {
       difference() {
       topSuface();
       translate([0,0,31])
       main();
       rotate([0,180,0])
       translate([0,0,70])
       differenceCube();
       screwHoles();
       //delete top part
       translate([0,0,100])
       cube([180,115,141],center=true);
       translate([0,0,-22])
       cube([300,300,105],center=true);
        }   
    }

```
## Pin Holder Tray
The pin holder tray was created in the previous iteration to give socket like tight support to the pin as well as it has dimensions according to real paper embossed braille pin ratio. The research is to be found here: [[2nd Design Proposal - Pin Research#Pin Holder Tray]]
## Bottom Cover
The bottom cover should act as the support of the entire physical device structure. It will provide stability to the entire system as well as in the future iterations will hold electronic components of the system.
### Image
![[Pasted image 20240829205340.png]]
### Code
```
module topSuface () {
    minkowski() {
    translate([0,0,100])
    cube([185,120,38],center=true);
    sphere(10,$fn=20);
    }}

module main () {
  difference() {
  cube([188,123,5],center=true); 
  cube([180,115,10],center=true);
}}

module legs() {
    translate([-87,-52,125])
    cylinder(7,3.55,3.55);
    translate([-87,52,125])
    cylinder(7,3.55,3.55);
    translate([87,-52,125])
    cylinder(7,3.55,3.55);
    translate([87,52,125])
    cylinder(7,3.55,3.55);
}

module screwHoles () {
       translate([93,-62,80])
       cylinder(70,3.55,3.55);
       translate([93,62,80])
       cylinder(70,3.55,3.55);
       translate([-93,62,80])
       cylinder(70,3.55,3.55);
       translate([-93,-62,80])
       cylinder(70,3.55,3.55);
}
    
minkowski() {
       difference() {
       topSuface();
       legs();
       translate([0,0,88])
       main(); 
       screwHoles();
       translate([0,0,97])
       cube([182,117,50],center=true);
       translate([0,0,34])
       cube([300,300,105],center=true); 
        }
    }
```
# Creating
The elements were 3D printed with Makerbot Replicator+ and photographed to reflect on the physical traits.
Images of casing:
## Bottom Cover
![[IMG_6687.jpg]]
## Top Cover
![[IMG_6692.jpg]]
## Middle Cover
![[IMG_6691.jpg]]
## Assembled Setup
![[IMG_6870.jpg]]
## Print Settings 
| Setting               | Values Used                  |
|------------------------|-------------------------------|
| Layer Height           | 0.2 mm                        |
| Infill Density         | 30%                           |
| Infill Pattern         | Grid                          |
| Shells (Wall Lines)    | 2                             |
| Top Layers             | 4                             |
| Bottom Layers          | 3                             |
| Print Speed            | 60 mm/s                       |
| Travel Speed           | 90–120 mm/s                   |
| Extruder Temperature (PLA) | 210°C                    |
| Build Plate Temperature| 60°C                          |
| Supports               | None     |
| Raft                   | Enabled       |
| Cooling Fan            | Enabled after 1–2 layers      |
# Cost
| Item      | Description  | Unit Price (CAD) |
|-----------|--------------|------------------|
| Filament  | Per spool    | 14.00            |
| **Total** |              | **14.00**        |
# Critical Reflection
Despite minor measurement errors and manual adjustments during assembly, the casing prototype was successfully printed and assembled. A notable drawback is its excessive height, mainly stemming from the thickness of the bottom Cover; reducing this could lower the device's height by about 4cm. Furthermore, the pin holder tray design is redundant, as the pins should be positioned at the bottom of the cover. This adjustment would not only further reduce the device height by 2-3cm but also create a more efficient layout for the electronic components, thereby saving space.The middle section effectively connects the top and bottom cover parts, providing some options for adjustment.The top section is also well-crafted with no flaws.

