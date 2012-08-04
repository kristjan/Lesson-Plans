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
* Open up Game Maker
* From the **File** menu, select **Open**, browse to where you unzipped the files,
  and open `galaga.gmk`

## Stop invading my space

Last time we had some trouble keeping the ship from wandering off the screen.
Let's put a stop to that with a little movement logic.

1. Open up the ship object properties by double-clicking on your `ship` object.
1. For the `<Left>` key event, drag a new
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   **Test Expression** action from the `control` tab
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression-location.png)
    * Set the expression to `x >= 10`
    * Drag it above the existing
      ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) **Move
      Fixed** action
1. Now add an ![](https://github.com/downloads/kristjan/Lesson-Plans/else.png)
   **Else** below the
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) **Move
   Fixed**
1. Back on the `move` tab, add another
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png) **Move
   Fixed** action under the
   ![](https://github.com/downloads/kristjan/Lesson-Plans/else.png) **Else**
    * Leave _Applies to_ on `self`
    * Set the direction to `stop`
    * Set speed to `0`
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/no-moving.png)
1. Now repeat steps 1-4 for the `<Right>` key
    * The
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   **Test Expression**'s expression this time will be `x <= 608`

    ![](https://github.com/downloads/kristjan/Lesson-Plans/stop-at-boundary.png)

![](https://github.com/downloads/kristjan/Lesson-Plans/run.png) **Run** your
game and try to fly your ship off the screen to the left or right. Now it should
stop when it hits the edge.

## Run away!

The baddies are pretty easy to hit; let's have them fly back and forth.

### Moving

1. Open the baddie1 object properties by double-clicking the `baddie1` object.
1. On the ![](https://github.com/downloads/kristjan/Lesson-Plans/create.png)
   event, add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/speed-horizontal.png)
   **Speed Horizontal** move action anywhere
    * Set the speed to `3`

Now the baddies will all fly to the right, right off the screen!

### Zig Zag

To make the baddies move back and forth, we can do a similar thing to how we
stopped our spaceship from flying off the screen.

1. Still with the `baddie1` properties open, click _Add Event_ and add
   ![](https://github.com/downloads/kristjan/Lesson-Plans/other.png)
   _Other > Intersect Boundary_ to `baddie1`. This event will fire whenever a
   baddie touches the edge of the room.
1. From the `control` tab, add our good friend
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-expression.png)
   **Test Expression**
    * Set the expression to `x >= 608`, which is when the baddie is touching the
     right edge of the room.
1. Add an
   ![](https://github.com/downloads/kristjan/Lesson-Plans/execute-code.png)
   **Execute Code** action
    * Click on _Object_ in the top right and select `baddie1` to affect every
      instance of the baddies
    * Type into the code editor `speed = -3` so the baddies will start moving
      left
    * Click the ![]() check to save
1. Repeat steps 2 and 3 for when the baddies touch the left side of the screen
    * The expression for the left side is `x <= 0`
    * This time, set `speed = 3` to move back to the right

![](https://github.com/downloads/kristjan/Lesson-Plans/boundary-logic.png)


Now everyone flies back and forth!

## Firepower

It doesn't seem fair that we can take our sweet time blowing defenseless aliens
out of the sky. Let's give them some artillery too.

### Ready!

1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-sprite.png)
   **New Sprite**. A window will pop up.
    * Name the sprite `badMissile`.
    * Click on _Load Sprite_ and open the file `sprite/badMissile.png` from
      inside the demo files
    * Make sure _Transparent_ is checked
    * Click OK
1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-object.png)
   **New Object**. A window will pop up.
    * Call the new object `badMissile`
    * Select the `badMissile` sprite from the dropdown list
    * Click OK

### Aim!

1. Open the baddie1 object properties by double-clicking the `baddie1` object
   (not the sprite!).
    * Click on the _Add Event_ button and add a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/step.png) _Step >
      Step_ event. This will run every step of the game loop.
    * Drag a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/test-chance.png)
      **Test Chance** from the `control` tab
        * Set sides on the die to `500` so the baddies fire randomly about every
          500 steps, which is once a second or so.
        * Click OK
    * Drag a
      ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
      **Create Instance** from `main1` underneath the
      ![](https://github.com/downloads/kristjan/Lesson-Plans/test-chance.png)
      **Test Chance**
        * Select _Object_ and pick `badMissile` from the dropdown
        * Make sure to check `relative`
        * Click OK
        * Click OK again to close the baddie properties
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/create-bad-missile.png)
1. Open the badMissile object properties by double-clicking the `badMissile`
   object.
