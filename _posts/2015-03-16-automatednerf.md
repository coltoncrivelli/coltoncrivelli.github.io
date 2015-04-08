---
title: Automated Nerf Turret
layout: post
image: /images/nerf/final.jpg
published: true
---

The final project for my mechatronics class was to modify a Nerf gun giving it the ability to autonomously locate, and fire at, an incandescent bulb. The system relies on a RTOS and tasks, programmed in C++, encoders, phototransistors and much more.

<!-- more -->

![Final Task Diagram]({{ site.url }}/images/nerf/task_diagram.png)

The task diagram depicted above was largely determined as a result of the way that we decided to make our sensing unit. The idea is that the sensing unit first determines the targets location horizontally before proceeding to determining where the target is vertically. As a result of this design choice, there is no need for having two separate tasks that move the system horizontally and vertically at the same time. Similarly, since the system only begins the firing sequence once it's found the target vertically, there is no need for a separate firing task. All of these tasks are encompassed in task seekill (pronounced seek kill) while the control task handles instantiating motor and encoder classes that keep track of position and allow PID control.

![Finite State Machine for Task Seekill]({{ site.url }}/images/nerf/state_diagram.png)

FSM's of each task are provided. The above FSM depicts the entire process of task Seekill.

![Finite State Machine for Task Control]({{ site.url }}/images/nerf/control_fsm.png)

Above is the FSM for task control.

![Encoder]({{ site.url }}/images/nerf/encoder.jpg)

This is the encoder that we made to use with our system. It was 3D printed.

![Power Supply Noise]({{ site.url }}/images/nerf/psu_noise.jpg)

One of the primary issues that we ran into in this project was noise. The above picture shows noise that came from the power supply that we were using and was greatly reduced by adding decoupling capacitors.

![Ghost Interrupts]({{ site.url }}/images/nerf/bounce.jpg)

Any significant amount of jittery noise in the system would cause unintended interrupt counts. Eventually we made solved this by using a Schmitt trigger.

![Circuit Diagram]({{ site.url }}/images/nerf/circuitdiagram.jpg)

The above picture shows the final filtering circuit that we used with our encoder signal. The buffer was very important because the phototransistors we had needed a resistor in the range of 10MEG's to get a useable signal from. Since this resistance is so large, we need a buffer to prevent loading. We were getting noise from the motor and power supply and we found that we needed both a LP filter and the Schmitt trigger to get the encoder counting without errors.

![Imager]({{ site.url }}/images/nerf/imager.jpg)

This is the sensing unit that we put together to sense IR light from the heat lamp that represented our target.

![Imager Focusing Light]({{ site.url }}/images/nerf/focus.jpg)

The above image shows our sensing system working and it shows the effectiveness of the lens for focusing the light until particular phototransistors.

![Line Scan]({{ site.url }}/images/nerf/linescan.jpg)

We laser cut holes for all of the components.

![Automating Nerf Triggering]({{ site.url }}/images/nerf/nerfcontrol.jpg)

This gives some insight into how we automated the triggering of the Nerf gun. We controlled those FETs with our Arduino mega and by toggling some GPI/O pins we could get the gun firing.

![Twisted Wires for Noise Reduction]({{ site.url }}/images/nerf/twist.jpg)

The above picture highlights our use of twisting wires to reduce noise.

![Automated Nerf Turret]({{ site.url }}/images/nerf/final.jpg)

The beautiful final product.
