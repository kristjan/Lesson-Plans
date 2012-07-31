# Galaga 2

![](http://upload.wikimedia.org/wikipedia/en/thumb/2/2a/Galaga.png/220px-Galaga.png)

[Galaga](http://en.wikipedia.org/wiki/Galaga) is a classic arcade game that
first appeared in 1979, as a sequal to Galaxian. The goal of the game is to
pilot your space ship, shooting down flying aliens, while avoiding their
missiles. Despite being relased 33 years ago, Galaga and similar spinoffs are
still popular, appearing on smartphones and Xbox Live Arcade.

This tutorial builds more action and adventure onto the
[first Galaga lesson](https://github.com/cameronmcefee/Lesson-Plans/blob/master/galaga/galaga.md).


## Get Game Maker Lite

* [Download for **Windows**](http://www.yoyogames.com/gamemaker/windows)
* [Download for **Mac**](http://www.yoyogames.com/gamemaker/mac)

## Open the project

If you don't have your project from Lesson 1:

* Download the [demo files](https://github.com/kristjan/Lesson-Plans/blob/galaga_part_deux/galaga-2/demo-files.zip?raw=true)
* Unzip them
* Open `galaga.gmk`

## Stop invading my space

Last time we had some trouble keeping the ship from wandering off the screen.
Let's put a stop to that with a little movement logic.

1. Open up the ship object properties by double-clicking on your `ship` object.
1. For the `<Left>` key event, add a new
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-question.png)
   Test Question action from the `control` tab:
    * Set the expression to `x >= 10`
    * Drag it above the existing
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) Move
   action
1. Now add an ![](https://github.com/downloads/kristjan/Lesson-Plans/else.png)
   Else below the
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) Move
1. Back on the `move` tab, add another
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) Move
   Fixed action under the
   ![](https://github.com/downloads/kristjan/Lesson-Plans/else.png) Else
    * Set it to no direction
    * Set speed to `0`

    ![](https://github.com/downloads/kristjan/Lesson-Plans/stop-at-boundary.png)
1. Now repeat steps 1-4 for the `<Right>` key
    * The
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-question.png)
   Test Question's expression this time will be `x <= 608`

![](https://github.com/downloads/kristjan/Lesson-Plans/run.png) Run your game
and try to fly your ship off the screen to the left or right. Now it should stop
when it hits the edge.

