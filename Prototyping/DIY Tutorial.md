# Device Production
To form a device there are several steps. 
- 3D printing
- Electronic Connection
- ChatGPT and Whispers API 
# 3D printing
Step 1. To start 3D printing prepare the printer bed. To prepare it purchase a strong painting duct tape and wrap the printing bed line by line moving linearly from the front to the back.
Step 2. Download OpenSCAD software
Step 3. Create a folder "Cow Parts" and Copy and Paste the following codes to OpenSCAD. For each code press F6 button and then F7 and save it in the folder.
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
## Codes
### Casing
>Reprint the entire casing scaled down to 70% for electronic compartment
#### Top Cover
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
#### Middle Cover
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
#### Bottom Cover
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
#### Head Holder
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
#### Cow Shape
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
#### Tail
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
### Pins - Print six times
#### Bottom pin
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
#### Top pin Casing
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
#### Converter
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
#### Button Casing
```
module cylinderTop () {
    translate([0,0,11])
    difference(){
    cylinder(26,10,10,center=true);
    cylinder(28,6.5,6.5,center=true);
    }
}
    
module transferCube () {
    translate([0,0,-9])
    cube([12,13,10],center=true);
}

module gripDots () {
    translate([0,7.4,23.2])
    sphere(r = 0.3);
     translate([0,-7.4,23.2])
    sphere(r = 0.3);
    
    translate([6.3,-3.8,23.2])
    sphere(r = 0.3);
    translate([6.3,3.8,23.2])
    sphere(r = 0.3);
    
    translate([-6.3,3.8,23.2])
    sphere(r = 0.3);
    translate([-6.3,-3.8,23.2])
    sphere(r = 0.3);
    
    //inside cylinder dots 
    translate([0,6.5,19.2])
    sphere(r = 0.3);
    translate([0,-6.5,19.2])
    sphere(r = 0.3);
    translate([6.5,0,19.2])
    sphere(r = 0.3);
    translate([-6.5,0,19.2])
    sphere(r = 0.3);
    
}

module railCyliderSupport () {
     translate([0,2.3,-3.2])
     cube([20,1.8,5],center=true); 
     translate([0,-2.3,-3.2])
     cube([20,1.8,5],center=true);
    }
    
module cableHoles () {
    rotate([45,0,90])
    translate([0,2,-6])
    cylinder(11,3,3,center = true);
     rotate([45,0,-90])
    translate([0,2,-6])
    cylinder(11,3,3,center = true);
    }
    
 module buttonScrewHolder () {
     translate([0,0,23])
      cylinder(3,8.5,8.5,$fn=6,center=true);
     }
   
    difference() {
    cylinderTop ();
    cableHoles();
    buttonScrewHolder();  
        }
        
    difference () {
    transferCube();
    cableHoles();
        }
        
    difference () {
    railCyliderSupport();
    cableHoles();
    }    
        
    gripDots();
```
#### Braille Cap
```
module attachmentCube() {
    translate([0,0,22])
    difference(){
        cylinder(26,12,12,center=true,$fn = 300);
        cylinder(28,10.75,10.75,center=true,$fn = 300);
        }
    }

module cylinderPin() {
    difference() {
     cylinder(35,20,20,$fn = 300);
     translate([0,0,-5])
     cylinder(35,18,18,$fn = 300);
     }
    }

   cylinderPin();
   attachmentCube();
```
#### Cable Blocker
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
To prepare the fidelity sand the printed models following this tutorial: https://www.youtube.com/watch?v=ZTE9bJyUO_8 
### Time to Sand Casing Exterior Modules - 12 hours
# Electronic Components
## Components List 
| Item               | Quantity |
|--------------------|----------|
| Screws (M5)             | 6        |
| Motors (N10 - 1080 rpm)           | 6        |
| Motor Controllers (TB6612FNG)  | 3        |
| ESP32-S3           | 1        |
| Raspberry Pi Zero 2 W      | 1        |
| Wires (Any)          | 1        |
| Extension Board (Adafruit MCP23017 I2C GPIO Expander)   | 1        |
| USB Extender (Any)       | 1        |
| USB Sound Card (Any)        | 1        |
| USB Cables (MicroUSB to USB)        | 2        |
| Buttons (Link Below) | 6        |
| Aluminum Foil | 1       |
Button Link : https://www.aliexpress.com/item/4000164264475.html?spm=a2g0o.productlist.main.13.4d6e8Q3L8Q3LGN&algo_pvid=65202e15-4f33-459c-ac4a-f74ad9f55610&algo_exp_id=65202e15-4f33-459c-ac4a-f74ad9f55610-6&pdp_ext_f=%7B%22order%22%3A%222626%22%2C%22eval%22%3A%221%22%7D&pdp_npi=4%40dis%21CAD%213.68%212.97%21%21%212.59%212.09%21%402101c59817456189224257199e0d79%2110000000546188163%21sea%21CA%210%21ABX&curPageLogUid=iEiE8f0FsbST&utparam-url=scene%3Asearch%7Cquery_from%3A
All the parts can be found on websites such as aliexpress.com, amazon.ca , roboshop.ca or digikey.ca
# Assembly
Check for item pins and wiring. If they are not soldered please see the tutorial: https://www.youtube.com/watch?v=Qps9woUGkvI&t=2s and solder the wires and pins to the specific places. 
In the common case: 
- Wires has to be striped and soldered to the N10 motor
- TB6612FNG Motor Controllers pins has to be soldered to the board
- Raspberry Pi Zero 2 W pins has to be soldered to the board
- Adafruit MCP23017 I2C GPIO Expander pins has to be soldered to the board
When all the electronic components are soldered and ready to use: 
## Casing and Pin
### Step 1
Take the bottom pin and put the motor inside pulling the wires through the holes.
### Step 2 
Attach converter to the motor
### Step 3
Put screw on top of the converter and screw the nut
### Step 4
Put the top pin casing on the screw and bottom pin - Make sure the screw nut snaps in to the hole.
### Step 5
Snap in the button casing to the top pin casing
### Step 6
Put the button to the casing and drag the wires through the holes
### Step 7
Put braille cap on the button
### Step 8
Pull the stripped wire through the square attachment and glue the wires to the aluminum (can be sticky aluminum foil or simply attached with the duct tape)
> Repeat for 6 pins
### Step 9
Place the pins in the holes of bottom casing
> Leave the middle and top casing attachment till the end
## Electronics
### Connect the Electronic Components According to This diagram: 
![[final diagram.png]]
> Make sure that the electronic components and buttons and motors aren't connected yet

