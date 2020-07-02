---
layout: worksheet
title: Psychophysics Lab
---

## 1. Recap Arduino pinout

Arduino in lattepanda is great. It’s cheap, easy to use, and comes pre-assembled with a lot of useful tools for data acquisition and control. Let’s get started…

![LattePanda Pinout Diagram](http://www.lattepanda.com/wp-content/uploads/2016/06/PINOut-diagram.png)

## 2. Flicker Fusion Threshold

The flicker fusion threshold, or flicker fusion rate, is a concept in the psychophysics of vision. It is defined as the frequency at which an intermittent light stimulus appears to be completely steady to the average human observer.

###### what is your fusion frequency?

### Task 2.1: Stimulus and Measuring Devices

* Connect a Digital LED Module to the Digital Pin 9

<img src="https://dfimg.dfrobot.com/data/DFR0021/20140812/G/_DSC0406.jpg" width="50%" />

### Task 2.2: Uploading Flicker Fusion code to your arduino

* Run the Arduino software (Arduino.exe), and set the following options:
  - Tools->Board: Arduino Leonardo
  - Tools->Serial Port: (The COM port on which the arduino is connected…try a few.)
* Open the **Flicker.ino** code that is on the google drive
* Upload the code to the Arduino

### Task 2.3: Interfacing Bonsai with Arduino

* Open the **Flicker.bonsai** workflow that is on the google drive
* Change the serial port of **SerialStringWrite** to match the COM port of the Arduino
* Run the workflow
* Try changing the value of the **Int** Source to change the flicker frequency.

### Task 2.4: Experimental Protocol and Data Collection

If you don’t notice the LED flickering On and Off, then it must be flickering faster than your psychophysical “fusion frequency”, the frequency beyond which you can no longer detect the blinking.

###### (Congratulations, you just did your first neuroscience experiment with an Arduino!)

## 3. Simple Response Time Task

There is just one stimulus, and when it appears, you need to respond as fast as you can by pressing the button.

### Task 3.1: Stimulus and Measuring Devices

* Keep the Digital LED Module connected to the Digital Pin 9
* Connect a Digital Push Button to the Analog Input 0
* Connect the pin using a Jumper wire

<img src="https://2betrading.com/1313-large_default/module-digital-push-button.jpg" width="30%">

### Task 3.2: Uploading Standard Firmata Example to your arduino

* Run the Arduino software (Arduino.exe), and set the following options:
  - Tools->Board: Arduino Leonardo
  - Tools->Serial Port: (The COM port on which the arduino is connected…try a few.)
* Open the File > Examples > Firmata > StandardFirmata.
* Find the line `unsigned int samplingInterval = 19;` and change the number to 10.
* Upload the code to the Arduino

### Task 3.3: Interfacing Bonsai with Firmata

* In Bonsai Open a **New Project**, and save it as ReactionTime.bonsai
* From the toolbox find and insert an **AnalogInput** Source.
  - Change the serial port of **AnalogInput** to match the COM port of the Arduino
  - Change the input pin to match the pin where you connected the digital push button.
* Run the workflow and check if you can detect the push button action.
* Stop the bonsai workflow
  - From the toolbox find and insert another **AnalogInput** Source.
  - Change the serial port of **AnalogInput** to match the COM port of the Arduino
  - Change the input pin to  the analog input 1, where you connected the jumper wire
* From the toolbox, find and insert a **Boolean** source.
* From the toolbox, find and insert a **DigitalOutput** sink and connect the **Boolean** source to it.
* Run the workflow and change the Value of the **Boolean** source to turn the LED on and off.

### Task 3.4:Experimental Protocol and Data Collection

* From the toolbox, find and insert a CsvWriter sink after the first analog input source.
* Change the FileName of the CsvWriter to `Response.csv`. Change the Suffix to Timestamp.
* From the toolbox, find and insert another CsvWriter sink after the second analog input source.
* Change the FileName of the CsvWriter to `Stimulus.csv`. Change the Suffix to Timestamp.
* Run the workflow and select one person to activate the stimulus, and another person to respond. Run through the following protoco
  - The person controlling the stimulus will randomly choose a time to activate the LED
  - The person responding to the stimulus should hold the push button in their hands, and as fast as possible press the button as soon as the LED comes on.
    * Make sure that the person responding does not see the person activating the LED.
  - Repeat 5 times to make sure everyone is used to the task
  - After the training phase, the person responding should press the button 3 times in a row to mark when the experiment starts.
  - Repeat the experiment 5 times to record the actual response times.
* Stop the workflow and change between different members of the group to collect the response times from everyone.
