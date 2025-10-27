Date : 2024-09-22

# Tasks : Small two pin device assembly and comfort of use considering functionality, buttons and up/down movement

# Goals
- Design Small Compact casing with 2 pins to understand the casing and device empirically
- Design new bottom cover pin attachment method

# Description
The proposal aim is to create a working prototype to test the general usability of the minimal prototype of the device to test the feeling of the minor device prototype. The aim would be to test physical casing with working pins attached to understand significance and follow up with possible flaws of the casing, buttons and motors in the mini device. Bottom cover was also redesigned to put the pins directly at the bottom on the cover not on the additional tray on top of it. 

# Prototyping

## Casing
The casing was designed to contain 2 modular pins, modular casing. The driver of the pins were put as two 1:50 motors Arduino Uno board and TB6612FNG motor, 2 buttons (small button with red cap) connected with cables.
### Top Cover
The only modification, despite the smaller size, from the previous design was that the silo for the pin casing has deeper printed supports which should provide more stable vertical movement. The braille cap will have enough support both while moving and with the click functionality.
#### Images
![[Pasted image 20250401153327.png]]
#### Code:
```
module topSuface() {
  minkowski() {
    translate([0, 0, 100]) cube([50, 120, 100], center = true);
    sphere(10, $fn = 20);
  }
}

module holes() {
  translate([0, 32.5, 15]) cylinder(35, 22, 22, center = true);
  translate([0, -32.5, 15]) cylinder(35, 22, 22, center = true);
}

module holeSupport() {
  difference() {
    translate([0, 32.5, 152.4]) cylinder(15, 22.5, 22.5, center = true);
    translate([0, 32.5, 152.4]) cylinder(16, 20.5, 20.5, center = true);
  }

  difference() {
    translate([0, -32.5, 152.4]) cylinder(15, 22.5, 22.5, center = true);
    translate([0, -32.5, 152.4]) cylinder(16, 20.5, 20.5, center = true);
  }
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
    cube([80, 142, 100], center = true);
    translate([0, 0, 46])
        // inner ring in the rectangle
        difference() {
      cube([78, 151, 10], center = true);
      cube([61, 131, 10], center = true);
    }
  }
}

holeSupport();
minkowski() {

  difference() {
    topSuface();
    translate([0, 0, 31]) main();
    differenceCube();
    translate([0, 0, 150]) holes();
    translate([0, 0, 84]) cube([55, 125, 141], center = true);
    translate([0, 0, -22]) cube([300, 300, 105], center = true);
  }
}
```
### Middle Cover
#### Images
![[Pasted image 20250401153410.png]]
#### Code: 
```
module topSuface() {
  minkowski() {
    // cube([69.5,139,60.5],center=true);
    cube([50, 120, 60.5], center = true);
    sphere(10, $fn = 20);
  }
}

module middleHole() { cube([54.18, 123.68, 100], center = true); }

module innerMerger() {
  translate([0, 0, 31]) cube([59.5, 129.5, 10], center = true);
  translate([0, 0, -31]) cube([59.5, 129.5, 10], center = true);
}

module differenceCubeTop() { cube([54.1, 124.1, 60.5], center = true); }
module flateresCubes() {
  translate([0, 0, 38]) cube([70, 140, 12], center = true);
  translate([0, 0, -38]) cube([70, 140, 12], center = true);
}

difference() {
  topSuface();
  middleHole();
  differenceCubeTop();
  flateresCubes();
}
difference() {
  innerMerger();
  middleHole();
}
```
### Bottom Cover
#### Images
![[Pasted image 20250401153502.png]]
#### Code: 
```
module topSuface() {
  minkowski() {
    translate([0, 0, 100]) cube([50, 120, 100], center = true);
    sphere(10, $fn = 20);
  }
}

module main() {
  difference() {
    cube([20, 120, 5], center = true);
    cube([40, 115, 10], center = true);
  }
}

module pinHoles() {
  translate([0, 32.5, 0]) cube([8.2, 8.2, 100], center = true);
  translate([0, -32.5, 0]) cube([8.2, 8.2, 100], center = true);

  translate([0, 22, 0]) cube([6, 6, 100], center = true);
  translate([0, -22, 0]) cube([6, 6, 100], center = true);
}

module pinSupports() {
  difference() {
    translate([0, 32.5, 152]) cube([10.2, 10.2, 10], center = true);
    translate([0, 32.5, 152]) cube([8.2, 8.2, 12], center = true);
  }

  difference() {
    translate([0, -32.5, 152]) cube([10.2, 10.2, 10], center = true);
    translate([0, -32.5, 152]) cube([8.2, 8.2, 12], center = true);
  }
}

module differenceCube() {
  // outer rectangle
  translate([0, 0, 80]) difference() {
    cube([80, 142, 100], center = true);
    translate([0, 0, 46])
        // inner ring in the rectangle
        difference() {
      cube([78, 151, 10], center = true);
      cube([61, 131, 10], center = true);
    }
  }
}

pinSupports();
minkowski() {
  difference() {
    topSuface();
    translate([0, 0, 31]) main();
    translate([0, 0, 120]) pinHoles();
    differenceCube();
    translate([0, 0, 84]) cube([55, 125, 141], center = true);
    translate([0, 0, -22]) cube([300, 300, 105], center = true);
  }
}
```
## Electronics
The electronics used the TB6612FNG Motor Controller, Arduino Uno board and 1:30 and 1:50 N10 motors.
### Code
```
//Button Pins
int buttonPinOne = 9;
int buttonPinTwo = 10;
int Stby = 11;

//Motor A
int pwmA = 4;
int in1A = 5;
int in2A = 3;

// Motor B
int pwmB = 6;
int in1B = 7;
int in2B = 8;

//Button States
int buttonStateOne = 0;
int buttonStateTwo = 0;

//TopStateTiming
int pinOneTopState = 0;
int pinTwoTopState = 0;

//Constants
int TIME_VALUE = 2000;

// Motor Speed Values - Start at zero
int MotorSpeedA = 0;
int MotorSpeedB = 0;

void setup() {

  Serial.begin(9600);

  //Motor A setup

  pinMode(pwmA, OUTPUT);
  pinMode(in1A, OUTPUT);
  pinMode(in2A, OUTPUT);

  //Motor B setup

  pinMode(pwmB, OUTPUT);
  pinMode(in1B, OUTPUT);
  pinMode(in2B, OUTPUT);



  //Button pins setup

  pinMode(buttonPinOne, INPUT);
  pinMode(buttonPinTwo, INPUT);



  //Digital Write since button have 2 pins only

  digitalWrite(buttonPinOne, HIGH);
  digitalWrite(buttonPinTwo, HIGH);
}

void loop() {

  // button States
  buttonStateOne = digitalRead(buttonPinOne);
  buttonStateTwo = digitalRead(buttonPinTwo);

  if (buttonStateOne == 0) {
    // Button One and Motor One Code
    if (pinOneTopState == 0) {
      Serial.print("PRESSED ONE");
      digitalWrite(in1A, LOW);
      digitalWrite(in2A, HIGH);
      MotorSpeedA = 255;
      digitalWrite(pwmA, MotorSpeedA);
      delay(TIME_VALUE);
      MotorSpeedA = 0;
      digitalWrite(pwmA, MotorSpeedA);
      pinOneTopState = 1;

    }

    else {
      Serial.print("CLICKED ONE");
      digitalWrite(in1A, HIGH);
      digitalWrite(in2A, LOW);
      MotorSpeedA = 255;
      digitalWrite(pwmA, MotorSpeedA);
      delay(TIME_VALUE);
      MotorSpeedA = 0;
      digitalWrite(pwmA, MotorSpeedA);
      pinOneTopState = 0;
    }
  }


  //Button Two and Motor Two Code
  if (buttonStateTwo == LOW) {
    if (pinTwoTopState == 0) {
      Serial.print("PRESSED TWO");
      digitalWrite(in1B, LOW);
      digitalWrite(in2B, HIGH);
      MotorSpeedB = 255;
      digitalWrite(pwmB, MotorSpeedB);
      delay(TIME_VALUE);
      MotorSpeedB = 0;
      digitalWrite(pwmB, MotorSpeedB);
      pinTwoTopState = 1;

    }

    else {
      Serial.print("CLICKED");
      digitalWrite(in1B, HIGH);
      digitalWrite(in2B, LOW);
      MotorSpeedB = 255;
      digitalWrite(pwmB, MotorSpeedB);
      delay(TIME_VALUE);
      MotorSpeedB = 0;
      digitalWrite(pwmB, MotorSpeedB);
      pinTwoTopState = 0;
    }
  }
}
```
# Creating
## 3D Printing
The casing module was 3d printed, assembled and empirically tested.
The braille pins including pins casings, braille caps and buttons were taken from the previous design. 
![[IMG_4555.jpg]]
Mini Casing With Pins