## Final Assembly
## Step 10
Put the electronic components into the other printed compartment.
## Step 11
Attach the buttons and motors according to the diagram. Check if initially the buttons are rising linearly one after another starting from 1 and following to 2 and 3 in the other row. If not change holes of pins on the bottom tray to match it.  Pull the wires through the hole in both compartments.
## Step 12
Attach the cable holder by putting it sideways and twist it to hold
## Step 13
Put the USB extender into the pin compartment on the shorter wall. Attach the sound card. Attach speakers and microphone to it and pull the microphone through the hole in the cable holder.
## Step 14
Connect Raspberry PI to the monitor and keyboard and mouse through the USB extender and pull the wires through the cable hole. 
> Makes sure to pull the power supply wires through the hole too
## Step 15
Enclose the compartments.

# ChatGPT and Whispers
## Step 16 
Upload the Raspberry PI operating system to the SD card from this website : https://www.raspberrypi.com/software/
## Step 17
Open the operation system and create a python .py file and copy paste the code below. 

```
import openai
import os
import sounddevice as sd
import numpy as np
import wave
import subprocess
import random
import time
import serial  # Import serial communil,;;;;;ttion
import threading
import re

# OpenAI API Key
api_key = "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"  # Replace with your actual API key
client = openai.OpenAI(api_key=api_key)

# Audio settings
SAMPLE_RATE = 44100
CHANNELS = 1
DURATION = 15  # Listening time in seconds

# Increase buffer size for smoother audio recording
sd.default.latency = 'high'

# Set system-wide volume to 100% for loudest playbacke
subprocess.run(["amixer", "set", "PCM", "180%"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
# Keep track of used nouns
selected_nouns = set()  

# Serial communication setup
ESP32_PORT = "/dev/serial0"  # Updated for Raspberry Pi UART
BAUD_RATE = 115200
try:
    ser = serial.Serial(ESP32_PORT, BAUD_RATE, timeout=1)
    time.sleep(2)  # Allow time for connection to establish
    print("Connected to ESP32 via TX/RX!")
except serial.SerialException as e:
    print(f"Serial Error: {e}")
    ser = None

def play_signal():
    subprocess.run(["mpg123", "--gain", "300", "signal.mp3"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)

def play_end_signal():
    subprocess.run(["mpg123", "--gain", "300", "signal.mp3"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)

def record_audio(filename="input.wav"):
    print("🎤 Listening... Speak now!")
    recording = sd.rec(int(SAMPLE_RATE * DURATION), samplerate=SAMPLE_RATE, channels=CHANNELS, dtype=np.int16)
    sd.wait()
    play_end_signal()
    with wave.open(filename, "wb") as wavefile:
        wavefile.setnchannels(CHANNELS)
        wavefile.setsampwidth(2)
        wavefile.setframerate(SAMPLE_RATE)
        wavefile.writeframes(recording.tobytes())
    print("✅ Recording saved!")

def transcribe_audio(filename="input.wav"):
    with open(filename, "rb") as audio_file:
        transcript = client.audio.transcriptions.create(
            model="whisper-1",
            file=audio_file
        )
    return transcript.text.strip()

def play_processing():
    def play_loop():
        while processing_flag:
            subprocess.run(["mpg123", "--gain", "300", "processing.mp3"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)
    
    global processing_flag
    processing_flag = True
    threading.Thread(target=play_loop, daemon=True).start()

def stop_processing():
    global processing_flag
    processing_flag = False
    subprocess.run(["mpg123", "--gain", "300", "processing.mp3"], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)


def generate_congratulatory_message():
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        temperature=1.2,
        messages=[
            {"role": "system", "content": "You are an encouraging AI. Generate a fun and engaging congratulatory message for someone who spelled a word correctly."},
            {"role": "user", "content": "Give me a great response to praise someone for spelling correctly."}
        ],
        max_tokens=150
    )
    return re.sub(r'[^\w\s]','',response.choices[0].message.content.strip())

def generate_intro():
    system_instruction = (
        "You are a friendly, engaging storytelling assistant that will lead chidren at the age of 0-5 through some braille exercises. Introduce yourself in a natural, conversational way. "
    )
    user_message = "Introduce yourself naturally before asking the user to share a story theme."
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        temperature=1.3,
        messages=[
            {"role": "system", "content": system_instruction},
            {"role": "user", "content": user_message}
        ],
        max_tokens=180,
        stop=["\n"]
    )
    return response.choices[0].message.content.strip()

# Function to extend the story naturally
def extend_story(previous_story):
    system_instruction = (
        "You are continuing a story. Add only 2 sentences which is 300 characters maximum. Keep the pacing smooth and natural. Ensure sentences are complete and do not get cut off."
    )

    user_message = f"Continue the story with exactly 2 sentences or 300 characters Ensure sentences are complete and do not get cut off. Current story: {previous_story}"

    response = client.chat.completions.create(
        model="gpt-4-turbo",
        temperature=1.2,
        messages=[
            {"role": "system", "content": system_instruction},
            {"role": "user", "content": user_message}
        ],
        max_tokens=160,
        stop=["\n"]
    )
    return response.choices[0].message.content.strip()

def select_noun(story):
    words = story.split()
    nouns = [word for word in words if word[0].isupper() and len(word) > 2]  # Picks proper nouns

    if nouns:
        unique_nouns = list(set(nouns) - selected_nouns)
        if unique_nouns:
            selected = random.choice(unique_nouns)
        else:
            selected = random.choice(nouns)  # Fallback if all are used
    else:
        selected = random.choice(words)  # Fallback if no proper nouns

    selected_nouns.add(selected)  # Store used nouns
    return selected


def generate_story(theme):
    system_instruction = (
        "You are a skilled storyteller for young children. Start with only 2-3 engaging sentences. The story suppose to be suited for kids. Make sure it's simple and engaging."
    )
    user_message = f"The theme is: {theme}. Begin the story in just 2-3 sentences."
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        temperature=1.2,
        messages=[
            {"role": "system", "content": system_instruction},
            {"role": "user", "content": user_message}
        ],
        max_tokens=120,
        stop=["\n"]
    )
    return response.choices[0].message.content.strip()

def text_to_speech(text, filename="output.mp3"):
    response = client.audio.speech.create(
        model="tts-1",
        voice="sage",
        input=text
    )
    with open(filename, "wb") as f:
        f.write(response.content)
    subprocess.run(["mpg123", "--gain", "1700", filename], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)

def send_to_esp32(letter):
    if ser is None:
        print("Serial connection not established.")
        return
    
    ser.write(letter.upper().encode('utf-8'))  # Send letter to ESP32
    print(f"Sent to ESP32: {letter}")
    time.sleep(0.1)  # Small delay to ensure transmission
    while True:
        if ser.in_waiting:
            response = ser.readline().decode('utf-8').strip()
            print(f"Received from ESP32: {response}")
            if response == "Done":
                break  # Proceed when ESP32 acknowledges completion

def main():
    if ser is None:
        print("ESP32 is not connected. Exiting...")
        return
    
    intro = generate_intro()
    text_to_speech(intro)
    play_signal()
    record_audio()
    play_processing()
    play_processing()
    theme = transcribe_audio()
    stop_processing()
    print(f"📖 Story Theme: {theme}")
    play_processing()
    play_processing()
    story = generate_story(theme)
    stop_processing()
    print("📝 Story:", story)
    text_to_speech(story)
    while True:
        selected_word = select_noun(story)
        text_to_speech(f"Now spell the word: {selected_word}")
        for letter in selected_word:
            text_to_speech(f" Now we will spell the letter {letter}")
            send_to_esp32(letter)
        print("Good job! Well spelled.")
        text_to_speech(generate_congratulatory_message())
        print("🔄 Extending story...")
        play_processing()
        new_part = extend_story(story)
        stop_processing()
        story += " " + new_part
        print("📖 Updated Story:", story)
        text_to_speech(new_part)

if __name__ == "__main__":
    main()
```

