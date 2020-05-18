---  
title: "XY vs. MS, Exhaustively"
custom_title: true
nav_order: 2
parent: Literature
---

<center>
<h1>XY vs. MS, an Conceptually Exhaustive Comparison</h1>
<h3>alternate title 1: a quick detour/derivation of electroacoustic<b>*</b> transduction</h3>
<h3>alternate title 2: how i learned to use footnotes excessively</h3>
</center>

-----

**Context:** It's 7:17AM EST, sitting at Variety Coffee Roasters on 7th Ave. Drinking a cappuccino and eating a carrot-mango-coconut muffin. I'm alternating between tasting lychee and medicine from the coffee, and the muffin sort of tastes like tortilla chips. Also listening to Isaiah Sharkey's LOVE.LIFE.LIVE album. A good funk.

-----

## XY and MS Microphone Techniques in Comparison ([Hibbing 1989](https://secure.aes.org/forum/pubs/journal/?elib=6065))

Two common methods of stereophonic capture are XY and Mid-Side (MS) pairs.

In an XY pair, two identical directional microphones are pointed with their main pickup axes[^1] separated by some angle. The entire array is then positioned so that the line bisecting each axis is pointed towards the acoustic source to be captured. I think this type of pair is seen more commonly because it's intuitive to see how each mic, pointed in different directions, will pick up sound sources differently[^2].

In a MS pair, a directional microphone is paired with a bidirectional (figure-eight) microphone; designated "Mid" and "Side" channels respectively. The main pickup axis of the Mid microphone is pointed towards the acoustic source to be captured, while the axis of the Side microphone is angled 90 degrees to that of the Mid mic; by convention, the positive convention of the bidirectional mic is oriented 90 degrees clockwise to the Mid axis (to the right).

In the case of MS, it's a little harder to understand how these work without a little head-bending. A lot of it has to do with how the bidirectional Side channel picks up sound from each side. Because a bidirectional microphone diaphragm is open on both ends, a force acting on one side of the diaphragm in one direction induces a voltage in one direction, while a force acting on the opposite side induces a voltage in the opposite direction[^3].

If a plane wave were propagating towards one end of the microphone capsule[^4] (let's call this "front side" of the microphone the positive side, with the wavefront traveling at 0 degree incidence, or on-axis), it would exert a force corresponding to a **positive voltage.**

If the wave were travelling in the opposite direction (180 degrees off-axis.), the force exerted on the negative side of the diaphragm would result in a **negative voltage.**

If the wave were travelling perpendicular to the normal vectors of the diaphragms (90 degrees off-axis), it would exert an equal force to either side, resulting in maximal destructive interference, or **zero voltage**.

Sweeping the angle of incidence of wavefronts from on-axis to 180 degrees off-axis, you would see the change in voltage start at a maximum voltage, drop and cross zero, then continue decreasing to a minimum negative voltage. This is why the bi-directional microphones are also called pressure gradient microphones, as the gradient, or direction of wavefront travel, affects the pickup of the mic. This is also why they're called figure-eight microphones, as the complete 360-degree sweep traces out a figure-of-eight on a polar plot.

In comparison, an omnidirectional microphone consists of a diaphragm is only open on one side. As a result, pressure changes from any direction can only push in one direction. Now the important part: the same concept holds for sinusoidal signals, but magnitude relationships change to phase relationships, ultimately producing frequency-dependent changes in magnitude. This gives rise to the proximity effect, which I'll write in another post.

Hibbing's paper takes off by first explaining that two-dimensional microphones can be decomposed into linear combinations of an omnidirectional and bidirectional source. For example, the ideal cardioid pattern is an equally-weighted sum of an omnidirectional monopole and a bidirectional dipole. Then, each dipole can be further decomposed into a weighted sum of perpendicular dipoles, or orthonormal basis functions. As a result, different XY and MS configurations can be compared with each other by directly comparing the relative weights of omnidirectional and bidirectional components.

Several neat graphs are derived, where Hibbing parameterizes XY pairs with the directivity of each microphone and the angle of separation between pickup axes, then MS pairs with the directivity of the Mid microphone and the relative level of the bidirectional Side microphone. These graphs show XY and MS configurations that are equivalent in directional pickup MS; how the pattern of an XY pair could match with that of an MS pair, and vice versa.

Several other graphs were also given, that DID THIS INSTEAD OF THAT. This was because it was hard to engineer microphones that are continuously variable in directivity, since the acoustic path between front and rear microphones had to be physical varied (there were some interesting labyrinthine solutions, such as the [RCA 77](https://www.aearibbonmics.com/aeas-r84-vs-the-rca-77-whats-the-difference/) and [AEA KU3A](http://recordinghacks.com/microphones/RCA/KU-3A). Folks have since figured out how to delay the signals between oppositely-polarized capsules to achieve the same directivity effect. But even then, there aren't many microphones on the consumer market that have continuously variable directivities. [Here's an example of one](https://patents.google.com/patent/US4354059).

By the way, it's worth noting that in both cases, the microphone capsules of each pair are supposed to be colocated in theory. Because it's impossible to have current microphone capsules (or any discrete objects, for that matter) occupy the same physical space, microphones can be placed one above the other in practice. This offset of a centimeter or two in a direction orthogonal to the direction of capture is negligible.

## Footnotes
<b>*</b>  acoustoelectric? electroacoustic?

[^1]: that is, the ray that originates on the microphone capsule and points in the direction that the microphone is most sensitive to changes in pressure at some standard distance, usually 1m. In the case of a finite planar aperture by which virtually every current microphone capsule can be characterized, this corresponds with the normal vector pointing out of the center of the capsule.
[^2]: ... as long as they aren't perceptually indistinguishable point, line, or plane sources symmetric across the plane that contains both a point on the planar intersection of surfaces of the microphone capsules and the line that bisects the angle between microphone capsules' normal vectors. But I think those rarely happens.
[^3]: Ribbon microphones are an example of a bidirectional microphone, which consist of a conductive film parallel to the magnetic field lines from magnet poles on either side. Current is induced across the foil when a force is applied in the direction normal to the foil. This can be derived from the Faraday-Lenz law. The current signal then passes through some fancy tube or transistor preamp circuitry and is converted to some a voltage in some nominal range, ready to be passed to other equipment.
[^4]: that is, the vector normal to the wavefront and and pointing in the direction of travel is antiparallel to the pickup axis of 
