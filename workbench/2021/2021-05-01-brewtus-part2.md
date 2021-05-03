---
title: Brewtus Build (Part 2)
date: 2021-03-08
grand_parent: Workbench
parent: 2021
nav_order: 96
---

Brewtus isn't exactly potty trained. He leaks out of the hot water wand every now and then. I used that as an opportunity to upgrade to joystick-toggle steam and hot water valves. Along the way, I also wanted to see if there was a way to reduce the amount of water that I had to purge from the wand when it hasn't used for a while.

Here's a hodge-podge list of what I've gathered so far:

- The steam boiler pressure is monitored by a pressurestat that functions as a single-pole dual-throw (SPDT) switch. It is wired to complete the electrical heating circuit when the steam boiler drops below a set pressure.
- The set-pressure of the pressurestat can be manually adjusted on the sensor itself. It is factory set to maintain a boiler pressure of 1.4 to 1.6 bar. Mine currently sits in that range.
- The water level in the steam boiler is maintained by a level probe. It sits around half-full of liquid water.
- The steam wand is served by a copper pipe extending from the top of the boiler while the hot water tap is served by a copper pipe extending from the bottom of the boiler.

When the machine is powering on from a cold start, the steam boiler is at atmospheric pressure due to the open vacuum breaker valve. Because this is below the pressurestat set point, the heating element engages. Once the water begins boiling, rising steam closes the vacuum breaker and pressure begins to build as water continues to vaporize. This continues until the pressurestat reaches its set point. At this point, the boiler is up to temperature and we can assume that the top of the steam boiler is filled with steam.

Assuming that any losses in pressure are negligible while the steam valve is closed, liquid water present at the steam wand indicates that the temperature is dropping enough for steam to condense back into water before exiting the wand. This drop in temperature is most likely happening downstream of the boiler. For a closer look at this path, the following drawing depicts the previous assembly:

<figure><img src="https://raw.githubusercontent.com/alextongue/alextongue.github.io/master/workbench/resources/brewtus/sticky_steam1.jpg" width="800"></figure>

The steam pipe (A) is secured to the existing steam valve by a threaded fitting (B), and a shallow nut (C) secures the entire valve assembly to the stainless steel front panel (D). When the valve is closed, the contents of the steam boiler are restricted to the actual valve orifice (E). I decided to focus first on the front panel: Given its shape as a large sheet of metal, it effectively functions as a heat sink that can easily wick away temperature from the steam path. I figured this is especially likely since it is also in contact with the valve body, which itself requires a lot of energy to rise up to temperature.

I ended up installing a fiber washer in between the valve body and the front panel (F) to decouble the valve body from the panel. I'm not sure how much I was able to reduce the "temperature leakage" with the addition of this washer, since the panel is still in contact with the steam path via its rear. In the new joystick steam valve, there was no lock nut attaching the valve to the panel. Instead there was an adapter that converts the joystick fitting to a flat male thread that mates better with the copper steam pipe. There was a bonded sealing washer that was supposed to be for the rear of the panel, but I decided not to use it because of the same amount of space taken by the fiber washer at the front of the panel. Adding that sealing washer may offer a little more insulation.

<figure>
    <img src="https://raw.githubusercontent.com/alextongue/alextongue.github.io/master/workbench/resources/brewtus/fiberwashers.jpg" width="1500">
    <figcaption>Had to bore out the washers a little to fit around the steam valve thread</figcaption>
</figure>

Aside from the front panel, the valve body is still indirectly radiating heat into the air. And of course, water can also very much accumulate at the steam wand, which is another unfortunately long shape with low thermal mass. The previous owners had already installed a no-burn wand, which consists of a high-temperature teflon tube packed into a slightly wider metal wand. This type of wand should, by nature, provide insulation and increase the "reverse potential" for steam to condense, but there has been some anecdotal evidence that espresso machine owners have had better results with steaming after they reverted to the good-'ol-metal-pipe steam wand.

At the end of the day, this entire effort only affects the first half-second or so where I am purging water from the wand. Once steam starts flowing, all parts in local contact with the steam path are up to temperature. In any event, I'm digging the joysticks as a welcome aesthetic flex.

<figure><img src="https://raw.githubusercontent.com/alextongue/alextongue.github.io/master/workbench/resources/brewtus/joysticks.jpg" width="1500"></figure>