1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create.png) **Create**
   event
1. Drag in a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/move-fixed.png)
   **Move Fixed** action
    * Set the direction to Down
    * Set speed to `10`
    * Click OK
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/bad-missile-properties.png)
1. Click _Add Event_ and add an
   ![](https://github.com/downloads/kristjan/Lesson-Plans/other.png) _Other >
   Outside Room_ event
1. Drag in a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy-instance.png)
   **Destroy Instance** action
   * Set _Applies to_ to `self`

1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/collision.png)
   _Collision_ event with your `ship`.
1. Drag in two
   ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy-instance.png)
   **Destroy Instance** actions from the `main1` tab
    * Set one to `self` to blow up the missile
    * Set one to `other` to blow up the ship
    * Click OK to close the missile properties

### Fire!

1. Open the ship object properties by double-clicking the `ship` object.
1. Click _Add Event_ and add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy.png)
   **Destroy** event
1. Drag in a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
   **Create Instance** action from the `main1` tab
    * Set object to `explosion`
    * Set x and y to `-20`
    * Check `relative`
    * Click OK
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/destroy-ship.png)
1. Click OK again to save the ship properties

Now when the `badMissile` hits your `ship`, it explodes!
![](https://github.com/downloads/kristjan/Lesson-Plans/run.png) **Run** your
game and get out of the way!

## Winning and Losing

### Can't win 'em all

1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-sprite.png)
   **New Sprite**. A window will pop up.
    * Name the sprite `gameOver`.
    * Click on _Load Sprite_ and open the file `sprite/gameOver.png` from
      inside the demo files
    * Make sure _Transparent_ is checked
    * Click OK
1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-object.png)
   **New Object**. A window will pop up.
    * Call the new object `gameOver`
    * Select the `gameOver` sprite from the dropdown list
    * Click OK
1. Open the badMissile object properties by double-clicking the `badMissile`
   object.
1. On the ![](https://github.com/downloads/kristjan/Lesson-Plans/collision.png)
   _Collision_ event with your `ship`, add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
   **Create Instance** from `main1`
    * Set object to `gameOver`
    * Set x to `130`
    * Set y to `500`
    * Click OK
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/create-game-over.png)
1. Click OK again to save the badMissile properties


### Hooray!

1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-sprite.png)
   **New Sprite**. A window will pop up.
    * Name the sprite `youWin`.
    * Click on _Load Sprite_ and open the file `sprite/youWin.png` from
      inside the demo files
    * Make sure _Transparent_ is checked
    * Click OK
1. Create a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/new-object.png)
   **New Object**. A window will pop up.
    * Call the new object `youWin`
    * Select the `youWin` sprite from the dropdown list
    * Click OK
1. Open the goodMissile object properties by double-clicking the `goodMissile`
   object.
1. Select the ![](https://github.com/downloads/kristjan/Lesson-Plans/collision.png)
   _Collision_ event with `baddie1`
1. Add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/test-instance-count.png)
   **Test Instance Count** action from `control`
    * Set the object to `baddie1`
    * Leave number at `0`
    * Leave operation at `Equal to`
    * Click OK
1. Add a
   ![](https://github.com/downloads/kristjan/Lesson-Plans/create-instance.png)
   **Create Instance** from `main1`
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/good-missile-collision.png)
    * Set object to `youWin`
    * Set x to `175`
    * Set y to `100`
    * Click OK
    * ![](https://github.com/downloads/kristjan/Lesson-Plans/create-you-win.png)
1. Click OK again to save the goodMissile properties
