---
layout: post
title: LIGHTSPEED
feature-img: "img/header_03.jpg"
---

> LIGHTSPEED is a remake of the classic game Asteroids with most of the fun replaced with science!

## Playing the Game

Use **WASD** or the **arrow keys** to navigate your ship. **A/left-arrow** and **D/right-arrow** control your orientation while **W/up-arrow** fires your rear thruster and **S/down-arrow** fires your weaker front thruster. These are powerful thrusters which boost your ship following the equations of [relativistic acceleration](http://math.ucr.edu/home/baez/physics/Relativity/SR/acceleration.html) (your thrusters change your momentum, but your velocity is the hyperbolic tangent of your ships rapidity).

### Arcade Mode
Arcade mode pits you in a perilous [Asteroids](http://en.wikipedia.org/wiki/Asteroids_(video_game)) remake based upon the _survival horror_ genre. Your ship has no weapons (not even a flashlight!) and so your only choice is to dodge the asteroids for as long as possible until Einsteins finally gets the better of you. The asteroids that you will be avoiding are numerous, dangerous and - for the most part - ultra-relativistic.

![Arcade mode]({{ site.baseurl }}/img/ls_1.png)

As the game progresses the speed of light slowly decreases while the speeds of the asteroids increase. In the later portions of the game this will even result in superluminal asteroids! These `tachyoids' show up a scintillating yellow colour. Mentally extrapolate their trajectory and make sure you your ship is _elsewhere_ located otherwise you'll be hit first, then see yourself getting hit moments later. Tachyoids have no respect for [causality](http://en.wikipedia.org/wiki/Causal_contact). The game is over when you have lost all of your lives.

## Sandbox Mode

Sandbox mode lets you play with the game mechanic. Use the controls at the top to add/remove asteroids, set their speed and play with the speed of light. In addition to the normal controls, you can click-and-drag to relocate your ship.

Also shown in the display is your ships fractional velocity of the speed of light, $$\beta$$, and its corresponding [Lorentz factor](http://en.wikipedia.org/wiki/Lorentz_factor), $$\gamma$$. The red line shows which way your ship is oriented and the blue line its current speed and heading.

The option to show **True Positions** (or, _cheat mode_) renders the outline of the _actual_ positions of the asteroids. Lines are also drawn to connect the _true_ positron with any _apparent_ positions, as observed by your ship.

![Sandbox mode with true positions]({{ site.baseurl }}/img/ls_2.png)

As the asteroids move through space, they are continuously emitting photon shells. These shells encode the position and velocity of the asteroid at the time of their creation and subsequently expand outward at the speed of light. The information stored in the photon shells in the immediate vicinity of your ship is used to render the observed scene. By enabling the **Photon Shells** option, the propagation of the shells is visualised.

![Sandbox mode with photon shells]({{ site.baseurl }}/img/ls_3.png)

## Game play Options

In reality, the effects of relativity are intimately interconnected. In this game however, some laws of physics my be conveniently enabled or disabled at your pleasure on the title screen.

### Toroidal Mode

When enabled, the universe is of the classic never-ending variety with the left edge-of-space stitched to the right and the top to the bottom. The topology of such a universe is a _Torus_ or American-doughnut shaped (universally known to be the _worst_ doughnut shape as it precludes the possibility of jammy satisfaction). With Toroidal Mode off, the universe is edged with perfectly elastic walls which instantaneously bounce your ship back. This, technically, involved infinite acceleration, which would kill you were your ship's inertial dampers not connected up to a [Heisenberg compensator](http://en.memory-alpha.org/wiki/Heisenberg_compensator).

Switching off Toroidal mode substantially improves performance in Arcade Mode.

### Length Contraction

One of the ways the universe distorts such that the speed of light remains constant to all observers is the apparent [contraction](http://en.wikipedia.org/wiki/Length_contraction) of the universe at relativistic velocities, along the direction of motion. The true contraction is the reciprocal of the Lorentz factor. However as a concession to keep the game vaguely playable, the magnitude of the length contraction effect is decreased by 90%. 

Turning off space contraction will prevent you getting a headache. And improve performance.

### Relativistic Doppler Shift

![Sandbox mode at a gamma factor of 5.5]({{ site.baseurl }}/img/ls_4.png)

For large relative velocities between your ship and an asteroid, the light from the asteroid is either blue-shifted if it is approaching or red-shifted if it is receding from you. Enabling [Relativistic Doppler Shift](http://en.wikipedia.org/wiki/Relativistic_Doppler_effect) implements this effect. 

Turning off Relativistic Doppler Shift will give a small performance boost.

## Download and Source Code 

[Download LIGHTSPEED.jar]({{ site.baseurl }}{% link /files/LIGHTSPEED.jar %}){: .button}

Run with:
{% highlight bash %}
java -jar LIGHTSPEED.jar
{% endhighlight %}

LIGHTSPEED is written in Java and is available on Github.

[LIGHTSPEED on Github](https://github.com/timboe/Lightspeed){: .button}