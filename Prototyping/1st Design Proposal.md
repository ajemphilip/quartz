Date : 2024-07-07

# Task : Create a first physical pin prototype with casing mechanism

# Goals
- Test usability of prepared casing for assessment of pin movement smoothness and effectiveness with the active DC motor. 
- Test modularity and difficulty of 3D design and printing of the components with more advanced movement approach. 
- Empirical assessment of first 3D printed prototype casing and its materiality
- Assess to what extent 3D printing can be precise to avoid adhesives to assemble the pin/device

# Description
Considering the selected DC motor prototype pin mechanism from the past research I applied the usable casing to start the pin research development process.  The pin in this case uses a screw that is locked with the casing which enables the nut to spin and as a result of that action move the pin up and down.

# Prototyping
The idea was to create a dc motor mechanism and 3D printed casing to test modularity and motoric possibilities of the system. The prototype also suppose to determine the idea of dc motor and screw pin movement solution including smoothness, speed and reveal the problems that might occur during the movement. To visualize the possibilities of the movement 2 sketches has been made.

![[Pin - BottomRail.jpg]]
Pin with the rail hole at the bottom part of the casing

![[Pin - TopRail.jpg]]
Pin with the rail hole at the top part of the casing

With the drawing I determined that top pin element should have long holes (rails) and the bottom should have circular holders (supporters). Two elements connected should give a stable support to move the pin up and down.

To fulfil the functionality of both the previous prototype and current vision the following components were used:
- Screw 
- Nut
- 9V DC Motor

The main idea was to 3D print three separate components to include and assess modular approach to the braille pin. The theoretical questions posted during the prototyping phase were:
- How well and easy can three components match
- Assessment of difficulty of both assemblage and creation of such modular system.

With that said it was also important that parts would match with each other and perform its motoric function so all the necessary selected components in the pin will form a collective system. 
It was crucial especially for the 3d printed "Screw-Motor Converter" to precisely fit the screw and motor on their endings to be relatively stable when spinning.
The motoric assessment includes: 
- smoothness of up/down movement
- speed of up/down movement
- other issues

The purpose of the creation was to physically test dc motor as a main engine to move the pin and to physically feel the general feeling and usability of such system to apply further improvements.

## Creating
The prototyping as 3D models were created in openSCAD and 3D printed with Makerbot replicator+. 
The creation process started with 3D design of the pin. design happened in three portions which were:
- Top Pin Printing 
- Bottom Pin Printing
- Converter Printing
- Assembly of the System

### Materialized Device
![[Pasted image 20240711170126.png]]

### Top pin

Top pin shape was modelled to accommodate the up/down sliding movement with DC motor. The inside nut holder hole was modelled in the nut shape to form a shaft motoric functionality. The holes on the sides suppose to be used as a rails to stop the round movement when slide and locked against bottom pin supporters. The top pin shape gives possibility to slide in the element with the desired braille pin shape to give flexibility for the future evaluations as well as a means of modularity and replicability.
#### Images

![[Pasted image 20240711170019.png]]
Nut holder hole

![[Pasted image 20240711170353.png]]
Supporters and rails

![[Pasted image 20240711170531.png]]
Top square to put braille pin ending

#### Code
```
module mainHolder() {
    rotate([0,180,0])
    difference(){ 

   cylinder (61,17,17,$fn=100);
   translate ([0,0,7])
   cylinder (60,15,15);
}
  }
  
  module elasticBreakLeft() {
     translate([12,0,-35])
     rotate([0,0,90])
     cube([3,10,65],center=true);
      }
      
       module elasticBreakRight() {
     translate([-12,0,-35])
     rotate([0,0,90])
     cube([3,10,65],center=true);
      }
      
  module transferCube() {
     translate([0,0,0])
     cylinder(33,11,5,$fn=100);
      }
        

 module negatePin() {
     cylinder (100,4,4,$fn=100);
     }
     module unionized () {
         union(){
             mainHolder();
     transferCube();}
         }
     difference(){
         unionized();
         translate([0,0,-4])
         cylinder(7,7.5,7.5,$fn=6,center=true);
         cylinder(63,5,5,$fn=100,center=true);
         translate([0,0,0])
         elasticBreakLeft();
         elasticBreakRight();
         }
         translate([0,0,34])
         cube(10,center=true);
```

### Bottom Pin
Bottom pin design accommodate the dc motor socket and railing support. Dc motor socket has little bumps to hold motor in place while spinning. The square bottom was developed for stability and to assess whether the element cab be placed directly into a future exterior casing without adhesives.
#### Image
![[Pasted image 20240711170655.png]]
Motor Socket

