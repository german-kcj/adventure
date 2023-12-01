 # Lesson Plan: MakeCode Arcade Game Development Introduction

## Objective
By the end of this lesson, students will be able to create a game using MakeCode Arcade that incorporates core game mechanics, enemy AI, scoring, timers, and additional features such as sound and visual effects.

## Materials
- Access to the [makeCode Arcade](https://arcade.makecode.com) web platform. 
- Access to a projector or screen for demonstration.
- Handouts or access to online resources for reference.
- **RECOMENDED**: Create a makeCode account to save and share your creations.

## Target Audience
Teens with little or no familiarity with programming concepts.

## Lesson Outline

### Introduction
- Welcome and introduce the concept of game development with MakeCode Arcade.
- Explain that we will create a game with multiple features and levels.
- Demo a completed version of the game and briefly introduce the core components of the game.

### LEVEL 1 - Core Game Mechanics 
#### 1.1. Setting Up the Player1 Sprite
   - Show how to create a ``||sprites:Player1 sprite of kind Player||``.
   - Add a ``||controller:block||`` to allow controling the **Player1** sprite with the arrow keys or buttons.
   - Explain the option to keep the **Player1** within the screen or handle when it leaves the screen.
   - Add the the ``||sprites:block||`` to keep the **Player1** within the screen.
   - Test the game.  You should see and be able to control the Player1 Sprite.

   ```blocks
   let Player1 = sprites.create(img`
    . f f f . f f f f . f f f . 
    f f f f f c c c c f f f f f 
    f f f f b c c c c b f f f f 
    f f f c 3 c c c c 3 c f f f 
    . f 3 3 c c c c c c 3 3 f . 
    . f c c c c 4 4 c c c c f . 
    . f f c c 4 4 4 4 c c f f . 
    . f f f b f 4 4 f b f f f . 
    . f f 4 1 f d d f 1 4 f f . 
    . . f f d d d d d d f f . . 
    . . e f e 4 4 4 4 e f e . . 
    . e 4 f b 3 3 3 3 b f 4 e . 
    . 4 d f 3 3 3 3 3 3 c d 4 . 
    . 4 4 f 6 6 6 6 6 6 f 4 4 . 
    . . . . f f f f f f . . . . 
    . . . . f f . . f f . . . . 
    `, SpriteKind.Player)
controller.moveSprite(Player1)
Player1.setStayInScreen(true)
```

#### 1.2. Creating and Placing Fruit
Continue adding to the current code within the ``||loops: on start||`` block the following:
   - Create a ``||sprites:Fruit sprite of kind Food||``.
   - Try to ``||scene:place it randomly||`` on the screen. *This will not work as expected, as we have not defined a **Tilemap**. *
   - Introduce the concept and add a ``||scene:tilemap||`` for random placement.
    
  ### ~hint 

    - Make sure that the ``||scene:tilemap||`` is **10 by 8 units**.  Change the size in the Tilemap Editor.
    - For now we will leave the ``||scene:tilemap||`` blank.  We'll create our world later on.
    - Make sure that the ``||scene:tilemap||`` is placed before the ``||scene:place it randomly||`` block.

### ~

  ```block
  // @hide
  let Player1 = sprites.create(img`
  . f f f . f f f f . f f f . 
  f f f f f c c c c f f f f f 
  f f f f b c c c c b f f f f 
  f f f c 3 c c c c 3 c f f f 
  . f 3 3 c c c c c c 3 3 f . 
  . f c c c c 4 4 c c c c f . 
  . f f c c 4 4 4 4 c c f f . 
  . f f f b f 4 4 f b f f f . 
  . f f 4 1 f d d f 1 4 f f . 
  . . f f d d d d d d f f . . 
  . . e f e 4 4 4 4 e f e . . 
  . e 4 f b 3 3 3 3 b f 4 e . 
  . 4 d f 3 3 3 3 3 3 c d 4 . 
  . 4 4 f 6 6 6 6 6 6 f 4 4 . 
  . . . . f f f f f f . . . . 
  . . . . f f . . f f . . . . 
  `, SpriteKind.Player)
  // @hide
  controller.moveSprite(Player1)
  // @hide
  Player1.setStayInScreen(true)
  
  let Fruit = sprites.create(img`
  . . . . . . . . . . . 6 6 6 6 6 
  . . . . . . . . . 6 6 7 7 7 7 8 
  . . . . . . 8 8 8 7 7 8 8 6 8 8 
  . . e e e e c 6 6 8 8 . 8 7 8 . 
  . e 2 5 4 2 e c 8 . . . 6 7 8 . 
  e 2 4 2 2 2 2 2 c . . . 6 7 8 . 
  e 2 2 2 2 2 2 2 c . . . 8 6 8 . 
  e 2 e e 2 2 2 2 e e e e c 6 8 . 
  c 2 e e 2 2 2 2 e 2 5 4 2 c 8 . 
  . c 2 e e e 2 e 2 4 2 2 2 2 c . 
  . . c 2 2 2 e e 2 2 2 2 2 2 2 e 
  . . . e c c e c 2 2 2 2 2 2 2 e 
  . . . . . . . c 2 e e 2 2 e 2 c 
  . . . . . . . c e e e e e e 2 c 
  . . . . . . . . c e 2 2 2 2 c . 
  . . . . . . . . . c c c c c . . 
  `, SpriteKind.Food)
  tiles.setCurrentTilemap(tilemap`level1`)
  tiles.placeOnRandomTile(Fruit, assets.tile`transparency16`)
```

#### 1.3. Collision Detection - *Player1 catches Fruit*
   - Discuss how to check for Fruit pickup.
   - Explain how to detect collisions between the Player1 and the Fruit.
   - Implement logic to handle the Fruit pickup event.
   - Add the ``||sprites:overlaps ||``event block and make sure that it is checking for sprites of kind **Player** and **Food**.
   - This block will check for as long as the game is running if the sprites of kind Player and Food intersect.
   - Add the ``||destroy||`` block and ensure that ``||otherSprite||`` is selected.  In this case it represents the **Fruit**.
  
    ```blocks
    sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    sprites.destroy(otherSprite)
    })
    ```
    - GIF of how to add the **otherSprite** block to the ``||sprites: destroy||`` block.
    - ![add otherSprite to destroy](https://res.cloudinary.com/garcila/image/upload/v1694377306/arcade_overlap.gif)

