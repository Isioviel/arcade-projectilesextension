# Science Oxford - Extend your Game with Projectiles

## Introduction

This tutorial will add to your introductory game.

In this game, you currently have a player character chased by an enemy character.
The longer you manage to run away, the higher your score.

We will add in the ability to throw things at the enemy to destroy them.

You now have access to **all of the blocks** in MakeCode.

## Throw a projectile
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

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    projectile = sprites.createProjectileFromSprite(img`.`, mySprite, 50, 50)
})
```