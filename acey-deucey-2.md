# Acey Deucey Part 2

## Splash @showdialog

Description.

## Next function

Now, let's create a function that gets the deck of cards setup for our game.
Don't forget to call the function in `on start`!

```blocks
// @hide
function setupSprites () {
}

function setupDeck () {
}

setupSprites()
// @highlight
setupDeck()
```

## Create a deck of cards

Add a deck of cards to the game.

```block
function setupDeck () {
    let theDeck: Shoe = PlayingCards.createPokerDeck()
}
```

## Time for a shuffle!

The deck is in new-deck order. Let's give it a shuffle!

```block
function setupDeck () {
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @highlight
    theDeck.shuffle()
}
```

## Done

Congratulations! You've added a deck of cards to the game!

But it doesn't do much right now.

In the next part, we will hook up the deck of cards to the sprites!

```template
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

```ghost
function setupDeck () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
}
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
let theDeck: Shoe = null
setupSprites()
setupDeck()
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
fancyText=github:riknoll/arcade-fancy-text.git
```
