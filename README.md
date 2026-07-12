# The-Night-Beam-Motion-Detection-System
The Night Beam Motion Detection System is a low-cost smart security system designed to detect intrusions by monitoring a continuous light beam. When an object or person interrupts the beam, the system immediately triggers an audible and visual alarm to notify the user of potential movement in the protected area. 

## Features
- Beam-Break Motion Detection: Detects movement by monitoring interruptions in a continuous laser beam using a phototransistor. 
- Intrusion Alarm System: Triggers both audible and visual alarms when motion is detected. 
- Visual Status Indicator: Uses an LED to provide immediate visual feedback during an alarm event. 
- Audible Alert System: Sounds a buzzer to notify users of potential intrusions. 
- Arm and Disarm Functionality: Allows the user to enable or disable the monitoring system using a push button. 
- Real-Time Light Monitoring: Continuously measures and processes light intensity readings from the phototransistor. 
- Sensor Reading Averaging: Takes multiple sensor readings and calculates an average to reduce noise and improve reliability. 
- Adaptive Beam Baseline: Continuously updates the normal beam intensity to compensate for minor changes in ambient lighting. 
- Configurable Sensitivity: Detection thresholds can be adjusted to suit different environments and lighting conditions. 
- Low-Cost Design: Built using inexpensive and widely available components. 
- Simple and Expandable Architecture: Can easily be extended with features such as Wi-Fi notifications, mobile applications, event logging, or remote monitoring.
  
## Hardware Requirements
1. ESP8266 NodeMCU Development Board 
2. Phototransistor 
3. Laser Diode Module or LED Light Source 
4. Piezo Buzzer 
5. LED (Red) 
6. Push Button Switch 
7. Resistors 
8. Breadboard 
9. Jumper Wires
    
## Software Requirements
The following software is required to build and program the Night Beam Motion Detection System: 
1. Arduino IDE 
2. ESP8266 Board Package for Arduino 
3. USB Driver for NodeMCU ESP8266 (CH340 or CP2102, depending on your board) 
4. Serial Monitor configured to a baud rate of 115200 
5. No additional external libraries are required, as the project uses built-in Arduino functions such as tone(), analogRead(), and digitalWrite().
   
## Pin Configuration
1. A0 (Analog Input): Connected to the phototransistor circuit and used to measure the intensity of the laser beam.
2. D5 (Digital Output): Connected to the LED indicator, which illuminates when motion is detected.
3. D6 (Digital Output): Connected to the piezo buzzer, which generates an audible alarm when the beam is interrupted.
4. D7 (Digital Input): Connected to the push button used to arm and disarm the system.
5. 3.3V Pin: Provides power to the phototransistor circuit and other low-power components as required.
6. GND Pin: Provides the common ground connection for all components in the circuit 
 
## System Architecture
The Night Beam Motion Detection System consists of a laser module (or a light beam), a phototransistor sensor, an ESP8266 NodeMCU microcontroller, a push button, an LED indicator, and a piezo buzzer. 
1. The laser module continuously emits a beam of light toward the phototransistor. 
2. The phototransistor measures the intensity of the received light and sends an analog signal to the ESP8266 NodeMCU through pin A0. 
3. The ESP8266 continuously processes the sensor readings and compares them to the normal beam intensity. 
4. The push button allows the user to arm or disarm the security system. 
5. If the laser beam is interrupted and the light intensity drops below the configured threshold, the ESP8266 identifies this as motion or an intrusion. 
6. The microcontroller then activates the LED indicator and piezo buzzer to provide visual and audible alerts.
   
After the alarm sequence has completed, the system resumes monitoring the laser beam for additional interruptions. 

## System Flow
```
Laser Module 
↓ 
Phototransistor Sensor 
↓ 
ESP8266 NodeMCU 
↓ 
┌─────────────┬─────────────┐ 
LED                     Piezo Buzzer      
↑ 
Push Button (Arm/Disarm)

```
 
The architecture follows a simple sense → process → alert approach, where the phototransistor senses the beam, the ESP8266 processes the readings and makes decisions, and the LED and buzzer provide immediate feedback to the user.


## How the System Works

**Step 1: System Initialization**
When the ESP8266 powers on, it initializes the LED, buzzer, push button, and phototransistor. The system starts in a disarmed state and waits for the user to activate it. 

**Step 2: Arming the System**
The user presses the push button to arm the system. Once armed, the ESP8266 records the current light intensity reading as the normal beam value. 

**Step 3: Continuous Monitoring** 
The light sensor continuously measures the intensity of the light beam. To improve accuracy and reduce noise, the system takes multiple readings and calculates an average value. 

**Step 4: Detecting an Intrusion**
If an object, hand, or person passes through the beam, the amount of light reaching the sensor suddenly decreases. The system compares the new reading to the previously recorded beam value and determines whether the drop exceeds the predefined threshold.

**Step 5: Triggering the Alarm**
When a significant drop in light intensity is detected, the system identifies this as motion or an intrusion. The LED indicator turns on and the buzzer sounds to alert the user. 

**Step 6: Resetting and Continuing Monitoring**
After the alarm has been activated, the system returns to monitoring mode and continues checking the light beam for additional interruptions. 

**Step 7: Disarming the System** 
The user can press the push button again to disarm the system. Once disarmed, the alarm is disabled and the system stops monitoring the light beam until it is armed again. 
 
