---
layout: post
title: Higgs O'clock
feature-img: "img/header_01.jpg"
---

> The Higgs O'clock watch face simulates the decay of a new Higgs boson every minute and renders how the Higgs decay would appear in the ATLAS Detector.

![Higgs O'clock Banner]({{ site.baseurl }}/img/higgs_1.png)

## Higgs O'clock

A watch face available for Pebble smart-watches. 

In analogue mode, the Higgs decay is fixed to $$WW \rightarrow e\nu\mu\nu$$. The muon (red line) tells the minute and the electron (green) tells the hour.

In digital mode the background event is re-simulated every minute. A decay is randomly chosen from $$H\rightarrow bb$$, $$H\rightarrow \gamma\gamma$$, $$H\rightarrow WW\rightarrow l\nu l\nu$$, $$H\rightarrow WW\rightarrow l\nu qq$$, $$H\rightarrow WW/ZZ\rightarrow qqqq$$, $$H\rightarrow ZZ\rightarrow llll$$ and $$H\rightarrow ZZ\rightarrow llqq$$  where $$l = e,\mu$$ and without giving any consideration to the relative cross-sections of the processes. The final state are spread out around the azimuth to look good, rather than to conserve transverse momentum. All of this is to say, do not use this watch face as a Monte Carlo for your physics analysis.

The circular boarders around the ATLAS sub-detectors will turn from thin to thick as you progress towards your daily average-activity goal.

Features:
 * Digital mode, new Higgs decay every minute.
 * Analogue mode, tells the time with particles.
 * Optional Higgs decay information.
 * Optional calendar.
 * Optional weather, with on-watch caching.
 * Optional battery display.
 * Optional Bluetooth disconnect alert.
 * Optional activity display.

![Higgs O'clock screenshot]({{ site.baseurl }}/img/higgs_2.png)

## Download and Source Code 

Higgs O'clock is written in C and is available on Github.

[Download PBW File]({{ site.baseurl }}{% link /files/ATLASWatch.pbw %}){: .button}  
[Higgs O'clock on Pebble Apps](https://apps.getpebble.com/en_US/application/56ed6ab21644b39a7700000f){: .button}  
[Higgs O'clock on Github](https://github.com/timboe/ATLASWatch){: .button}  

$$H \rightarrow \gamma\gamma$$ candidate event display, [ATLAS Experiment © 2014 CERN](http://atlas.cern/)  
Uses [Slate](https://github.com/pebble/slate) and [gpath-bezier](https://github.com/pebble-hacks/gpath-bezier)
