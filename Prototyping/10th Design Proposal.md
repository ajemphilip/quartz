Date : 2024-10-13

# Tasks : Motor block aluminum sensor and AI-Thinker Board

# Goals
- Create aluminum sensor from conductive material to check pin height
- Connect AI-Thinker VC-02 board to ESP32 to perform voice activated actions

# Description
The previous methods of pin block failed therefore, in this design proposal using ESP32 touch sensor and small pieces of sticky aluminum foil on top pin and bottom pin the sensor was design so when two pieces touch together they increased the touch pin sensor value making the motor stop. AI-Thinker VC02 was also tested to test its capacity to take preselected "move the pin" command and shortly answer "moving the pin". The proposal tested voice integration, its fidelity as well as how well touch sensor performs and will it prevent pin from blocking.

# Prototyping
![[PENUP_20250425_200311.jpg]]
Pin with Aluminum Foil

The top and bottom pins were modified to accommodate aluminum foil piece and cable. The pieces had holes in them to attach the cable to one piece of aluminum foil and ESP32. The other piece was attached to other plastic piece sticking out from the pin. 

## Top Pin Modified
### Image
![[Pasted image 20250411213007.png]]
### Code
```
module railPinCasing () {
    difference () {
        translate([0,0,-23])
        cube([21,21,52],center=true);
        translate([0,0,-28])
        cube([18,18,48],center=true);
        }
    }

module transferCube() {
     translate([0,0,15.5])
     cube([14,15,33],center=true);
      }
      
module gripDots() {
     translate([0,6.8,35])
     sphere(r = 1);
     translate([0,-6.8,35])
     sphere(r = 1);
     translate([6.4,0,35])
     sphere(r = 1);
     translate([-6.4,0,35])
     sphere(r = 1);
     }
     
 module gripDotsScrew () {
translate([0,5,-3])
sphere(0.2); 
 translate([0,-5,-3])
sphere(0.2);      
}

 module screwHolderCylinder () {
     translate([0,0,-4])
     cylinder(6.5,5.8,5.8,$fn=6,center=true);
     }    
     
 module screwSpaceCylinder () {
      cylinder(63,4.5,4.5,$fn=100,center=true);
     }
     
 module topButtonHolder () {
       difference() {
       translate([0,0,34])
       cube([17.5,18.5,13.5],center=true);
       translate([0,0,31])
       cube([12.6,13.6,20],center=true);
             }
     }  
     
module sensorCube (){
    difference(){
    translate([13,0,-48.5])
    cube([6,6,2],center=true);
    translate([13,0,-48.5])
    cube(2.9,center=true);
    }
}
     
module differencedTop () {
        difference() {
        transferCube();
        screwHolderCylinder();
        screwSpaceCylinder();
            }
        }  

 module diferencedBot () {
     difference() {
        railPinCasing();
        screwHolderCylinder();
        screwSpaceCylinder();
  }
}   
//modules
     differencedTop();  
     topButtonHolder();
     gripDots();
     sensorCube();
     gripDotsScrew();
     difference() {
     diferencedBot();
}
```
## Bottom Pin Modified
### Image
![[Pasted image 20250411213143.png]]
### Code
```
module mainCube () {
    difference() {
cube([17,17,25],center=true);
translate([0,0,3])
cube([14,12,26],center=true);
    }
}

module gripDots () {
    translate([0,5.6,0])
    sphere(1);
    translate([0,-5.6,0])
    sphere(1);
    translate([6.6,0,0])
    sphere(1);
    translate([-6.6,0,0])
    sphere(1);
}  

 module cableHoles (){
     translate([4.5,0,-8])
     cylinder(10,3,3,center=true);
     translate([-4.5,0,-8])
     cylinder(10,3,3,center=true);
}
module sensorCube (){
    difference(){
    translate([10,0,-11.5])
    cube([6,6,2],center=true);
    translate([10,0,-11.5])
    cube(2.9,center=true);
    }
}

module bottomAttachementCube () {
translate([0,0,-16])
cube([8,8,8],center=true);
}

//Modules
difference(){
    mainCube();
    cableHoles();
}

sensorCube();
bottomAttachementCube();
gripDots();
```
## Electronics
Esp32 Sketch was made with the following code:
```
#include <HardwareSerial.h>

int STBY = 27;  //standby

//Motor A
int PWMA = 13;  //Speed control
int AIN1 = 14;  //Direction
int AIN2 = 12;  //Direction

//button pin
int buttonPin1 = 5;

//motorActive indicator
bool motor1Active = false;

//analog pin
int analogPin = 34;

//general start time
unsigned long startTime;

//separate start time variable for test
unsigned long startTime1 = 0;
unsigned long startTime2 = 0;
unsigned long prevTime = 0;

//motor timing stages
unsigned long elapsedTimeMotor1 = 0;

//received value
unsigned int receivedValue = 0;

//motor states
bool motor1State = 0;

//button states
bool button1State = 0;

//iterationCount
bool isFirstIterationMotor1 = false;

HardwareSerial VC02(2);  // Use UART2 (TX: 17, RX: 16)

void setup() {
  Serial.begin(9600);
  VC02.begin(9600, SERIAL_8N1, 16, 17);

  pinMode(STBY, OUTPUT);
  pinMode(PWMA, OUTPUT);
  pinMode(AIN1, OUTPUT);
  pinMode(AIN2, OUTPUT);

  // button pins setup
  pinMode(buttonPin1, INPUT_PULLUP);

  //set stattime to millis
  startTime = millis();
}

void loop() {

  if (VC02.available()) {
    // String response = VC02.readString();
    // Read the incoming bytes
    byte highByte = VC02.read();
    byte lowByte = VC02.read();

    // Combine the two bytes into a single 16-bit value
    receivedValue = (highByte << 8) | lowByte;
    // Print the received value in HEX format
    Serial.print("Received HEX value: 0x");
    Serial.println(receivedValue, HEX);
  }
  delay(100);

  // analog sensor
  int sensorValue = touchRead(T0);
  Serial.println(touchRead(T0));

  //disable standby to make the motors run
  digitalWrite(STBY, HIGH);

  //set motor A and motor B speed, 0-255 255 being the fastest
  analogWrite(PWMA, 255);

  //control motor1 button click
  //if motor is not moving activate the button
  if (motor1Active == false) {
    button1State = digitalRead(buttonPin1);
  }
  //else disable the button - block clicking possibility
  else
    button1State = 2;

  //motor 1 controller code
  // if button is pressed or motor1 is moving one or the other direction
  if (button1State == 0 || motor1Active == true || receivedValue == 0xA190) {
    if (isFirstIterationMotor1 == true) {
      motor1Active = true;
      elapsedTimeMotor1 = millis();
      isFirstIterationMotor1 = false;
    }
    if (millis() - elapsedTimeMotor1 <= 1700 && motor1State == false) {
      // Serial.println("Motor is going Up");
      Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(AIN1, HIGH);
      digitalWrite(AIN2, LOW);

    } else if (millis() - elapsedTimeMotor1 <= 2000 && motor1State == true && sensorValue > 0) {
      // Serial.println("Motor is going Down with timer");
      // Serial.println(millis() - elapsedTimeMotor1);
      digitalWrite(AIN1, LOW);
      digitalWrite(AIN2, HIGH);
    } else {
      // Serial.println("Motor is Off");
      // set start time as code block time
      elapsedTimeMotor1 = millis();
      digitalWrite(AIN1, LOW);
      digitalWrite(AIN2, LOW);
      isFirstIterationMotor1 = true;
      receivedValue = 0;
      if (motor1State == 0) {
        motor1State = 1;
      } else motor1State = 0;
      motor1Active = false;
    }
  }
}
```
AI-Thinker VC02 SDK was modified through the manufacturer website https://voice.ai-thinker.com/
The SDK added two new commands "move the pin" and response "moving the pin"
# Creating
Casing parts were printed, and aluminum foil was applied to both ends of the pin.
All the electronic components were connected according to this electronic diagram:
![[voice 1.png]]

