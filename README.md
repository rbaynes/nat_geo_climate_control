# National Geographic explorers programming fun.  
July 20, 2017

## Programming challenge
Build a circuit and write the embedded software necessary to control a simple climate.

## What is a control system?
It is a system with a feedback loop that has one or more inputs about the system (sensing) and one or more ways to affect the system (outputs/actuation) to produce a desired state.  [Control theory](https://en.wikipedia.org/wiki/Control_theory)
![Alt text](/closed-loop-control-system.gif?raw=true)

## Simple climate control
We will build a simple system to attempt to control humidity.  The sensor will tell us the relative humidity and we can lower it by controlling the speed of a fan pointed at it.

## Set up your development system
  * Use Windows or Mac PC with USB port.
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
  * [AM2315](https://cdn-shop.adafruit.com/datasheets/AM2315.pdf) temperature and humidity sensor with male pins on its wires.  
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
[image and wiring credits](https://learn.adafruit.com/adafruit-arduino-lesson-13-dc-motors)

## Programming
  1. Overview of the sensor, I2C and its frequency (.5 Hz).
  1. Overview of PWM for the 12V fan (using 5V and a transistor so the digital output is not driving the fan)
  1. Overview of Arduino programming:
    * C++ with utility classes (String, Serial, etc).
    * Embedded, so the only way to get debugging output is from the serial port (or blinking an LED).
    * Why `setup()` and `loop()` ?
  1. Try the two test programs after you wire the circuits:  Sensor test and fan/motor PWM test.
  1. **Using the two test programs, can you write a control program that reads the sensor and uses the fan to reduce (or hold) the humidity at a set level?**  
    * (hint: if you get stuck, open simple_climate.ino to see one implementation)
    * Here is some example output in the serial monitor from one of my tests:
```
Enter the set point for relative humidity (a tenth lower than ambient) [100.00]: 
Temperature: 23.40 C	Humidity: 34.80 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.90 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 36.40 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 36.90 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 36.50 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 36.10 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 35.70 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 35.40 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 35.10 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 35.00 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.80 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.70 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.60 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.60 %	Desired Humidity: 100.00 %	Fan speed: 0
Temperature: 23.50 C	Humidity: 34.60 %	Desired Humidity: 100.00 %	Fan speed: 0
Humidity set point: 34.50
Temperature: 23.50 C	Humidity: 34.60 %	Desired Humidity: 34.50 %	Fan speed: 0
Temperature: 23.50 C	Humidity: 34.60 %	Desired Humidity: 34.50 %	Fan speed: 125
Temperature: 23.50 C	Humidity: 34.90 %	Desired Humidity: 34.50 %	Fan speed: 150
Temperature: 23.50 C	Humidity: 36.10 %	Desired Humidity: 34.50 %	Fan speed: 175
Temperature: 23.50 C	Humidity: 36.30 %	Desired Humidity: 34.50 %	Fan speed: 200
Temperature: 23.50 C	Humidity: 37.40 %	Desired Humidity: 34.50 %	Fan speed: 225
Temperature: 23.50 C	Humidity: 37.10 %	Desired Humidity: 34.50 %	Fan speed: 250
Temperature: 23.50 C	Humidity: 37.10 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.50 C	Humidity: 35.90 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.60 C	Humidity: 35.30 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.60 C	Humidity: 34.80 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.60 C	Humidity: 34.50 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.60 C	Humidity: 34.40 %	Desired Humidity: 34.50 %	Fan speed: 230
Temperature: 23.60 C	Humidity: 35.90 %	Desired Humidity: 34.50 %	Fan speed: 205
Temperature: 23.60 C	Humidity: 36.10 %	Desired Humidity: 34.50 %	Fan speed: 230
Temperature: 23.60 C	Humidity: 35.80 %	Desired Humidity: 34.50 %	Fan speed: 255
...
Temperature: 23.50 C	Humidity: 34.40 %	Desired Humidity: 34.50 %	Fan speed: 255
Temperature: 23.50 C	Humidity: 34.30 %	Desired Humidity: 34.50 %	Fan speed: 230
Temperature: 23.50 C	Humidity: 34.20 %	Desired Humidity: 34.50 %	Fan speed: 205
Temperature: 23.50 C	Humidity: 34.10 %	Desired Humidity: 34.50 %	Fan speed: 180
Temperature: 23.40 C	Humidity: 34.00 %	Desired Humidity: 34.50 %	Fan speed: 155
Temperature: 23.40 C	Humidity: 34.00 %	Desired Humidity: 34.50 %	Fan speed: 130
Temperature: 23.40 C	Humidity: 34.10 %	Desired Humidity: 34.50 %	Fan speed: 105
Temperature: 23.40 C	Humidity: 34.10 %	Desired Humidity: 34.50 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.10 %	Desired Humidity: 34.50 %	Fan speed: 0
Temperature: 23.40 C	Humidity: 34.20 %	Desired Humidity: 34.50 %	Fan speed: 0
```

## Stretch goal / fun / homework
  * Add in the LED panel.
  * How can we improve this control system?
  * Make it more accurate (hold the desired point longer)?
  * Make it more responsive?
