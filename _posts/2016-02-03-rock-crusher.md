---
layout: post
title: Rock Crusher
feature-img: "img/header_02.jpg"
---

> Rock Crusher is a match-three game for Pebble smart-watches where you swap neighbouring rocks to get at least three of the same type in a row.

![Rock Crusher]({{ site.baseurl }}/img/rc_1.png)

## Rock Crusher

Match-three games are a fun coding exercise and trying to invent novel special moves leads to interesting emergent game play effects as different combos interact with each other.

Rock crusher utilises the Pebble's accelerometer as an input method which works well as a cursor to select squares on the grid and indicate the direction to swap. A difficulty curve is obtained in two ways, first the number of pieces in play increases every few levels up to 8 in level 12 and above. Second, the points required to go up a level increase exponentially (115% of the previous level's requirement) whereas the point bonus gained from special moves scales multiplicatively with the level and points from basic moves (match-3 and match-4) only scale additively, soon making them contribute very little.

Controls:
 * Move the cursor with the _right_ and _down_ buttons, or _tilt_ your wrist.
 * Enter _swap_ mode by pressing the _up_ button.
 * In _swap_ mode, choose the direction to swap with the _up_, _down_, _left_ or _right_ button, or _tilt_ your wrist.
 * When not in _swap_ mode, press the _left_ button to save and exit.
 
Specials:
 * Match four rocks in a row to make a Pearl, which can match any colour of rock. Hence a double Pearl match is impossible.
 * Match a rock in two directions to make Black Powder which will blow up nearby rocks of the same type that it is matched with.
 * Match five rocks in a row to blast all of that rock type.
 * Match two Black Powder to cause a mighty explosion.
 * Match a Pearl with Black Powder to wipe out the row and column.

![Rock Crusher screenshot]({{ site.baseurl }}/img/rc_2.png)

## Download and Source Code 

Rock Crusher is written in C and is available on Github.

[Download PBW File]({{ site.baseurl }}{% link /files/RockCrush.pbw %}){: .button}  
[Rock Crusher on Pebble Apps](https://apps.getpebble.com/en_US/application/56acfea45319ec52a600003c){: .button}  
[Rock Crusher on Github](https://github.com/timboe/RockCrush){: .button}  
