---
title: Continuous-time Delta-sigma System
layout: post
image: /images/noiseshaping/noise_shaping_scope.png
published: true
---

This was a project for my Advanced Analog Electronics Design course where I built a second-order continuous-time delta-sigma modulator.

<!-- more -->

![Schematic of DAC Configuration]({{ site.url }}/images/noiseshaping/DAC_ckt_dia.png)

The golden rule of EE projects is to break everything down into simple modules and simulate, build, and test them all separately. The above diagram shows a DAC configured with a 5V reference from a LDO regulator and output of the DAC is going through a inverting op-amp with rails at 8 and -8V.


![Output of Configured DAC]({{ site.url }}/images/noiseshaping/output_of_DAC.png)

After hooking up the inputs of the DAC to an arduino uno, the entire operation range of the DAC was verified. 


![DAC and ADC Integration]({{ site.url }}/images/noiseshaping/DAC_ADC_ckt_dia.png)

The above diagram shows the integration of the DAC and the ADC. The error was generated across a POT.


![Noise from External Timer]({{ site.url }}/images/noiseshaping/noise_ext_timer.png)

This was the first output that I got from the schematic shown above. As you can see the output of the DAC is really noisy. After entirely too many hours of debugging, I realized that the noise was coming from an external timer that I was using. I hooked up a 555 as my timer but didn't account for the significant surges of current that resulted in the above noisy DAC output. 


![Noise from Power Supply]({{ site.url }}/images/noiseshaping/noise_psu.png)

More noise! This time the noise was from the power supply itself. After reducing the time scale on the oscope, I found the frequency of the noise and was able to calculate an appropriate sized capacitor to snuff out the noise. 

![Clean ADC and DAC Signal]({{ site.url }}/images/noiseshaping/DAC_ADC_clean.png)

And finally we get the output signal that we were looking for. 

![Diagram of Low Pass Filter]({{ site.url }}/images/noiseshaping/LPF_diag.png)

In order to create a noise-shaping circuit, a 2nd order low-pass filter is going to have to be added to the DAC-ADC loop. The name of the game was to pick a resistor value that gave a gain no greater than 3dB. 

![Simulated Low Pass Filter Response]({{ site.url }}/images/noiseshaping/sim_LPF_response.png)

After picking an R value of 200k, I simulated the filter and found that the gain met the spec. 

![Measured Low Pass Filter Response]({{ site.url }}/images/noiseshaping/LPF_resp_meas.png)

After simulating the low-pass filter, I measured the actual output. The focus was on the frequencies that resulted in a max gain, a gain of unity, and the 3dB gain. 

![Scope Image Emphasizing Pulse Density Modulation]({{ site.url }}/images/noiseshaping/pdm_scope.png)

This is a scope image after everything has been put together. This image emphasizes the interpolation from the second-order continuous-time delta-sigma modulator 


![Scope Image Emphasizing Noise Shaping]({{ site.url }}/images/noiseshaping/noise_shaping_scope.png)

The above image shows the interpolation with a triangle wave input instead of a sine wave, and it shows the FFT so that the noise-shaping can be appreciated/emphasized. 
