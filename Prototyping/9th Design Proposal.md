Date : 2024-10-06

# Tasks : Motor Simultaneous Movement with time control, casing modifications and ESP32 Introduction

# Goals
- Assemble Proper size, 6 braille pin device
- Use ESP32 as microcontroller (WHY?)
- Use millis() to control the timing instead of delays

# Description
The design proposal introduces higher fidelity of the braille device with more detailed definition of a braille casing as well as additional functionality that will allow the pins to move simultaneously without any blocking in the code. The casing in the proposal will be used as a braille cell with 6 pins attached with the ability to test device as an middle grade prototype and understand improvement to be made. ESP32 with its cost effective solution and computational power replaced Arduino Uno. ESP32 offers more pins which are necessary for connection and will be tested to bring speech-to-text and text-to-speech functionality which is beyond capability of Arduino UNO. The code was modified to use millis() instead of delays to move pin separately in the loop rather the stop the execution of the code to wait until the pin will go up.

# Prototyping
The idea behind the prototyping was to create more stable and real version of the device that resembles final fidelity design with the usable fidelity.

## Casing
The previous 2 pin design proven to be very successful option therefore the casing will continue with the bottom tray as pin holder approach and extended braille cap silos. The only different will be in size where this iteration will introduce full size device.
### Top Tray
#### Images
![[Pasted image 20250411212321.png]]
#### Code
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
    }   
}
```
### Middle Tray
#### Images
![[Pasted image 20250411210549.png]]
#### Code
```
module topSuface () {
    minkowski (){
        //cube([69.5,139,60.5],center=true); 
        cube([185,120,60.5],center=true);
        sphere(10,$fn=20);
        }
  
}

module middleHole () {
    cube([190,123.68,100],center=true); 
    }  
    