The SDK was not hard to create however the website and software its all in Chinese making it more difficult.

The functionality is recorded in this video
https://youtu.be/_ngmXNRcRPc

## The final setup is showcased on the picture: 
![[IMG_6714.jpg]]
Aluminum Foil at Bottom Pin

![[IMG_6710.jpg]]
Aluminum Foil Full PIn

![[IMG_6708.jpg]]
Ai-Thinker VC02 and Pin

![[IMG_6712.jpg]]
Motor and Sensor

![[IMG_6713.jpg]]
Aluminum Foil Top Pin Casing

![[IMG_6715.jpg]]
Aluminum Foil Bottom Pin wiring

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
| Item              | Quantity | Unit Price (CAD) | Total (CAD) |
|-------------------|----------|------------------|-------------|
| Screw (M5)            | 1        | 0.1155           | 0.1155      |
| Motor (N10)            | 1        | 3.48             | 3.48        |
| ESP32-S3          | 1        | 8.67             | 8.67        |
| Filament          | 1        | 14.00            | 14.00       |
| AI-Thinker VC02   | 1        | 2.33             | 2.33        |
| Aluminum Foil     | 1 roll   | 1.50             | 1.50        |
| **Total**         |          |                  | **30.10**   |
# Critical Reflection
Aluminum sensor performed very well. Motor was stopping in the right moment avoiding all the blocks which makes it preferred situation. 
AI-Thinker VC02 board generally performs its function however the voice semes to be very robotic with Chinese accent on top of that. The sensor is very sensitive therefore it turns on sometimes without any wakeup word spoken. With that said, it has no latency and its relatively cheap which is not the worst option when it comes to locally hosted voice control.

# References
_Ai-Thinker蓝牙模块_无线模块_物联网模块_WiFi模块【安信可官网】_. (n.d.). Retrieved April 26, 2025, from [https://voice.ai-thinker.com/](https://voice.ai-thinker.com/)