## Step 18 
Generate the OpenAI key through this tutorial and copy-paste it to the code. 
1. Create an OpenAI Account
- Visit https://platform.openai.com/signup
- Sign up with your email, Google account, or Microsoft account.

2. Verify Your Email
- Check your email inbox.
- Click the verification link from OpenAI.

3. Log In to the OpenAI Platform
- Go to https://platform.openai.com/
- Click "Log In" and enter your credentials.

4. Go to the API Keys Section
- After logging in, click your profile icon in the top-right corner.
- Select "View API Keys" from the dropdown menu.

5. Create a New API Key
- Click "Create new secret key."
- Copy the key when it appears. You will not be able to view it again later.

6. Save the API Key
- Store the key somewhere secure, such as a password manager or an encrypted file.

7. Use the API Key in Your Application
- Example for Python:
    ```python
    import openai

    openai.api_key = "your-api-key-here"
    ```

## Step 19
Run script in the console using this command to install plugins:
```
pip install openai sounddevice numpy pyserial
sudo apt install mpg123
```
Run this command to run script: 
```
python3 send.py
```

## Enjoy the Braille Device

# References
_Finishing 3D Prints: How to Sand, Fill and Prime 3D Printed Parts_. (n.d.). [Video recording]. Retrieved April 26, 2025, from [https://www.youtube.com/watch?v=ZTE9bJyUO_8](https://www.youtube.com/watch?v=ZTE9bJyUO_8)

Ltd, R. P. (n.d.). _Raspberry Pi OS_. Raspberry Pi. Retrieved April 26, 2025, from [https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/)

oneTesla (Director). (2014, June 18). _Soldering Tutorial for Beginners: Five Easy Steps_ [Video recording]. [https://www.youtube.com/watch?v=Qps9woUGkvI](https://www.youtube.com/watch?v=Qps9woUGkvI)

_Organic Parametric Shapes: Bézier Curves in OpenSCAD_. (n.d.). Retrieved April 26, 2025, from [https://raphaelluckom.com/posts/bezier_curves.html](https://raphaelluckom.com/posts/bezier_curves.html)

_Overview—OpenAI API_. (n.d.). Retrieved April 26, 2025, from [https://platform.openai.com](https://platform.openai.com)

_Push Button Switch Arduino|12mm Momentary Push Button Switches 3a 125vac 1.5a 250vac—6pcs Set_. (n.d.). Aliexpress. Retrieved April 26, 2025, from [//www.aliexpress.com/item/4000164264475.html?src=ibdm_d03p0558e02r02&sk=&aff_platform=&aff_trace_key=&af=&cv=&cn=&dp=&aff_short_key=](https://doi.org///www.aliexpress.com/item/4000164264475.html?src=ibdm_d03p0558e02r02&sk=&aff_platform=&aff_trace_key=&af=&cv=&cn=&dp=&aff_short_key=)