module innerMerger () {
    translate([0,0,31])
    cube([197,130.5,10],center=true);
    translate([0,0,-31])
    cube([197,130.5,10],center=true);
    }
    
 module differenceCubeTop () {
    cube([54.1,124.1,60.5],center=true);
}
module flateresCubes () {
     translate([0,0,38])
     cube([210,140,12],center=true);
     translate([0,0,-38])
     cube([210,140,12],center=true);
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
### Bottom Tray
#### Images
![[Pasted image 20250411210408.png]]
#### Code
```
module topSuface () {
    minkowski() {
    translate([0,0,100])
    cube([185,120,100],center=true);
    sphere(10,$fn=20);
   }
}
    
module main () {
difference() {
cube([188,123,5],center=true); 
cube([180,115,10],center=true);
    }
}

module pinHoles () {
translate([0,32.5,0])
cube([8.2,8.2,100],center=true);
translate([0,-32.5,0])
cube([8.2,8.2,100],center=true);
translate([-65,-32.5,0])
cube([8.2,8.2,100],center=true);
translate([-65,32.5,0])
cube([8.2,8.2,100],center=true);
translate([65,32.5,0])
cube([8.2,8.2,100],center=true);
translate([65,-32.5,0])
cube([8.2,8.2,100],center=true);
}

module CableHole() {
    translate([0,70,134])
    rotate([90,90,0])
    cylinder(30,16,16,center=true);
    }
module GripDots() {
    //side dots
    translate([99,0,125])
    sphere(1);
    translate([-99,0,125])
    sphere(1);
    //other dots
    translate([0,-65.1,125])
    sphere(1);
    
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
minkowski() {
       difference() {
       topSuface();
       translate([0,0,31])
       main();
       translate([0,0,120])
       pinHoles();
       differenceCube();
       translate([0,0,84])
       cube([191,125,141],center=true);
       translate([0,0,-22])
       cube([300,300,105],center=true); 
       CableHole();
        }
    }
```
### ESP32 With Millis()
```
int motor1Pin1 = 27;
int motor1Pin2 = 26;
int motor2Pin1 = 33;
int motor2Pin2 = 25;
int motor3Pin1 = 2;
int motor3Pin2 = 0;
int motor4Pin1 = 22;
int motor4Pin2 = 23;
int motor5Pin1 = 19;
int motor5Pin2 = 13;
int motor6Pin1 = 14;
int motor6Pin2 = 21;

//first motor controller board
int buttonPin1 = 17;
int buttonPin2 = 16;
int buttonPin3 = 18;
int buttonPin4 = 5;
int buttonPin5 = 15;
int buttonPin6 = 32;

bool motor1Active = false;
bool motor2Active = false;
bool motor3Active = false;
bool motor4Active = false;
bool motor5Active = false;
bool motor6Active = false;

//general start time
unsigned long startTime;
//separate start time variable for test
unsigned long startTime1 = 0;
unsigned long startTime2 = 0;
unsigned long prevTime = 0;

//motor timing stages
unsigned long elapsedTimeMotor1 = 0;
unsigned long elapsedTimeMotor2 = 0;
unsigned long elapsedTimeMotor3 = 0;
unsigned long elapsedTimeMotor4 = 0;
unsigned long elapsedTimeMotor5 = 0;
unsigned long elapsedTimeMotor6 = 0;

//motor states
bool motor1State = 0;
bool motor2State = 0;
bool motor3State = 0;
bool motor4State = 0;
bool motor5State = 0;
bool motor6State = 0;

//button states
bool button1State = 0;
bool button2State = 0;
bool button3State = 0;
bool button4State = 0;
bool button5State = 0;
bool button6State = 0;

//iterationCount
bool isFirstIterationMotor1 = false;
bool isFirstIterationMotor2 = false;
bool isFirstIterationMotor3 = false;
bool isFirstIterationMotor4 = false;
bool isFirstIterationMotor5 = false;
bool isFirstIterationMotor6 = false;

void setup() {
  Serial.begin(9600);
  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  // pinMode(enable1Pin, OUTPUT);

  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);
  // pinMode(enable2Pin, OUTPUT);

  //Motor pin 3
  pinMode(motor3Pin1, OUTPUT);
  pinMode(motor3Pin2, OUTPUT);

  //Motor pin 4
  pinMode(motor4Pin1, OUTPUT);
  pinMode(motor4Pin2, OUTPUT);

  //Motor pin 5
  pinMode(motor5Pin1, OUTPUT);
  pinMode(motor5Pin2, OUTPUT);

  //Motor pin 6
  pinMode(motor6Pin1, OUTPUT);
  pinMode(motor6Pin2, OUTPUT);

  //button pins setup
  pinMode(buttonPin1, INPUT_PULLUP);
  pinMode(buttonPin2, INPUT_PULLUP);
  pinMode(buttonPin3, INPUT_PULLUP);
  pinMode(buttonPin4, INPUT_PULLUP);
  pinMode(buttonPin5, INPUT_PULLUP);
  pinMode(buttonPin6, INPUT_PULLUP);

  //set stattime to millis
  startTime = millis();
}

void loop() {

  //control motor1 button click
  //if motor is not moving activate the button
  if (motor1Active == false) {
    button1State = digitalRead(buttonPin1);
  }
  //else disable the button - block clicking possibility
  else
    button1State = 2;

  //control motor2 button click - same as above
  if (motor2Active == false) {
    button2State = digitalRead(buttonPin2);
  } else button2State = 2;

  //control motor3 button click - same as above
  if (motor3Active == false) {
    button3State = digitalRead(buttonPin3);
  } else button3State = 2;

  //control motor4 button click - same as above
  if (motor4Active == false) {
    button4State = digitalRead(buttonPin4);
  } else button4State = 2;

  //control motor5 button click - same as above
  if (motor5Active == false) {
    button5State = digitalRead(buttonPin5);
  } else button5State = 2;

  //control motor6 button click - same as above
  if (motor6Active == false) {
    button6State = digitalRead(buttonPin6);
  } else button6State = 2;

  //motor 1 controller code
  // if button is pressed or motor1 is moving one or the other direction
  if (button1State == 0 || motor1Active == true) {
    if (isFirstIterationMotor1 == true) {
      motor1Active = true;
      elapsedTimeMotor1 = millis();
      isFirstIterationMotor1 = false;
    }
    if (millis() - elapsedTimeMotor1 <= 3000 && motor1State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(motor1Pin1, LOW);
      digitalWrite(motor1Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor1 <= 3000 && motor1State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(motor1Pin1, HIGH);
      digitalWrite(motor1Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor1 = millis();
      digitalWrite(motor1Pin1, LOW);
      digitalWrite(motor1Pin2, LOW);
      isFirstIterationMotor1 = true;
      if (motor1State == 0) {
        motor1State = 1;
      } else motor1State = 0;
      motor1Active = false;
    }
  }

  //motor 2 code
  if (button2State == 0 || motor2Active == true) {
    if (isFirstIterationMotor2 == true) {
      motor2Active = true;
      elapsedTimeMotor2 = millis();
      isFirstIterationMotor2 = false;
    }
    if (millis() - elapsedTimeMotor2 <= 3000 && motor2State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(motor2Pin1, LOW);
      digitalWrite(motor2Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor2 <= 3000 && motor2State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor2);
      digitalWrite(motor2Pin1, HIGH);
      digitalWrite(motor2Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor2 = millis();
      digitalWrite(motor2Pin1, LOW);
      digitalWrite(motor2Pin2, LOW);
      isFirstIterationMotor2 = true;
      if (motor2State == 0) {
        motor2State = 1;
      } else motor2State = 0;
      motor2Active = false;
    }
  }

  //motor 3 code
  if (button3State == 0 || motor3Active == true) {
    if (isFirstIterationMotor3 == true) {
      motor3Active = true;
      elapsedTimeMotor3 = millis();
      isFirstIterationMotor3 = false;
    }
    if (millis() - elapsedTimeMotor3 <= 3000 && motor3State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(motor3Pin1, LOW);
      digitalWrite(motor3Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor3 <= 3000 && motor3State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor3);
      digitalWrite(motor3Pin1, HIGH);
      digitalWrite(motor3Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor3 = millis();
      digitalWrite(motor3Pin1, LOW);
      digitalWrite(motor3Pin2, LOW);
      isFirstIterationMotor3 = true;
      if (motor3State == 0) {
        motor3State = 1;
      } else motor3State = 0;
      motor3Active = false;
    }
  }

  //motor 4 code
  if (button4State == 0 || motor4Active == true) {
    if (isFirstIterationMotor4 == true) {
      motor4Active = true;
      elapsedTimeMotor4 = millis();
      isFirstIterationMotor4 = false;
    }
    if (millis() - elapsedTimeMotor4 <= 3000 && motor4State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor4);
      digitalWrite(motor4Pin1, LOW);
      digitalWrite(motor4Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor4 <= 3000 && motor4State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor4);
      digitalWrite(motor4Pin1, HIGH);
      digitalWrite(motor4Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor4 = millis();
      digitalWrite(motor4Pin1, LOW);
      digitalWrite(motor4Pin2, LOW);
      isFirstIterationMotor4 = true;
      if (motor4State == 0) {
        motor4State = 1;
      } else motor4State = 0;
      motor4Active = false;
    }
  }

  //motor 5 code
  if (button5State == 0 || motor5Active == true) {
    if (isFirstIterationMotor5 == true) {
      motor5Active = true;
      elapsedTimeMotor5 = millis();
      isFirstIterationMotor5 = false;
    }
    if (millis() - elapsedTimeMotor5 <= 3000 && motor5State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor5);
      digitalWrite(motor5Pin1, LOW);
      digitalWrite(motor5Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor5 <= 3000 && motor5State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor2);
      digitalWrite(motor5Pin1, HIGH);
      digitalWrite(motor5Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor5 = millis();
      digitalWrite(motor5Pin1, LOW);
      digitalWrite(motor5Pin2, LOW);
      isFirstIterationMotor5 = true;
      if (motor5State == 0) {
        motor5State = 1;
      } else motor5State = 0;
      motor5Active = false;
    }
  }

  //motor 6 code
  if (button6State == 0 || motor6Active == true) {
    if (isFirstIterationMotor6 == true) {
      motor6Active = true;
      elapsedTimeMotor6 = millis();
      isFirstIterationMotor6 = false;
    }
    if (millis() - elapsedTimeMotor6 <= 3000 && motor6State == false) {
      Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor6);
      digitalWrite(motor6Pin1, LOW);
      digitalWrite(motor6Pin2, HIGH);

    } else if (millis() - elapsedTimeMotor6 <= 3000 && motor6State == true) {
      Serial.println("Motor is going Down with timer");
      Serial.println(millis() - elapsedTimeMotor6);
      digitalWrite(motor6Pin1, HIGH);
      digitalWrite(motor6Pin2, LOW);
    } else {
      Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor6 = millis();
      digitalWrite(motor6Pin1, LOW);
      digitalWrite(motor6Pin2, LOW);
      isFirstIterationMotor6 = true;
      if (motor6State == 0) {
        motor6State = 1;
      } else motor6State = 0;
      motor6Active = false;
    }
  }
}
```

# Creating
The board change posted some problems when it came to connecting TB6612FNG Motor Controller to ESP32. Due to the fact that connection didn't work the older model L298N was used to accommodate motor movement functionality. 

ESP32 was connected according to this diagram:
![[6 Motors Diagram 1.png]]

The elements were 3D printed, motors were put inside the pins and the entire device was assembled and tested.
![[IMG_6671.jpg]]
Pins and Electronic Setup

![[IMG_6672.jpg]]
Electronic Components

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
| Supports               | None     |
| Raft                   | Enabled       |
| Cooling Fan            | Enabled after 1–2 layers      |
# Cost
| Item                  | Quantity | Unit Price (CAD) | Total (CAD) |
|-----------------------|----------|------------------|-------------|
| Screw (M5)                | 6        | 0.1155           | 0.693       |
| Motor (N10)                 | 6        | 3.48             | 20.88       |
| Motor Controller (L298N) | 3     | 1.75             | 5.25        |
| ESP32-S3              | 1        | 8.67             | 8.67        |
| Filament              | 1        | 14.00            | 14.00       |
| Button (Smaller Red Cap Button)     | 6        | 0.391            | 2.346       |
| **Total**             |          |                  | **51.84**   |
# Critical Reflection
Esp32 reduced the cost of the device significantly. It was performing the same way as Arduino Uno offering more pins.
Generally the device performed its action well. Pins were moving up and down with moderate speed as well as the 6 pin device was performing as good as the 2 pin version. It was standing stable on the table and modularity concepts were snapping together well.
Millis code added functionality to the device to move pins simultaneously and the performance of the code was also very good. There were not problem with timings however motor blocks still occurred implying the need for additional sensor controlling motor position.
Another consideration is that device position, meaning front and back is not clearly articulated making it difficult to understand future letter haptically. The front and back of the device should be clearly articulated. 