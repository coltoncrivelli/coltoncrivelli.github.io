---
title: Automated Nerf Turret
layout: post
image: /images/n64/laminator.jpg
published: false
---

On the quest to make my own circuit boards by the toner transfer method, I immediately realized that the standard iron would not cut it. So I purchased this laminator on craigslist for $20 to modify. <!-- more --> The laminator originally ran at two temperatures, neither high enough to melt laser toner onto a circuit board. I modified the laminator to run hotter by tricking its processor with a resistor. The laminator's temperature is controlled by reading a thermistor pressed against the rollers and turning the heating elements on and off. While the laminator was heating up, I measured the temperature of the rollers and the resistance of the thermistor and graphed them. Using this data, I extrapolated what additional resistance was necessary to have the laminator turn off at the temperature I required. I added this resistance, and the laminator heated out of control, full power to the heaters with no regulation. Measuring again in this new area of the thermistor's operation, I found out that I entered a thoroughly non-linear region of resistance for the thermistor. I used this to refine my resistor value and get the laminator to run really hot, but not so hot as to melt everything.

![Toner Transferred board]({{ site.url }}/images/n64/toner.jpg)

This worked, for a couple months. The laminator then went into storage over a summer. After I came back, I attempted to use the laminator again. I turned it on, and let it sit for a while to warm up. I noticed after a while that it was taking a while longer than normal to reach set temp.

![Laminator Failure]({{ site.url }}/images/laminator/melted.jpg)

Poop. Something went wrong. The laminator heated hot enough to seriously melt the sides. I've tried to track down the cause of this out of control heating, and I cannot quite isolate it. The laminator had two thermal fuses, one of which was removed to make it reach the higher set temperature. The second seemed to have no effect, as when I originally hacked the thermistor, it heated out of control with no set temp. It seems that something went wrong with the microcontroller itself and it quit controlling the temperature.

![Laminator Control Board]({{ site.url }}/images/laminator/controlboard.jpg)

At some point I blew a fuse on the board testing for problems. I replaced it with an automotive fuse on the left. It's all I had on hand, deal with it. This picture is from my starting to plot out the board and figure out where the problem is. The plan was to fix or replace the control board, and then replicate the end plates in aluminum with PTFE spacers to reduce heat transfer from the rollers and their extruded covers to the end plates. Taking measurements off a mutilated piece of plastic is hard. At some point, I realized this was an awful lot of effort, and expense, to fix a laminator that I bought for $20. If I completed all this, I'd probably double the cost of the laminator at least just with materials. I also don't make boards very often, and when I do, they're difficult to solder without a silkscreen. I'm not going to call this a failure, but I am letting this one rest. If I need boards in the future, it's plenty reasonable to get them made by OSH Park and their ilk.
