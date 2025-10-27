Date : 2024-10-20

# Tasks : Creative Presentation of Device Orientation and Device Casing Adjustments

# Goals
- Create modular system to attach printed items to front and back of the device
- Create head and tails shapes to creatively indicate device orientation

# Description
The design proposal introduces the modification of the braille device with additional functionality that will serve to identify front and back of the device. Its was identified, since braille pin is symmetrical, to indicate front and back to avoid confusion and teach braille letters with clarity for the users. 

# Prototyping
![[PENUP_20250425_200547.jpg]]
Head and Tail Sketch

The modifications changed only top tray to have hole in front and at the back of the tray to accommodate modular attachment of the head. Due to children interest, generally low difficulty of the creation and to match the device theme, the device imitate the cow and the head shape is formed as rectangular. The tail is also simple curved line significantly smaller in size to emphasize in the top and bottom difference.
## Top Tray
### Image
![[Pasted image 20250411213653.png]]
### Code
```
module topSuface () {
    minkowski() {
    translate([0,0,100])
    cube([185,120,100],center=true);
    sphere(10,$fn=20);
   }
}

module frontShapeHolderHole() {
    translate([-98,0,138])
    cube(10,center=true);
    }
    
module backShapeHolderHole () {
    translate([98,0,138])
    cube(10,center=true);
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

module holeSupport() {
    difference() {
    translate([0,32.5,152.4])
    cylinder(15,22.5,22.5,center=true);
    translate([0,32.5,152.4])
    cylinder(16,20.5,20.5,center=true);
}

    difference() {
    translate([0,-32.5,152.4])
    cylinder(15,22.5,22.5,center=true);
    translate([0,-32.5,152.4])
    cylinder(16,20.5,20.5,center=true);
  }
  
  difference() {
  translate([-65,-32.5,152.4])
  cylinder(15,22.5,22.5,center=true);
  translate([-65,-32.5,152.4])
  cylinder(16,20.5,20.5,center=true);
    }
    
  difference() {
  translate([65,-32.5,152.4])
  cylinder(15,22.5,22.5,center=true);
  translate([65,-32.5,152.4])
  cylinder(16,20.5,20.5,center=true);
    }
    
  difference() {
  translate([65,-32.5,152.4])
  cylinder(15,22.5,22.5,center=true);
  translate([65,-32.5,152.4])
  cylinder(16,20.5,20.5,center=true);
    }
    
  difference() {
  translate([-65,32.5,152.4])
  cylinder(15,22.5,22.5,center=true);
  translate([-65,32.5,152.4])
  cylinder(16,20.5,20.5,center=true);
    }
    
     difference() {
  translate([65,32.5,152.4])
  cylinder(15,22.5,22.5,center=true);
  translate([65,32.5,152.4])
  cylinder(16,20.5,20.5,center=true);
    }
}

module GripDots() {
    //side dots
    translate([99,0,125])
    sphere(1);
    translate([-99,0,125])
    sphere(1);
    //other dots
    translate([0,65.1,125])
    sphere(1);
    translate([0,-65.1,125])
    sphere(1);
    
    //attachement cube dots
    translate([99,0,143.5])
    sphere(1);
    translate([99,0,133])
    sphere(1);
    translate([99,5,138])
    sphere(1);
    translate([99,-5,138])
    sphere(1);
    
    //attachement cube other side
    translate([-99,0,143.5])
    sphere(1);
    translate([-99,0,133])
    sphere(1);
    translate([-99,5,138])
    sphere(1);
    translate([-99,-5,138])
    sphere(1);
    }
    
module main () {
difference() {
cube([20,120,5],center=true); 
cube([40,115,10],center=true);
    }
}

 module differenceCube () {
         //outer rectangle
         translate([0,0,80])
         difference(){
         cube([215,142,100],center=true);
         translate([0,0,46])
         // inner ring in the rectangle
         difference(){
         cube([215,151,10],center=true);
         cube([198,131,10],center=true);
        }
    }
}

GripDots();
holeSupport();
minkowski() {
       
       difference() {
       topSuface();
       translate([0,0,31])
       main();
       differenceCube();
       translate([0,0,150])
       holes();
       translate([0,0,84])
       cube([191,125,141],center=true);
       translate([0,0,-22])
       cube([300,300,105],center=true); 
       frontShapeHolderHole();
       backShapeHolderHole();
        }   
    }
```
## Head Holder
### Image
![[Pasted image 20250411212047.png]]
### Code
```
module cubeHolder () {
    cube([9.5,9.5,25],center=true);
    }  
 module supportBar() {
     translate([0,6,11.5])
     cube([5,4,2],center=true);
     }
cubeHolder();
supportBar();
```
## Head Shape
### Image
![[Pasted image 20250411211941.png]]
### Code
```
module head () {
    cube([60,80,70],center=true);
    }
    
    module cubeHolder () {
        translate([0,-1,0])
    cube([10.8,13,25],center=true);
    }  
    
 module supportBar() {
     translate([0,7,11])
     cube([5,4,3],center=true);
     }
     
module mouth () {
    //topmouth
    translate([38,0,-5])
    cube([1,30,1],center=true);
    //side mouth 
    //left
    translate([38,-25,-20])
    rotate([90,0,0])
    cube([1,15,1],center=true);
    //right 
    translate([38,25,-20])
    rotate([90,0,0])
    cube([1,15,1],center=true);
    //mainmouth
    translate([45,0,-20])
    cube([10,35,18],center=true);
    }
    
module eyes () {
    //right eye
    translate([40,25,15])
    cube([5,30,20],center=true);
    translate([40,30,15])
    sphere(6);
    
    //left eye
    translate([40,-25,15])
    cube([5,30,20],center=true);
    translate([40,-30,15])
    sphere(6);
    }
    
module nostrils() {
    //left nostril
    translate([59,8,-19])
    cube([3,10,10]);
    
    //right nostril
    translate([59,-16,-19])
    cube([3,10,10]);
    }
    
module ear () {
    translate([100,10,10])
    cylinder(20,10,5,center=true);
    rotate([180,0,0])
    translate([100,-10,10])
    cylinder(20,10,5,center=true);
    }
    
difference () {

minkowski (){
head();
sphere(10,$fn=20);
}
translate([-40,0,5])
rotate([90,0,90])
{
cubeHolder();
supportBar();
}
}
    
minkowski () {
   mouth();
   sphere(10,$fn=20);
}

eyes();
translate([-100,50,0])
rotate([45,0,0])
ear();

translate([-100,-65,10])
rotate([-45,0,0])
ear();

translate([20,30,50])
cylinder(30,10,5,center=true);

translate([20,-30,50])
cylinder(30,10,5,center=true);

nostrils();
```
## Tail
### Image
![[Pasted image 20250411211837.png]]
### Code
```
//Taken From:   https://raphaelluckom.com/posts/bezier_curves.html
module piecewise_join(points) {
  for (n=[1:len(points) - 2]) {
    hull() {
      translate(points[n-1]) children(0);
      translate(points[n]) children(0);
    }
    hull() {
      translate(points[n+1]) children(0);
      translate(points[n]) children(0);
    }
  }
}

sphere_points = [
   [-1,0,-20],
  [0,20,0],
  [3,40,0],
  [7, 50, 0]
];
piecewise_join(sphere_points) sphere(3);

module mount() {
    translate([0,10,-15])
    cube([9.5,9.5,10],center=true);
    }
    
module tailEnd () {
    translate([-93,75,-10])
    rotate([90,0,0])
    {
    translate([100,10,10])
    cylinder(30,10,5,center=true);
    rotate([180,0,0])
    translate([100,-10,20])
    cylinder(30,10,5,center=true);
    }
    }
    
tailEnd();
translate([0,-12,-10])
mount();
```
# Creating
All the elements were 3D printed and assembled together. Middle cover was printed using transparent filament twice with different print settings.

