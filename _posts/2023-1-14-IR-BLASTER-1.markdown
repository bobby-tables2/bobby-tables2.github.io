---
layout: post
title:  "An IR blaster that controls lights automatically | Development Update 1"
date:   2023-1-14 21:56:00 +0800
categories: jekyll update
---

# What is this project about?

![Picture of the IR blaster setup](/assets/images/2023-1-14-IR-BLASTER-1/ir_blaster.jpg)

Since I have remote controlled ceiling lights, I was given the suggestion to build an infrared blaster that would automatically control their settings like brightness. I chose to do so as I wanted to try my hand at electrical engineering again.

# Keeping track of time

Since I had an Arduino lying around, the first thing I did was to see if I could keep track of time with it, since the remote should vary things like brightness with the hour of the day. Using the **Time** library, the device could approximately keep track of time without any external components. 

I quickly wrote simple routines to adjust the time on the Arduino using the onboard button as well as display the current hour in base 2 using the many side lights (unique to the model of Arduino Uno I used).

# Component assembly

The Arduino is stuck to the breadboard to maximise compactness, and Lego pieces are tied to it to allow it to be placed on an easle.

The 2 main electrical components are the IR transmitter, used to send signals to the lights, and the Light Dependent Resistor (LDR), used to measure the light level.

Both components have a 5V live connection _(red)_ and a ground connection _(black)_ to the Arduino. They don't share breadboard rails because the indicator lights on the IR transmitter inteferes with the LDR if they are too close, but the LDR's power rail is actually connected to the transmitter's power rail by its resistor in order to save space. In addition, the LDR is connected to an analog read port on the Arduino by a _blue_ wire while the transmitter is connected to a pulse-width modulation (PWM) output port by an _orange_ wire.

![A sketch of the circuit diagram of the IR blaster](/assets/images/2023-1-14-IR-BLASTER-1/circuit_diagram.png)

# Arduino scripting

C++ is used to program the Arduino, and I also used the **IRremote** library in addition to the **Time** Library.

The ceiling lights' brightness, yellowness and on/off state can be controlled by remote. Reverse engineering the IR protocol by pointing the off-the-shelf remote at an IR sensor was easy, but the sensor is not included on the board to save space.

The brightness and yellowness values depend on the current hour, and is calculated using the **sin** function. The output looks something like this:

![Sketch of the graph of the birghtness and yellowness functions](/assets/images/2023-1-14-IR-BLASTER-1/light_level.png)

The IR blaster has 2 main methods of adjusting the ceiling lights, from scratch and gradually.

When the IR blaster is first turned on or when the LDR detects that the light has been switched off and on again, the Arduino attempts to reset the brightness and yellowness of the ceiling lights to a value based on a preset hour (if the Arduino was turned on) or the current hour (if the light was  turned on), aka "from scratch".

On the other hand, every hour, the IR blaster adjusts the lights slightly by calculating the values for the previous and current hours and adjusting accordingly to the difference, aka "gradually".

# Improvements

- IR transmitter sensitivity
  - The IR transmitter is weak and often struggles with sending signals even when pointed correctly.
- Automatically turning lights on and off
  - The IR blaster should be programmed to turn the lights on or off at certain hours.
- Control via smartphone
  - A smartphone should be able to send signals to the IR blaster via Bluetooth or WiFi via some interface, bypassing the of-the-shelf remote completely.