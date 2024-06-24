# Acey Deucey Part 3

## Splash @showdialog

Description.

## Round we go!

Create a function that begins a round. Remember to call it from `on start`!

```blocks
function startRound() {
}

// @highlight
startRound()
```

## Pick a card. Any card.

Pull the first card from the deck and store it in a variable.

```blocks
function startRound () {
    // @hide
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @highlight
    let leftCard: Card = theDeck.nextCard
}
```

## Show me the card!

Generate an image for the card and display it in the first sprite.

```blocks
function startRound () {
    // @hide
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @hide
    let leftSprite: Sprite = sprites.create(img`.`, 0)
    let leftCard: Card = theDeck.nextCard
    // @highlight
    leftSprite.setImage(theDeck.getCardImage(aCard, CardSpriteSize.Size32x32))
}
```

## More cards!

Do the same for the other two cards. Be sure to use unique variables
for each of the three cards. We'll need them later on!

```blocks
function startRound () {
    // @hide
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @hide
    let leftSprite: Sprite = sprites.create(img`.`, 0)
    // @hide
    let rightSprite: Sprite = sprites.create(img`.`, 0)
    // @hide
    let playerSprite: Sprite = sprites.create(img`.`, 0)
    let leftCard: Card = theDeck.nextCard
    leftSprite.setImage(theDeck.getCardImage(aCard, CardSpriteSize.Size32x32))
    let playerCard: Card = theDeck.nextCard
    playerSprite.setImage(theDeck.getCardImage(aCard, CardSpriteSize.Size32x32))
    let rightCard: Card = theDeck.nextCard
    rightSprite.setImage(theDeck.getCardImage(aCard, CardSpriteSize.Size32x32))
}
```

## Done!

Good job! In the next part, we'll use some fancy text to display
some instructions!

```template
function setupDeck () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
}
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
function startRound () {
    leftCard = theDeck.nextCard
    leftSprite.setImage(theDeck.getCardImage(leftCard, CardSpriteSize.Size32x32))
    playerCard = theDeck.nextCard
    playerSprite.setImage(theDeck.getCardImage(playerCard, CardSpriteSize.Size32x32))
    rightCard = theDeck.nextCard
    rightSprite.setImage(theDeck.getCardImage(rightCard, CardSpriteSize.Size32x32))
}
let rightCard: Card = null
let playerCard: Card = null
let leftCard: Card = null
let rightSprite: Sprite = null
let leftSprite: Sprite = null
let playerSprite: Sprite = null
let theDeck: Shoe = null
setupSprites()
setupDeck()
startRound()
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
fancyText=github:riknoll/arcade-fancy-text.git
```
