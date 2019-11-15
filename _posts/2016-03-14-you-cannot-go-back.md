---
layout: post
title: You Cannot Go Back
feature-img: "img/header_03.jpg"
youtubeId: "sGCk4dJMFic"
---

> A Knightmare inspired dungeon crawl for Pebble smart-watches.

{% include tube.html id=page.youtubeId %}

## You Cannot Go Back!

The goal for You Cannot Go Back was to create a small watch based dungeon crawler game which can be finished in a few minutes. A dungeon with three levels of 5-10 rooms per level is created with each room being drawn at random from one of twelve room types and with each room occurring at most once per level. The floor style is used denote the dungeon level. Due to the limitations of the three hardware buttons, the only user input to the game is the choice of which of three rooms to go to next, where some options lead to the next room and others lead to death. Some rooms can generate clues such as a word, symbol or sequence which must be memorised - these clues may then be consumed by rooms deeper in the dungeon where recall of the clue is required to proceed. This provides the games main challenge while other rooms host self-contained puzzles. 

![You Cannot Go Back screenshot]({{ site.baseurl }}/img/ycgb_1.png)

This project required continuous optimisation to stay within the 64 kb allowed RAM for Pebble application binaries and resources. All resources are loaded into memory in initialisation and stored and accessed within a minimal sprite sheet, this gives the application a fixed memory footprint and prevents fragmentation issues from loading and unloading resources. In the final build only a few bytes of RAM are left unallocated. 

![You Cannot Go Back screenshot]({{ site.baseurl }}/img/ycgb_2.png)

Features:
 * Randomly generated three-level dungeon.
 * Twelve types of puzzle room.
   * Maths and spatial puzzle solving.
   * Memory and recall.
   * Skill.
 * Challenges short term recall
   * With up to 5 clues to remember at any one time.
   * Any one of which may be needed to proceed.
 * Quick to play, a typical game is under 5 minutes.

![You Cannot Go Back screenshot]({{ site.baseurl }}/img/ycgb_3.png)

## Download and Source Code 

You Cannot Go Back is written in C and is available on Github.

[Download PBW File]({{ site.baseurl }}{% link /files/YouCannotGoBack.pbw %}){: .button}  
[You Cannot Go Back on Pebble Apps](https://apps.getpebble.com/en_US/application/56e4693181ff036ba9000020){: .button}  
[You Cannot Go Back on Github](https://github.com/timboe/YouCannotGoBack){: .button}  

Uses open game art from [Michele Bucelli](http://opengameart.org/users/buch), [Clint Bellanger](http://opengameart.org/users/clint-bellanger), [Umz](http://opengameart.org/content/blocky-animated-classic-hero-edit), Frank Martinez Jr.
