Date : 2025-01-19

# Tasks : Additional Compartment for Electronics.

# Goals
- Print Additional Electronic components compartment
- Develop Cable Blocker to hold cables

# Description
The proposal focuses on final device tweaks that gravitates around matters that are supporting the structure of the final design and its components. Generally the electronic components and pins suppose to be held in the singular device casing however because of the their volume due to wiring the additional compartment had to be created. Because of that, the wires between compartments had to be secured in the case of device relocation with additional component.
# Prototyping
![[PENUP_20250425_200657.jpg]]
Cable Blocker Sketch

The idea behind the blocker was to accommodate the cable hole to pin the cables in-between the hole and holder to keep them in place. It should be intact by the holders on the side and special square railing on the top to attach to the casing.
## Cable Blocker
### Code
```
module radiusModule() {
  difference() {
    cylinder(h = 20, r = 20, $fn = 100);
    cylinder(h = 50, r = 15, $fn = 100, center = true);
  }
}

module holderOpening() {
  cylinder(h = 23, r = 18, $fn = 100);
}

module holderHole() {
  cylinder(h = 50, r = 9, $fn = 100, center = true);
}

module blockTrim() {
  cube([11, 30, 50], center = true);
}

module blockTrimBottom() {
  cube([11, 30, 50], center = true);
}

module blockTrimInside() {
  cube([13, 35, 5.5], center = true);
}

module grip() {
  translate([0, 14.5, 21]) rotate([0, 90, 0]) cylinder(h = 2, r = 4, $fn = 3);

  translate([0, -14.5, 21]) rotate([0, 90, 0]) cylinder(h = 2, r = 4, $fn = 3);
}

difference() {
  holderOpening();
  translate([17, 0, 8]) blockTrim();
  translate([0, 0, 8]) radiusModule();
  holderHole();
  translate([5.6, 0, 16.25]) blockTrimInside();
  translate([-15.5, 0, 16.25]) blockTrimBottom();
}
translate([-15, 0, 0]) ropeHolder();
grip();
```
### Images
![[Pasted image 20250418143224.png]]

## Additional Electronic Compartment
The additional electronic compartment is the same as the large version in the proposal [[12th Design Proposal]] and [[11th Design Proposal]]. The only difference is the top casing where there are no pin holes.  Every component was scaled down to 70%.

### Modified Top Casing
```
module topSuface() {
  minkowski() {
    translate([0, 0, 100]) cube([185, 120, 100], center = true);
    sphere(10, $fn = 20);
  }
}

module frontShapeHolderHole() {
  translate([-98, 0, 138]) cube(10, center = true);
}

module backShapeHolderHole() {
  translate([98, 0, 138]) cube(10, center = true);
}

module GripDots() {
  // side dots
  translate([99, 0, 125]) sphere(1);
  translate([-99, 0, 125]) sphere(1);
  // other dots
  translate([0, 65.1, 125]) sphere(1);
  translate([0, -65.1, 125]) sphere(1);

  // attachement cube dots
  translate([99, 0, 143.5]) sphere(1);
  translate([99, 0, 133]) sphere(1);
  translate([99, 5, 138]) sphere(1);
  translate([99, -5, 138]) sphere(1);

  // attachement cube other side
  translate([-99, 0, 143.5]) sphere(1);
  translate([-99, 0, 133]) sphere(1);
  translate([-99, 5, 138]) sphere(1);
  translate([-99, -5, 138]) sphere(1);
}

module main() {
  difference() {
    cube([20, 120, 5], center = true);
    cube([40, 115, 10], center = true);
  }
}

module differenceCube() {
  // outer rectangle
  translate([0, 0, 80]) difference() {
    cube([215, 142, 100], center = true);
    translate([0, 0, 46])
        // inner ring in the rectangle
        difference() {
      cube([215, 151, 10], center = true);
      cube([198, 131, 10], center = true);
    }
  }
}

GripDots();
holeSupport();
minkowski() {
  difference() {
    topSuface();
    translate([0, 0, 31]) main();
    differenceCube();
    translate([0, 0, 150]) holes();
    translate([0, 0, 84]) cube([191, 125, 141], center = true);
    translate([0, 0, -22]) cube([300, 300, 105], center = true);
    frontShapeHolderHole();
    backShapeHolderHole();
  }
}
```
# Creating
The device was assembled and cables were additionally secured with the net around the circumference. To accommodate holes for other cables that need to be attached to the computer, the soldering iron was used to melt the plastic. 
![[IMG_6873.jpg]]
Cable Blocker Part

![[IMG_6872.jpg]]
Cable Blocker Attached

## Print Settings 
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
# Critical Reflection
![[Pasted image 20250425162710.png]]
Additional Electronic Compartment

The cables stay intact and they are firmly attached to the larger device. Because of the size of the smaller device the cables are generally tight around the cable hole therefore there were not need to additional holder. Smaller compartment is not attached firmly possibly because of the size of the element however it performs its action. 
