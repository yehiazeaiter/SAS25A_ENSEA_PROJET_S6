# Guide to setup and use the ultrasonic sensor HC-SR04 with STM32CubeIDE

## What it is for
This module is used to measure distances between 3 cm and 2 meters (otherwise it loses accuracy)

## Constitution
The HC-SR04 ultrasonic module is equiped with two main parts, an ultrasonic transmitter, and an ultrasonic receiver. It contains 4 pins : 
- 5V pin to power the module
- Trigger pin to control the transmitter
- Echo pin to read the receiver
- GND pin

![Ultrasonic sensor](https://github.com/user-attachments/assets/e8e98ddf-b7d6-4d03-a4e9-3f3115e92b43)

## How it works
The ultrasonic transmitter sends periodic ultrasonic pulses of 10 μs period. Upon detecting an object, these waves are reflected towards the receiver. Therefore, the time it takes for these waves to travel to the object forth and back is used to calculate the distance.

![Ultrasonic waves](https://github.com/user-attachments/assets/3416a6c6-576b-4ad3-bb4c-a6a48faab96d)
*Image credit : teachwithict*

## Pin setup
- 5V pin should be connected to a 5V power supply (can be drawn from the STM)
- Trigger pin should be connected to the STM in GPIO Output mode
- Echo pin should be connected to the STM in GPIO Input mode
- The GND pin should be connected to the GND node of the circuit

## Visualization 
In order to write the necessary STM code to correctly use this module, we have to understand what we should code precisely.
There are mainly two things :
- Pulse generation with the transmitter
- Reading the echoed signal with the receiver



## Pulse generation
In order to generate pulses, we are going to use some STM timer 
