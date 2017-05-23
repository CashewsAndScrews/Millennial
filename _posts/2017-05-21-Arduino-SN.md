---
layout: post
title: "An Arduino Supernova"
author: "Ashley & Alex"
categories: outreach
tags: [projects,outreach]
image:
  feature: asn_header.png
---

Last week, we visited a local high school and presented an outreach activity to an astronomy club. We simulated a supernova explosion using an Arduino-powered laser. We covered topics including supernovae astronomy, mathematical modeling and electronics. Below is a summary of what we covered and instructions for the experiment.

## Supernova Astronomy

The suggested reading list is [linked here](https://docs.google.com/document/d/1j4ukehCjw4DgcFCUO1NqYJIRFApPIhSf2DFFfvQsXIo/edit?usp=sharing).

Core-collapse supernovae mark the explosive death of massive stars. These giant stars explode when they run out of usable fuel in their cores to power fusion. Specifically, the stars cannot burn iron because this fusion process is an *endothermic* reaction, meaning that it takes more energy to burn iron than is released. When the core is unable to fuse more elements, it can no longer support itself and collapses due to gravity. However, the collapse is stopped by *electron degeneracy pressure* within the core, and the outer layers rebound, making a supernova. 

Within the supernova *ejecta*, or the stuff that is exploding outward, there is newly formed 56-Nickel, a radioactive element with a half-life of about a week. The radioactive decay of 56-Nickel powers most of the light that we see from the supernova explosion.


We model the *luminosity* of the supernova (or its energy over time) using the first law of thermodynamics:

![first law of thermo](/images/asn_3.png)

The left hand side represents the internal energy as a function of time. The first term on the right hand side is the *heat added* to the system. In this case, that is the radioactive power of the 56-Nickel. The second term is the *work done* by the system to expand the ejecta outward. The third term is the luminosity that we see from the supernova. This luminosity is dictated by a timescale known as the *diffusion time*. The diffusion time roughly tells you how long it takes a photon (or a particle of light) to leave the ejecta. Longer diffusion times generally lead to longer-lasting supernovae, while shorter diffusion times lead to shorter supernovae.

The luminosity of the supernova as a function of time is called the *light curve* of the supernova. We use the light curve to study the supernova's properties.

In our activity, we will explore the effects of a few parameters on the supernova light curve. Specifically, we will first look at how the ejecta mass affects the light curve by modeling a supernova with an Arduino. Then we will look at a more physical model and see how the mass of 56-Nickel and the ejecta's velocity affect the light curve.

## An Arduino Supernova

An *Arduino* is a relatively inexpensive and easy to use microcontroller which can be used to drive outputs and inputs, while interfacing with your computer. In this activity we used the Arduino with a laser attached to an output and a photoresistor attached to the input. A *photoresistor* is a component that lets more or less current through depending on how much light it is exposed to. 

We controlled the laser to flash on and off to represent a supernova. We measured the resistance of our photoresistor as it was exposed to the laser to represent a telescope camera observing a supernova. We also used photoluminescent (or glow-in-the-dark) stars in front of the laser to represent the presence of ejecta mass in the supernova. We compared the light curves with and without ejecta mass.

Below is a diagram of the Arduino circuit.

![arduino](\images\asn_2.png)

And the actual board:

![real arduino](\images/asn_6.png)

The circuit has three main components: the laser, the photoresistor and the button:

First, we control the laser with a PWM output. PWM stands for *pulse width modulation*. In this experiment, we turn the laser on for several milliseconds to represent our supernova explosion. We used a 5V, 405nm, 120mW laser. You need a blue-ish laser for the activity to work well.

Next, the photoresistor is used to measure the supernova. One leg of the photoresistor is attached to 5V and the other is attached to one of the Arduino's analog inputs. The analog input is also attached to ground through a large resistor. The resistance of the photoresistor is determined by how much light is shining on it. This variable resistance forces the analog input to read somewhere between 0V and 5V, depending on the relative resistance between the large resistor (ground) and the photoresistor. When the photoresistor has no light shining on it, its resistance is much larger than the other resistor. Therefore, the analog input reads a voltage close to 0V. When the photoresistor is exposed to light, its resistance drops, and the analog input reads a larger voltage. 

Finally, the button is used to tell the Arduino when to set off a supernova. It is wired in the same way as a photoresistor. But rather than light determining the resistance, the pressing of the button lowers the resistance to trigger the Arduino. This circuit is all placed inside of a black box so that no background light gets picked up by the photoresistor (much like observing the sky at night time!). 

The Arduino code is located on our github [here](https://github.com/CashewsAndScrews/Arduino_SN). See comments in this code to better understand how to adapt it for your Arduino.

You can see [this link](https://docs.google.com/document/d/1PPT-yslngogyZSKpOTCSjdIDPOIj7qzCyF9yDEEWJCY/edit?usp=sharing) for the lab instructions and guiding questions. In short, the students launch a supernova (1) without any ejecta mass, (2) with one ejecta star mass and (3) with two ejecta star masses. Each time, they visually look at the captured data and then record the light curve. A sample light curve is shown below.

![data](/images/asn_5.png)

Finally, we then fit the light curve with a real supernova model that is powered by the radioactive decay of 56-Nickel. The code to fit this data is located on our github [here](https://github.com/CashewsAndScrews/Arduino_SN). The code will rescale the data so that the y-axis corresponds to realistic luminosities (in erg/s).

An example of the best model fit to the one-star data is shown below. Assuming each time step is equal to one day, the model actually returns surprisingly realistic parameters, with an ejecta mass of about 4 solar masses. 

![model](/images/asn_4.png)

## A Model Supernova Applet

Finally, students can explore a more realistic model of supernovae using a web app, shown below. The sliders let the students change each parameter of the light curve independently: the total 56-Nickel mass, the total ejecta mass and the velocity of the ejecta mass. Students were asked to explore how each parameter affects both the overall brightness and duration (or diffusion time) of the supernova. 

<iframe src="http://ashleyvillar.com/slider.html" style="width:750px;height:400px;"></iframe>

If you have any comments or feedback on this project, please feel free to leave a comment below!

*Header image from Wikipedia Commons*

