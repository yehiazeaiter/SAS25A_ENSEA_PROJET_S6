# Quick guide to generate a PWM signal with an ST microcontroller

## What is it? 
PWM stands for Pulse-width modulation, which is any method of representing a signal as a rectangular wave with a varying duty cycle. So a PWM signal is simply a rectengular wave with a varying duty cycle.
![PWM signals](https://github.com/user-attachments/assets/e6c0b612-0971-4af8-805d-ff192dba14d5)

*Representation of a PWM signal with different duty cycles*

## Its uses
PWM is mainly used to get **analog like** results with a digital signal, and by digital signal, we mean a signal that switches between two values : 
- LOW which corresponds to 0 V
- HIGH which corresponds to a positive value, commonly 3.3 V or 5 V for microcontrollers

PWM is therefore useful for controlling the average power or or effective voltage delivered by an electrical signal. The higher the duty cycle is, the higher the average is. This is useful in applications like controlling LED brightness, DC motor speed, servo position, heating elements, and more.

The frequency of the signal is also important, it should be chosen correctly so that the electronic device is not negatively affected by the constant ON and OFF switching of the signal.

For example, if you use a PWM signal with a frequency of 10 Hz to control an LED’s brightness, the LED will appear to blink because the human eye can detect such slow flickering. However, if the frequency is increased to 1000 Hz or more, and the duty cycle is 50%, the LED will appear to emit a steady light at reduced brightness due to the eye's persistence of vision.

On the other hand, a motor, being electromechanical, cannot react instantly to rapid changes in the signal, due to inductance and inertia, so when choosing a PWM signal with a high enough frequency, the motor effectively responds to the average power of the PWM signal, rather than each individual pulse. 
Essentially, the frequency should be high enough so that the motor is not able to keep up with the signal fluctuations, otherwise there will be jitters in the movement. 

These two examples were given to explain that we see similar results (smooth output) in different devices, but they're due to different reasons, which is always good to keep in mind.

That being said, a frequency shouldn't be too high for the component either to avoid possible power dissipation and heating problems.
Always refer to the component's datasheet or technical specifications to have the correct frequency range.

## Generating a PWM signal with a microcontroller
For our example, we'll be using STML476RG, but this method shouldn't be very different across different ST microcontrollers.

PWM generation is pretty forward, it is done using timers, in our example, we chose the timer TIM5.
This timer can generate PWM signals in 4 channels, we'll choose channel 2. Do not forget to check the internal clock box.

There are three main parameters affecting our signal, PSC and ARR to choose its frequency, and the Pulse parameter decides the value of the duty cycle.
Our main clock speed is at 80 MHz, we choose PSC = 79 and ARR = 999 to have a timer frequency of 1 kHz.

The Pulse value basically refers the number of timer counts the output stays HIGH within each PWM cycle, therefore, it should be chosen relatively to the ARR value.
For example, to have a 50% duty cycle, we set Pulse to 500.
![tim5 settings](https://github.com/user-attachments/assets/ec644df9-ba5b-4053-a20b-3544f13db29e)

*Screenshot of the TIM5 configuration*

As you can see in the parameters, there are different PWM modes to choose from, for a normal PWM signal, we choose Mode 1. It simply means that the output is HIGH when the timer counter is less than the Pulse value, and LOW when it's equal or greater, so the signal starts by being HIGH then switches to LOW.

Now that the timer is set, we can configure different pins to recieve this signal. For example, we choose PA1 :
![image](https://github.com/user-attachments/assets/ca4feb94-6af9-4cad-93a8-8c0fe7aeaac9)

Save the ioc file so that the IDE apply your configuration. Now you just need to start TIM5 and its PWM generation in the main.c file, in the `main()` function, after the initializations (in the  /* USER CODE BEGIN 2 */ for our case). 
```c
  HAL_TIM_Base_Start_IT(&htim5);
  HAL_TIM_PWM_Start(&htim5, TIM_CHANNEL_2);
```

If you want to change the ARR value (to control the frequency) or the Pulse value (to control the duty cycle) at any moment in the code, you can use the functions `__HAL_TIM_SET_AUTORELOAD(__HANDLE__, __AUTORELOAD__)` and `__HAL_TIM_SET_COMPARE(__HANDLE__, __CHANNEL__, __COMPARE__)`, in our case, the syntax would be :
```c
__HAL_TIM_SET_AUTORELOAD(&htim5, new_arr);               //used to change the ARR value
__HAL_TIM_SET_COMPARE(&htim5, TIM_CHANNEL_2, new_pulse); //used to change the Pulse value
```
And that's it!

Now you can visualise this signal on an oscilloscope, or try to dynamically change the brightness of a LED if you want a first easy application.
Enjoy!
