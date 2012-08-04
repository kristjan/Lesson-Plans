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

* Download the [demo files](https://github.com/kristjan/Lesson-Plans/blob/galaga_part_deux/galaga-2/demo-files.zip?raw=true)
* Unzip them
* Open `galaga.gmk`

## Stop invading my space

Last time we had some trouble keeping the ship from wandering off the screen.
Let's put a stop to that with a little movement logic.

1. Open up the ship object properties by double-clicking on your `ship` object.
1. For the `<Left>` key event, add a new
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   Test Expression action from the `control` tab:
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
    * Set it to `stop` direction
    * Set speed to `0`

    ![](https://github.com/downloads/kristjan/Lesson-Plans/stop-at-boundary.png)
1. Now repeat steps 1-4 for the `<Right>` key
    * The
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   Test Expression's expression this time will be `x <= 608`

![](https://github.com/downloads/kristjan/Lesson-Plans/run.png) Run your game
and try to fly your ship off the screen to the left or right. Now it should stop
when it hits the edge.

## Run away!

The baddies are pretty easy to hit; let's have them fly back and forth.

### Moving

1. Open the baddie1 object properties by double-clicking the `baddie1` object.
1. On the ![](https://github.com/downloads/kristjan/Lesson-Plans/create.png)
   event, add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/speed-horizontal.png)
   Speed Horizontal move action
    * Set the speed to 3

Now the baddies will all fly to the right, right off the screen!

### Zig Zag

To make the baddies move back and forth, we can do a similar thing to how we
stopped our spaceship from flying off the screen.

1. Add an
   ![](https://github.com/downloads/kristjan/Lesson-Plans/intersect-boundary.png)
   Intersect Boundary event to `baddie1`. This event will fire whenever a baddie
   touches the edge of the room.
1. From the `control` tab, add our good friend
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   Test Expression
    * Set the expression to `x >= 608`, which is when the baddie is touching the
     edge of the room.
1. Add an
   ![](https://github.com/downloads/kristjan/Lesson-Plans/execute-code.png)
   Execute Code action
    * Set the object to `baddie1` to affect _every_ instance of the baddies
    * Type into the code `speed = -3` so the baddies will start moving left
1. Repeat steps 2 and 3 for the left side of the screen
    * The expression for the left side is `x <= 0`
    * This time, set `speed = 3` to move back to the right


## Firepower

It doesn't seem fair that we can take our sweet time blowing defenseless aliens
out of the sky. Let's give them some artillery too.

### Ready!

1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-sprite.png)
   New Sprite. A window will pop up.
    * Name the sprite `badMissile`.
    * Click on _Load Sprite_ and open the file `sprite/badMissile.png`
    * Make sure _Transparent_ is checked
    * Click OK
1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-object.png)
   New Object. A window will pop up.
    * Call the new object `badMissile`
    * Select the `badMissile` sprite from the dropdown list

### Aim!

1. Open the baddie1 object properties by double-clicking the `baddie1` object.
    * Click on the _Add Event_ button and add a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/step.png) Step
      event. This will run every "step" of the game.
    * Drag a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/test-chance.png)
      Test Chance from the `control` tab
        * Set `sides` to 500 so the baddies fire randomly every 500 steps,
          which is about a second.
        * Click OK
    * Drag a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
      Create Instance from `main1` underneath the
      ![](https://github.com/downloads/kristjan/Lesson-Plans/test-chance.png)
      Test Chance
        * Select `badMissile` from the `object` dropdown
        * Make sure to check `relative`
        * Click OK
1. Open the badMissile object properties by double-clicking the `badMissile`
   object.
1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create.png) Create
   event
1. Drag in a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png)
   Move action
    * Set the direction to Down
    * Set `speed` to 10
1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/collision.png)
   Collision event with your `ship`.
1. Drag in two
   ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy-instance.png)
   Destroy Instance actions
    * Set one to `self` to blow up the missile
    * Set one to `other` to blow up the ship

### Fire!

1. Open the ship object properties by double-clicking the `ship` object.
1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy.png) Destroy
   event
1. Drag in a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
   Create Instance action
    * Set `object` to `explosion`
    * Set `x` and `y` to -20
    * Check `relative`

Now when the `badMissile` hits your `ship`, it explodes!
![](https://github.com/downloads/kristjan/Lesson-Plans/run.png) Run your game
and get out of the way!
