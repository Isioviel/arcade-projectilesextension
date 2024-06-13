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
    sprites.destroy(sprite, effects.halo, 500)
    sprites.destroy(otherSprite, effects.fire, 500)
})
```


## 3: Respawn the enemy
*Stop the game from being too easy, by adding a new enemy once you have destroyed one*

**Duplicate the enemy set-up blocks**
- In your ``||loops:on start||`` loop, you set up your enemy using these blocks:
    - ``||sprites:set mySprite2 to sprite of kind Enemy||``
    - ``||sprites:set mySprite2 position to||``
    - ``||sprites:set mySprite2 follow mySprite||``
- You need to **duplicate** all three of these blocks into the ``||sprites:overlap||`` event block:
    - **Right click** on the block and selecting **Duplicate**.
    - Drag-and-drop the duplicate into the ``||sprites:overlap||`` block, **after** the ``||sprites:destroy||`` blocks.

*If you know how to use functions, you could make this enemy creation code more efficient by defining and calling one.*

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(sprite, effects.halo, 500)
    sprites.destroy(otherSprite, effects.fire, 500)
    let mySprite2 = sprites.create(img`.`, SpriteKind.Enemy)
    mySprite2.setPosition(140, 100)
    mySprite2.follow(mySprite, 50)
})
```

## 4: Adjust the scoring
*How many points should you get for destroying the enemy?*

**Find the blocks**
- Click the ``||info:Info||`` menu.
- Find the ``||info:change score by 1||`` block.
- Drag-and-drop it inside your ``||sprites:overlap||`` loop.

**Adjust the scoring**
- How many points should destroying an enemy give you?
- Do you still want to get points by running away? *These points are given in an ``||game:on game update||`` event loop.*

**Can your player win the game?**
- Look in the ``||info:Info||`` for the ``||info:on score 100||`` block.
- Can you remember how to end the game? This time, you could set it to **WIN**.

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(sprite, effects.halo, 500)
    sprites.destroy(otherSprite, effects.fire, 500)
    let mySprite2 = sprites.create(img`.`, SpriteKind.Enemy)
    mySprite2.setPosition(140, 100)
    mySprite2.follow(mySprite, 50)
    info.changeScoreBy(10)
})
info.onScore(100, function () {
    game.gameOver(true)
})
```

## 5: Respawn the enemy in a Random location
*The game can get more challenging if you do not know where the enemy will respawn!*

**Edit the position block**
- Find the block that controls where the enemy respawns.
- This is the ``||sprite:set mySprite2 position||`` block, in your ``||sprite:overlap||`` event loop.

**Find the new blocks**
- Click the ``||math:Math||`` menu.
- Find the ``||math:pick random 0 to 10||`` block.
- Drag-and-drop it onto the ``||sprite:set mySprite2 position||`` block, so that it replaces the **first** numbers (x).

**Choosing the right numbers**
- By using this block, we are letting the computer choose a random value for x - how far left and right to go.
- The furthest left the enemy can get on the screen is **0**, so keep this as the first number.
- The furthest right the enemy can get is **160**, so replace the second number with this.

**Repeat for y**
- Replace the y number with another ``||math:pick random 0 to 10||`` block.
- This time, fully up is **0** and fully down is **120**.

**Test your code**
- Play your game and test it out - where does the enemy spawn?

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(sprite)
    sprites.destroy(otherSprite)
    let mySprite2 = sprites.create(img`.`, SpriteKind.Enemy)
    mySprite2.setPosition(randint(0, 160), randint(0, 120))
})
```