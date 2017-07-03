# National Geographic explorers programming fun.  July 20, 2017

## Programming challenge
Build a circuit and write the embedded software necessary to control a simple climate.

## What is a control system?
https://en.wikipedia.org/wiki/Control_theory
It is a system with a feedback loop that has one or more inputs about the system (sensing) and one or more ways to affect the system (outputs/actuation) to produce a desired state.

## Simple climate control
We will build a simple system to attempt to control humidity.  

## Set up your development system
  * Windows or Mac PC with USB port.
  * Download and install the [Arduino IDE](https://www.arduino.cc/en/Main/Software).
  * Download [sensor and I2C serial bus Arduino libraries](/arduino_library_for_am2315.tgz) and unzip them to your ~/Documents/Arduino/library directory.
  * Download [example code](/arduino_test_programs.tgz) and unzip it to your /Documents/Arduino directory.
  * Plug the USB cable into your PC and the Arduino board (without any circuits).
  * Start the Arduino IDE, open and compile the test programs.
    * IDE > File > Open... > pick "am2315_test"
    * Click the "upload" right arrow in the menu bar to make sure the sketch compiles and uploads.
    * Click the "serial monitor" button in the upper right corner of the window.
    
## Components
  * Arduino mega 2560 and USB cable.
  * Small bread board and handful of male to male jumper wires.
  * 12V PC fan - look for low current ones.
  * AM2315 temperature and humidity sensor with male pins on its wires.
  * PN2222 transistor.
  * 1N4001 diode.
  * 220 or 270 Ω resistor.

## Wiring the circuit
  * AM2315:
    * Red wire to 5V on Arduino
    * Black wire to GND on Arduino
    * Yellow wire to SDA on Arduino (I2C)
    * White wire to SLC on Arduino (I2C)
  * Breadboard:
    * Put each of the 3 legs of the transistor into their own row (left, middle, right facing the flat side of the transistor)
    * Connect the NON-silver banded end of the diode into the RIGHT leg row of the transistor.
    * Connect the black negative fan wire to the RIGHT leg row of the transistor.
    * Connect the red positive fan wire to the silver banded end of the diode row.
    * Connect the Arduino 5V output to the silver banded end of the diode row.
    * Connect the resistor to the middle transistor row and to a row farther out (to pin 3).
    * Connect the Arduino pin 3 to the far end of the resistor (away from the transistor).
    * Connect the left leg row of the transistor to the Arduino GND.

![Alt text](/arduino_breadboard.jpg?raw=true)