#### Code
```
module dcMotorHolder() {
  difference() {
    cylinder(28, 14.5, 14.5, $fn = 100);
    translate([0, 0, 2]) cylinder(28, 12.5, 12.5);
  }
}

module stabilizationPinRight() {
  rotate([90, 0, 0]) translate([0, 24, 13]) cylinder(6, 1.5, 1.5, $fn = 100);
}

module stabilizationPinLeft() {
  rotate([90, 0, 0]) translate([0, 24, -19]) cylinder(6, 1.5, 1.5, $fn = 100);
}

module elasticBreak() {
  translate([10, 0, 29]) rotate([0, 0, 90]) cube([2, 10, 38], center = true);
}
// triangle code taken from https://pyihub.org/triangle-in-openscad/
module supportPrintTriangleLeft() {
  translate([0.5, 13, 18]) rotate([90, -90, -90]) difference() {
    // creating a cube
    cube([5, 5, 1]);
    // rotating the cube
    translate([0, 0, -0.2]) {
      rotate([0, 0, 45]) {
        cube([11, 11, 3]);
      }
    }
  }
}
// triangle code taken from https://pyihub.org/triangle-in-openscad/
module supportPrintTriangleRight() {
  translate([-0.5, -13, 18]) rotate([90, -90, 90]) difference() {
    // creating a cube
    cube([5, 5, 1]);
    // rotating the cube
    translate([0, 0, -0.2]) {
      rotate([0, 0, 45]) {
        cube([11, 11, 3]);
      }
    }
  }
}

module holeBottom() {
  rotate([0, 0, 0]) translate([10, 0, -2]) cylinder(10, 3, 3, $fn = 100);
  rotate([0, 0, 0]) translate([-10, 0, -2]) cylinder(10, 3, 3, $fn = 100);
}

module squareHolder() {
  translate([0, 0, 1.5]) cube([50, 50, 5], center = true);
}

module sphereHolders() {
  translate([0, 12, 20]) sphere(r = 1);

  translate([0, -12, 20]) sphere(r = 1);

  translate([-12, 0, 20]) sphere(r = 1);

  translate([0, 25, 1.5]) sphere(r = 1);
  translate([-25, 0, 1.5]) sphere(r = 1);
  translate([0, -25, 1.5]) sphere(r = 1);
  translate([25, 0, 1.5]) sphere(r = 1);
}

stabilizationPinLeft();
stabilizationPinRight();
supportPrintTriangleLeft();
supportPrintTriangleRight();
sphereHolders();
difference() {
  union() {
    dcMotorHolder();
    squareHolder();
  }
  elasticBreak();
  holeBottom();
}
```

### Converter
Converter was created to match the endings of the dc motor and screw to form a shaft mechanism. The screw by rotating move the nut up or down and the converter passes the torque from the dc motor pin to the screw. It was important to aim for movement stability of the system.
#### Images
![[Pasted image 20240711171215.png]]
Converter
![[Pasted image 20240711170846.png]]
Shaft Mechanism

#### Code
```
module converterTop() {
    difference(){
    cylinder(15,10,10,$fn=6,center=true);
    translate([0,0,11])
    cylinder(24,7.5,7.5,$fn=6,center=true);
    }}

difference(){
    converterTop();
    translate([0,0,-5.1])
    cylinder(6,3.2,3.2,$fn=20,center=true);
}
```
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
| Supports               | None      |
| Raft                   | Enabled         |
| Cooling Fan            | Enabled after 1–2 layers      |
# Cost
| Item             | Description          | Unit Price (CAD) |
|------------------|----------------------|------------------|
| DC Motor (9V)        | 9V motor              | 4.13             |
| Filament         | Per spool             | 14.00            |
| Screw and Nut (M5)    | Per unit              | 0.1155           |
| Arduino Uno      | Microcontroller       | 39.75            |
| **Total**        |                      | **57.9955**      |
# Critical Reflection
 The pin project is generally usable but there are some cons that has to be addressed in the future iterations. To answer the questions posted Ill address them separately by considering technological/material matters in the area of focus.
 
## Casing
The 3D printed casing was physically assessed and matched the expectations but require some adjustments regarding the printed parts to be done. 

**Cons:**
- Because of lack of precise measurement tools some parts, especially converter, are not precisely done what results in some discrepancies while the pin moves.
- Issue encountered during the printing is the wall thickness - sometimes it was too thin and was breaking off what posts important questions about durability of the system. 
- When not measured precisely too thick dc motor socket was breaking up or not fitting the motor at all. 
- The pin casing is quite tall what might bring the problem of device size

**Pros:**
- Generally the setup is easy to assemble just by sliding the elements therefore, modularity in the domain of replicability is met. All elements match well.
- The elements can be easily 3D printed and altered according to the needs
- There is no need to use adhesives to assemble the system - all parts hold quite firmly when assembled
- Creation with 3D printing or rapid prototyping tools is quite easy 
- Case railing/supporters don't block the up/down movement
Generally 3 piece modular design seems to be quite reliable and ready for further community members adjustment. The casing after couple prints was reliable as early pin prototype but require to address the cons. 

![[Pasted image 20240711171837.png]]

## Movement
The dc motor with the screw shaft and converter works well. The elements fit well and perform its function but there has to be further adjustment to be made to avoid screw-nut blocks.

**Cons**
- The movement range is only 3.5cm which might be not sufficient to haptically present the movement
- The screw because of motor speed at the boundaries sometime blocks or unplug the top pin
**Pros**
- The motor reliably move pin up/down
- Motor in a very quick time manner move the pin
- Smoothness is good and motor has the strength to perform its action

Generally minor adjustments are to be made to make the movement reliable. 

To conclude the modularity is well done with some additional function to be added in the next iteration. The casing is quite durable and after adjustments and additions should perform its action well. The movement is rapid but smooth. In general the pin feels firm and well done as well as uncomplicated to assemble/build/adjust. 
It's a good start to assemble a braille pin in an assistive device and form a reliable system to present a braille letter concept to early learners. Generally the pin built seems a bit engineering like but does have the room for adjustment because of early posted solutions and modularity. Its difficult to address other question written in the proposal at this stage. 

# References
_Make a Triangle in OpenSCAD Using Various Methods_. (n.d.). Retrieved April 26, 2025, from [https://pyihub.org/triangle-in-openscad/](https://pyihub.org/triangle-in-openscad/)