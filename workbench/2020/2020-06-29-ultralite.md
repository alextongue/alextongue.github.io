---
title: MOTU Ultralite Mk4
date: 2020-06-29
grand_parent: Workbench
parent: 2020
nav_order: 96
---

<a href="https://motu.com/products/proaudio/ultralite-mk4">I got a new interface</a>! I've been using this for a couple months now, and it's been wonderful.

There was a brief persistent issue where all of the input pad relays and output relays seem to have failed and I was getting a faint and noise-ridden signal from the headphone outputs... but taking the cover off and wiggling the auto power-on jumper made it go away.

Here are some images of its innards:

<figure>
    <img src="https://github.com/alextongue/alextongue.github.io/blob/master/workbench/resources/ultralite/inside.jpg?raw=true" width="1000">
    <figcaption>The little header jumper on the right side,  halfway from the top is the auto power-on jumper. This bypasses the power button and allows for the device to power on and off by simply cutting power. I actually love it when manufacturers put user-configurable parts inside their equipment.</figcaption>
</figure>

And a closer view of the heavily-advertised ESS Sabre DAC. There are several more underneath the daughterboard to the right. The one that is visible is the 8 channel ES9018 (<a href="http://www.esstech.com/index.php/en/products/sabre-digital-analog-converters/audiophile-dacs/classic-sabre-8-channel-dacs/es9018/">web datasheet</a>). 

<figure>
    <img src="https://github.com/alextongue/alextongue.github.io/blob/master/workbench/resources/ultralite/ess_dac.jpg?raw=true" width="1000">
</figure>

## Web Control

In past years, MOTU has been one of the handful of companies to include true internal mixers[^1] in their interfaces. By mixing inputs and outputs using onboard DSP (usually Analog Devices SHARC) this type of mixing eliminates round-trip latencies that would otherwise be introduced by mixing through the host computer.

Probably due to changes in market interest and the growing efficiency of semiconductor supply chains, more OEMs have been adding internal mixing capabilities in their interfaces, but MOTU has long been in the game with CueMix, along with RME's TotalMix. Given the similarities of their names, I wouldn't be surprised if they were direct competitors...

My interface has been designed as part of a newer generation of AVB interfaces (except mine doesn't have AVB connectivity). In terms of hardware, this just means we have bright and pretty white-on-blue LCD screens instead of the old green-on-black segment displays. On the software side, however, a complete redesign was done with their mixing and routing software.

<figure>
    <img src="">
    <figcaption>MOTU Pro Audio Control</figcaption>
</figure>

I can't really speak for the old CueMix, but the newer software (now called "MOTU Pro Audio Control") does feel nice. To control the mixing and routing, everything is accessible only through a browser app. Though there is an installable "discovery app," opening the control panel simply redirects opens a browser tab to port 1280 on localhost. The neat part is that any device with a web browser connected to the local area network can access the interface by simply connecting to the host computer's local IP.

It is worth noting that there is a suite of programs that you could install that enables monitoring of any outputs sent to the computer via oscilloscope, stereo vectorscope, and spectrogram. I wouldn't make critical measurements with this, but this is a neat little set of features developed by MOTU's software folks.

If I could have one criticism, I've found that if the Pro Control page loses focus (e.g. if I switch to another browser tab), it seems like all of the GUI and meter behavior is suspended, maybe to reduce unnecessary throughput. When I switch back to the tab, however, it takes seconds to regain functionality of the buttons. This is where I lose some desired responsiveness, but I think this is still pretty good. Anything more time-critical would probably point me to a more robust digital mixer.

## In Practice

I was able to dig a little deeper into the Ultralite's mixing and networking capabilities to mix speech and live music for a wedding.

Not only was I able to set up a main mix for streaming the audio over a Zoom call on the host computer, but I was also able to set up a separate mix group, which in turn had separate hardware sends for crossing over between PA's and a subwoofer.

For connectivity, I hosted the interface on my friend's laptop, and I routed a "Zoom Mix" to be sent to the computer for the Zoom call. Since we were in a pretty remote location, the host computer was streaming via a WiFi tether to my phone as a hotspot. I wanted to have my hands on his computer to mix, but my friend also needed to keep his hands on the video call. To solve this, I connected my laptop to his via an Ethernet cable, and set up our wired cards to communicate on a separate IPv4 subnet from my phone. I simply pointed my browser to the host IP, and I was able to control and monitor flawlessly!

Sadly, I forgot to snap a picture of this setup, but here's a stripped down setup at the reception area for music playback. Because it wasn't as critical to keep the tethered connection exclusive, I ended up keeping my phone on me and controlling volume from the hotspot subnet it had created. Pretty neat!

<figure>
    <img src="https://github.com/alextongue/alextongue.github.io/blob/master/workbench/resources/ultralite/wedding.jpg?raw=true" width="1000">
    <figcaption>I may benefit from a rack here...</figcaption>
</figure>

If I were using one of their AVB-enabled interfaces, I'm pretty sure the same networking scheme is done by plugging routers and cables directly into the ethernet port on the interface itself, with the only added option the ability to route audio over these networks.

## Future Work

It would be. so. neat. if I could figure out the actual control messages to write my own webapp to monitor or set levels.

MOTU has released a couple guides on controlling their AVB-enabled interfaces through http requests and OSC messages, which could be found on their <a href="https://motu.com/proaudio/index.html">Pro Audio start page</a> under "External control APIs". I'm pretty sure the same protocol is used for my mk4, and I could sniff around on Wireshark or something to figure out more.

Here are the handful of conversations that I've found so far, of people trying to decode the commands:
- Some Motunation forum members were able to <a href="http://www.motunation.com/forum/viewtopic.php?f=14&t=63607">send control messages to change the routing</a>
- A couple more <a href="https://community.cantabilesoftware.com/t/multi-channel-recorded-output-splitting-into-stems-to-send-to-a-daw/2412/23">successful routing commands</a>, done by some Cantabile forum members

## **Footnotes**

[^1]: Some companies offer mixing software with a mixer panel that operates identically to internal mixer software, but the software still requires audio to be routed in and back out of the computer. Although this software acts as a hybrid by introducing some hardware controls (e.g. input pad and possible DAC output trim), mixing processing is still done on the computer. As far as I could tell, Zoom MixEfx is an example of this.