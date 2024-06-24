# Acey Deucey Part 1

## Splash @showdialog

Description.

## Setup sprites

Let's start by creating a function that we will use to get our sprites setup.
Remember to call your new function in `on start`!

```blocks
function setupSprites () {
	
}
setupSprites()
```

## Create sprites

Create three sprites that represent the three cards in play.

```block
function setupSprites () {
    let leftSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    leftSprite.setPosition(40, 30)
    let playerSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    playerSprite.setPosition(80, 60)
    let rightSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    rightSprite.setPosition(120, 90)
}
```

## Where's my card?

Hide the middle card.

```block
// @hide
let playerSprite: Sprite = null

playerSprite.setFlag(SpriteFlag.Invisible, true)
```

## There's my card!

Create a function that reveals the card.
(We will do more in this function later!)
Call the function when the player presses the **A** button or the **B** button.

```blocks
controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
    reveal()
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    reveal()
})
function reveal () {
    // @hide
    let playerSprite: Sprite = sprites.create(img`.`, 0)
    playerSprite.setFlag(SpriteFlag.Invisible, false)
}
```

## Good work!

Now, let's add a deck of cards to the game!

```ghost
controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
    reveal()
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    reveal()
})
function reveal () {
    playerSprite.setFlag(SpriteFlag.Invisible, false)
}
function setupSprites () {
    leftSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    leftSprite.setPosition(40, 30)
    playerSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    playerSprite.setPosition(80, 60)
    rightSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    rightSprite.setPosition(120, 90)
    playerSprite.setFlag(SpriteFlag.Invisible, true)
}
let rightSprite: Sprite = null
let leftSprite: Sprite = null
let playerSprite: Sprite = null
setupSprites()
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
fancyText=github:riknoll/arcade-fancy-text.git
```
