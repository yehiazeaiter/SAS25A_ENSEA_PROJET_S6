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
Essentially, the frequency should be high enough so that it is not able to keep up with the signal fluctuations, otherwise there will be jitters in the movement. 

These two examples were given to explain that we see similar results (smooth output) in different devices, but they're due to different reasons, which is always good to keep in mind.

That being said, a frequency shouldn't be too high for the component either to avoid possible power dissipation and heating problems.
Always refer to the component's datasheet or technical specifications to have the correct frequency range.


***To be continued***
