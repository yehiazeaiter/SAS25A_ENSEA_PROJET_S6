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

## Visualization 
In order to write the necessary STM code to correctly use this module, we have to understand what we should code precisely.
There are mainly two things :
- Pulse generation with the transmitter
- Reading the echoed signal with the receiver

The pulses look like the following : 

![pulses](https://github.com/user-attachments/assets/511df6e9-b71c-4fbb-ab73-984523617b45)


![zoomed in pulse](https://github.com/user-attachments/assets/cc9aac7f-dd7e-4d8a-acdd-ba5c342f21de)

The signal read on the Echo pin looks like the following :
![echo](https://github.com/user-attachments/assets/f475e4fb-b772-4252-b148-7041a16098b0)

In fact, the Echo signal stays on HIGH level until it receives the ultrasonic wave echo. Therefore, in order to calculate distance with its input, we should calculate the distance an ultrasonic wave travels during the time where it stays high, divided by two, because the wave travels the distance to the object back and fourth.

In the following two sections, we'll see how to do the right setup to finally calculate distance.

## Pin setup
- 5V pin should be connected to a 5V power supply (can be drawn from the STM)
- Trigger pin should be connected to the STM in GPIO Output mode
- Echo pin should be connected to the STM in GPIO Input mode
- The GND pin should be connected to the GND node of the circuit

## Pulse generation
In order to generate pulses, we are going to use some STM timer 
