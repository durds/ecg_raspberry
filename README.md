# ECG with Raspberry Pi and AD7705

## Team 3
### 2105361 - Eduardo Moraes

### 2104960 - Kallin Mansur da Costa

## Introduction
As an assignment for the laboratory sessions of the second part of the Real Time Embedded Programing course, the task of measuring an analogue signal with a Raspberry Pi board and an A/D converter.

With many different choices of measurements, the team decided to go for a critical Real Time measurement in which the knowledge of the Digital Signal Processing course could be applied.

## ECG
The electrocardiography is a way of monitoring the heart's rate as well as the chamber positions by sensing the electrical impulses it generates, a very low signal in the millivolt range.

This signal has to be amplified in order to be interpreted, and after this amplification the signal shows a lot of noise, specially the 50Hz from the power supply, which should be filtered out.

## Hardware
The hardware consists of a two stage amplification system, using a differential amplification IC and an operational amplifier and an isolation system.

 

The Amplifier was put together following the design available on biosignals.berndporr.me.uk and gives a total gain of 500. The group was then instructed to isolate this circuit from the A/D and its power supply for safety reasons. This was done by using a pair of optocouplers to produce a differential signal.

 

Having the amplification system powered by four AA batteries, and the output powered by the 3.3v on the Raspberry Pi the output signal had about 1V peak to peak, enough to be measured by the AD7705.

The A/D converter used was an AD7705 connected to the Raspberry via SPI. This A/D was set to measure the signal at a 250Hz sampling rate with its range set from 0v to 2.048v.

## Software
The main software used a Qwt library to display the waveform being sensed by the A/D converter on a screen, the example was a rather simple program which plotted incoming values with no signal processing at a 50Hz sampling rate.

As ECGs need a higher sampling rate, the AD7705 was set to operate at 250Hz. This meant that the refresh rate of the screen could be maintained at 25 FPS, but the plot array would have to be updated once every four milliseconds.

A new thread was started to acquire samples from the A/D converter, run each sample through a High Pass filter to eliminate the DC component and a Band Stop filter at 50Hz to eliminate noise coming from the power supply, after this the samples were fed to the plot array.

Additionally, the program would plot the output to a file and also calculate the BPM and plot it on the console.

## Demo
 https://www.youtube.com/watch?v=sgi8nEUMjbg





## Final Considerations
After analysing the demo ECG taken in the lab it was identified that there was a 90Hz noise present in the samples, coming from an unknown source.

Upon further inspection and MATlab analysis, it was identified that the A/D converter was actually sampling at about 140Hz this meant that simply adjusting the frequency parameters on the filters was enough to produce a clear ECG signal.








With enough time, the heart rate could be also plotted on the main screen of the program using the Qwt library, as well as making a printed circuit board that could reduce noise and improve electrical connections.