![[IMG_6718.jpg]]
Head Holder Attachment

![[IMG_6716.jpg]]
Cow Head

![[IMG_6717.jpg]]
Tail Attachment

![[Pasted image 20250411214440.png]]
Full Device

## Print Settings 
### Regular Print
| Setting               | Values Used                  |
|------------------------|-------------------------------|
| Layer Height           | 0.2 mm                        |
| Infill Density         | 30%                           |
| Infill Pattern         | Linear                          |
| Shells (Wall Lines)    | 5                             |
| Top Layers             | 4                             |
| Bottom Layers          | 3                             |
| Print Speed            | 60 mm/s                       |
| Travel Speed           | 90–120 mm/s                   |
| Extruder Temperature (PLA) | 210°C                    |
| Build Plate Temperature| 60°C                          |
| Supports               | Enabled     |
| Raft                   | Raft + Brim       |
| Cooling Fan            | Enabled after 1–2 layers      |
# Cost
| Item      | Quantity | Unit Price (CAD) | Total (CAD) |
|-----------|----------|------------------|-------------|
| Filament  | 3 spools  | 14.00             | 42.00       |
# Critical Reflection
The shapes attach to the holder and tray very well. Despite they move and feel a bit unstable when the device is moved they offer apparent difference between back and front. The shapes and details are well articulated haptically making them feelable by touch.

# References
_Organic Parametric Shapes: Bézier Curves in OpenSCAD_. (n.d.). Retrieved April 26, 2025, from [https://raphaelluckom.com/posts/bezier_curves.html](https://raphaelluckom.com/posts/bezier_curves.html)