![[IMG_4558.jpg]]
Mini Casing Top and Bottom Casings

![[IMG_4557.jpg]]
Mini Casing Components

![[IMG_4552.jpg]]
Braille Caps

![[Pasted image 20250413233045.png]]
Mini Casing Entire Device

## Diagram
The electronics were connected according to this diagram:
![[Arduino 2 Motors - Diagram 2 2.png]]
## Print Settings 
| Setting               | Values Used                  |
|------------------------|-------------------------------|
| Layer Height           | 0.2 mm                        |
| Infill Density         | 30%                           |
| Infill Pattern         | Diamond                          |
| Shells (Wall Lines)    | 5                             |
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
| Item              | Quantity | Unit Price (CAD) | Total (CAD) |
|-------------------|----------|------------------|-------------|
| Screw (M5)            | 2        | 0.1155           | 0.231       |
| Motor (N10)            | 2        | 3.48             | 6.96        |
| Motor Controller (TB6612FNG)  | 1        | 0.72             | 0.72        |
| Arduino Uno       | 1        | 39.75            | 39.75       |
| Filament          | 1        | 14.00            | 14.00       |
| Button (Smaller Green Cap Button)   | 1        | 0.386            | 0.386       |
| Button (Smaller Red Cap Button) | 1        | 0.391            | 0.391       |
| **Total**         |          |                  | **62.44**   |
# Critical Reflection

The testing can be seen in the following video: 
https://youtu.be/SJD08mUfLrc

Generally the comfort of device usage was good. The pins were moving up and down smoothly sporadically blocking. The device produced was robust and efficiently made the size translated braille pin usable. In this case there were no downsides of this setup therefore physical design of the casing, the pins and motors will be used in the next iterations. The only downside posted is the code which uses delays that block the motor from coming to the top simultaneously. Pin stability definitely was increased due to the pin silos making the pin movement stable and click more firm and comfortable making it preferred choice.