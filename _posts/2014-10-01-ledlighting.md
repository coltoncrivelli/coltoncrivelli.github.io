---
title: LED Lighting
layout: post
image: /images/lighting/interesting_PWM.png
published: true
---

Intro to lighting
When I moved into my apartment for my senior year at Cal Poly SLO, I realized that I had no suitable secondary light source for my room (i.e. a lamp) so naturally I decided to modify my roommate's 5m LED strip to act as an adjustable light source.

<!-- more -->

![High Level Diagrams]({{ site.url }}/images/lighting/high_lvl_diag.png)

The above high level diagrams give an overview of what I was trying to accomplish. I wasn't interested in making my own power adapter so that's shown as its own block that give me my desired 12V source. The LED dimming system is the part that I was interesting in building and the goal was to create something that would let me dim the normally very bright LEDs in a linear fashion.

![Evaluate Level 1 with Pot]({{ site.url }}/images/lighting/eval_lvl1_pot.png)

Hopefully the above block diagram made you cringe because once of the valuable aspects of this project was learning exactly why one shouldn't use a potentiometer for dimming lights, but it is good to evaluate all design options and to know why the option that you choose is the best option. The issue with dimming light sources with potentiometers is twofold. First using a potentiometer implies when less brightness is desired, resistance increases which decreases the current driving the LEDs, resulting in dimmer LEDs. But this means that all of the excess current is dissipated by a resistor, meaning that this is not efficient. Second, the forward current vs forward voltage of an LED is not linear but exponential, meaning that the dimming will not be linear. So what other design options are there?

![Functional Diagram]({{ site.url }}/images/lighting/functional_diag.png)

Both issues of efficiency and linearity are resolved by dimming the LEDs with pulse-width modulation as opposed to a potentiometer. The idea is that when a dimmer LED is desired, instead of dissipating current through a resistor, the power to the LEDs is switched on and off at a rate faster than human eyes can notice. For this project I chose to ensure that the frequency of the flickering took place no slower than 500Hz because I find that even though this is well above the threshold that humans should see, staring at something for long periods of time that's flickering at a couple hundred Hz can cause irritation. Considering that the primary purpose of the light is for reading at night, I valued a fast PWM rate. Now as long as the duty cycle of the PWM signal can be linearly changed, then this solves both issues.

![Controller Diagram]({{ site.url }}/images/lighting/controller_diag.png)

This black box diagram entires into actual design by choosing to accomplish the PWMing with a 555. I had yet to use a 555 at the time of this project so I was eager to figure out what they're all about. The interesting challenge resided in configuring a 555 to PWM at a set frequency but provide a way to change the duty cycle from roughly 0% to 100%.

![Design]({{ site.url }}/images/lighting/key_design_cons.png)

Alright. If you're still reading then you've managed to make it to the interesting section. The above image is showing quite a lot. First I'm representing a 555 as two comparators interfacing with an SR latch, so that things actually make sense. The magic on the left of the comparators is the additional circuitry that allows variable control over the PWM. To quickly summarize how the 555 operates, the threshold pin is tied to the positive input of one of the comparators while the negative input is tied to two-thirds VCC. The trigger pin is tied to the negative input of the other comparator and is compared to one-thirds VCC. Since the outputs of each comparator represents an input to the SR latch, changing the voltages on the trigger and threshold pins results in either a high or low voltage out of the comparators which means either a high or low signal out of the latch. By tying the threshold and trigger pins together and setting their voltage by a comparator, the time it takes to charge the comparator up to two-thirds VCC and down to one-third VCC becomes directly related to the frequency of the output signal. It should be noted that when the value of the trigger/threshold exceed two-thirds, the NPN is turned on, giving the capacitor a discharge route.

So if all of that makes sense, the idea in this particular schematic is that Rcharge and Rdischarge represent one potentiometer. As Rcharge increases then Rdischarge decreases proportionally, and since these resistor values determine the rate that the capacitor charges at, this means that the output frequency will never change. Instead if Rcharge is increased that means that the capacitor will take longer to charge up and less time to discharge, implying that the output signal will be high for longer then it will be low.

![Simulation]({{ site.url }}/images/lighting/simulation.png)

Before moving on, I did the right thing and actually simulated this concept to make sure it would work!

![Output of Simulation]({{ site.url }}/images/lighting/simulation_output.png)

Output of the simulation, everything is working as expected! We're getting a frequency much higher than 500Hz, the voltage potential across the capacitor is going back and forth between one-third and two-thirds, and the rate at which it charges is directly related to the amount of resistance on Rcharge.

![Max Brightness]({{ site.url }}/images/lighting/max_PWM.png)

This is a scope of the actually built design with the largest charging resistance. The duty cycle is at 99.72% which is pretty awesome.

![Minimum Brightness]({{ site.url }}/images/lighting/min_PWM.png)

It was noticed that with the smallest charging resistance, the lowest obtainable duty cycle was 9.1% which is not nearly as good as the 99.72% that we had on the other side of the spectrum. This is explained because the charging is logarithmic so a it takes the capacitor more time to charge then discharge.

![Proof of Concept]({{ site.url }}/images/lighting/interesting_PWM.png)

This image shows the output signal compared to the capacitor voltage and just does a good job of highlighting most of what I've talked about because you can see the output signal changing when the capacitor voltage hits two-thirds or one-thirds VCC.