## Calibration Guide

The system may require calibration depending on the ambient lighting conditions and the distance between the laser and phototransistor. If false alarms occur or motion is not detected reliably, adjust the following values in the code: 
```
BEAM_MIN – minimum light level required for a valid beam.
MOTION_DROP – amount by which the light level must decrease before an intrusion is detected.
```
## Operating Instructions

To use the system: 
1. Power on the ESP8266 
2. Align the laser or light beam with the phototransistor. 
3. Press the button to arm the system. 
4. Interrupt the beam to trigger the alarm. 
5. Press the button again to disarm.
   
## Installation Instructions

**Step 1: Gather the Required Components**
Ensure that you have all the necessary hardware components. See hardware requirements above.

**Step 2: Install the Required Software**
Download and install the Arduino IDE.
Install the ESP8266 Board Package:
Open File → Preferences.
In the Additional Boards Manager URLs field, add:
$ https://arduino.esp8266.com/stable/package_esp8266com_index.json $ 
Open Tools → Board → Boards Manager.
Search for ESP8266 and install the package.
Install the appropriate USB driver (CH340 or CP2102) if your computer does not automatically detect the NodeMCU.

**Step 3: Assemble the Circuit**
Place the ESP8266 NodeMCU on the breadboard.Connect the phototransistor circuit to pin A0.Connect the LED to pin D5.Connect the piezo buzzer to pin D6.Connect the push button to pin D7.Connect all required 3.3V and GND connections.Position the laser module so that it shines directly onto the phototransistor.

**Step 4: Download the Project Code**
Download or clone the project files and open the .ino file in the Arduino IDE. 

**Step 5: Configure the Arduino IDE**
Select Tools → Board → NodeMCU 1.0 (ESP-12E Module).
Select the correct COM Port under Tools → Port.

**Step 6: Upload the Program**
Connect the ESP8266 to your computer using a USB cable.
Click the Upload button in the Arduino IDE.

**Step 7: Verify the Installation**
Open the Serial Monitor.
Set the baud rate to 115200.

**Step 8: Calibrate the System**
Ensure the laser beam is properly aligned with the phototransistor.
Observe the light readings in the Serial Monitor.
If necessary, adjust the following values in the code:
```
BEAM_MIN
MOTION_DROP
```
to achieve reliable motion detection.

**Step 9: Test the System**
Press the button to arm the system.Interrupt the laser beam using your hand or another object. Verify that the LED illuminates and the buzzer sounds. Press the button again to disarm the system.


## Code Explanation
The program begins by defining the pin assignments for the LED, buzzer, and push button, along with two configurable thresholds:
```
BEAM_MIN – the minimum light intensity required to consider the laser beam present.
MOTION_DROP – the minimum decrease in light intensity required to trigger an alarm.
```
Several variables are then initialized to store the current state of the system:
- armed – indicates whether the system is currently monitoring the beam.
- alarmActive – stores whether an alarm is currently active.
- lastButtonState – used to detect button presses.
- lastLight – stores the previous beam intensity reading.


1. Setup Function
- Configures the LED and buzzer as outputs.
- Configures the push button using the internal pull-up resistor.
- Initializes serial communication at 115200 baud.
- Reads the initial light intensity from the phototransistor.
- Displays startup messages on the Serial Monitor.

2. Loop Function
- The loop() function executes continuously and performs the following tasks:
  
**Sensor Reading**
- The system takes ten analog readings from the phototransistor and calculates an average value. This reduces noise and improves detection reliability.

**Button Handling**
- The push button allows the user to arm or disarm the system. When armed, the current light level is stored as the reference beam intensity. When disarmed, all alarms are turned off and monitoring stops.
  
**Beam Monitoring**
- When the system is armed, the current light reading is compared with the previously stored beam intensity. If the following condition is true:
```
lastLight - light > MOTION_DROP
```
the system determines that the beam has been interrupted.


**Alarm Activation**
When motion is detected:
- The LED indicator turns on.
- The buzzer emits an alarm sound.
- The system waits briefly before returning to monitoring mode.


**Baseline Updating**
- If the beam is present, the program updates lastLight so that the system can adapt to small changes in ambient lighting conditions.


## Limitations
Although the system performs well as a simple security solution, it has several limitations:
- The laser and phototransistor must remain properly aligned.
- Strong ambient light or direct sunlight can affect sensor readings.
- Detection sensitivity may need to be manually calibrated for different environments.
- The system monitors only a single beam and therefore protects a limited area.

## Future Improvements
Several enhancements could be implemented to improve the functionality and usability of the system:
- Add Wi-Fi notifications using email, Telegram, or mobile push notifications.
- Develop a web dashboard for remote monitoring and configuration.
- Store intrusion events in a database or cloud platform.Add multiple beam sensors to protect larger areas.
- Implement battery backup for operation during power failures.
- Add a camera module to capture images when motion is detected.
- Integrate the system with smart home platforms and automation services.Add Over-the-Air (OTA) firmware updates for remote software upgrades.
- Implement adjustable sensitivity settings through a user interface.Include a real-time clock to timestamp intrusion events.
- Add data analytics and reporting to track the frequency and timing of detections.Create a mobile application for arming, disarming, and receiving alerts remotely.
  
These improvements would transform the Night Beam Motion Detection System from a simple beam-break alarm into a fully connected IoT security platform.

