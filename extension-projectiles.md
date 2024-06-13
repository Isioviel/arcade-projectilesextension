# Science Oxford - Extend your Game with Projectiles

## Introduction

This tutorial will add to your introductory game.

We will add in the ability to throw things at the enemy to destroy them.

You now have access to **all of the blocks** in MakeCode, so finding the correct blocks will be more challenging.

## 1: Throw a projectile
*Use button A to throw something*

**Find the blocks to make a new event loop**
- Click into the ``||controller:Controller||`` menu.
- Find the ``||controller:on A button pressed||`` block.
- Drag-and-drop it onto an **empty space** on the screen.

**Find the projectile block**
- Click into the ``||sprites:Sprites||`` menu.
- Find the ``||sprites:set projectile to projectile from mySprite||`` block.
- Drag-and-drop it into the ``||controller:on A button pressed||`` block.

**Edit the projectile**
- *If you renamed your player character earlier, change mySprite to the new name*.
- Click on the grey box to choose what your character throws.
- The two numbers in the block set the **speed** and **direction** the projectile moves.
    - **vx** sets the speed in the left/right direction
        - *set vx to 0 if you only want your player to throw up or down*
        - *set vx to a negative number to throw left, a positive number to throw right*
    - **vy** sets the speed in the up/down direction
        - *set vy to 0 if you only want your player to throw left or right*
        - *set vy to a negative number to throw up, a positive number to throw down*

**Test your game**
- Practice throwing projectiles - do they go where you want them to?
- Edit the speed and direction until you are happy with it.

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    projectile = sprites.createProjectileFromSprite(img`.`, mySprite, 50, 50)
})
```


## 2: Destroy the enemy
*Destroy the enemy when hit*

**Find the blocks to make a new event loop**
- Click the ``||sprites:Sprites||`` menu.
- Choose the ``||sprites:on sprite of kind Player overlaps with sprite of kind Player||`` block.
- Drag-and-drop it onto an **empty space** on the screen.

**Choose the right sprite types**
- Click the **first** ``||sprites:Player||`` option.
- Change it to ``||sprites:Projectile||``.
- Click the **second** ``||sprites:Player||`` option.
- Change it to ``||sprites:Enemy||``.

*The block now controls what happens when a projectile sprite overlaps (or touches) an enemy sprite.*

**Find the blocks**
- Click the ``||sprites:Sprites||`` menu.
- Find ``||sprites:destroy mySprite||``.
- Drag-and-drop this into the ``||sprites:overlap||`` block.
- Drag-and-drop the same block in again, so that you have **two** ``||sprites:destroy||`` blocks.

**Destroy the right sprites**
- You want to destroy the enemy and also the projectile that hit it.
- Look at your ``||sprites:overlap||`` block - there are two round red blocks labelled ``||variables:sprite||`` and ``||variables:otherSprite||``.
- Drag-and-drop ``||variables:sprite||`` onto the **first** ``||sprites:destroy||`` block, to replace ``||variables:mySprite||``.
- Drag-and-drop ``||variables:otherSprite||`` onto the **second** ``||sprites:destroy||`` block, to replace ``||variables:mySprite||``.

![drag-and-drop sprite and otherSprite variables](https://raw.githubusercontent.com/Isioviel/arcade-projectilesextension/master/images/sprite-otherSprite-dragdrop.PNG)

**Test your game**
- Practice destroying the enemy - does it work?

**Change the destroy effect**
- *Make sure that your game works correctly before continuing.*
- Click the ``||sprites:+||`` symbol at the end of the ``||sprites:destroy||`` blocks.
- Choose the effect you want, and test it out.

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    sprites.destroy(otherSprite)
})
```