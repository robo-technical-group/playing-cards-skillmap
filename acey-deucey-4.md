# Acey Deucey Part 4

## Splash @showdialog

Description.

## Ooh! Fancy!

Let's add some instructions.
Instead of using `game.splash()`, let's use a fancy text sprite!
Add it to the `setupSprites()` function.

```block
function setupSprites () {
    let leftSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    leftSprite.setPosition(40, 30)
    let playerSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    playerSprite.setPosition(80, 60)
    let rightSprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    rightSprite.setPosition(120, 90)
    playerSprite.setFlag(SpriteFlag.Invisible, true)
    // @highlight
    let textSprite: TextSprite = textsprite.create("A = In Between  B = Not", 0, 9)
    // @highlight
    textSprite.setPosition(80, 115)
}
```

## Is everything in order?

In `reveal()`, let's first calculate whether the cards are in the correct order.
Remember that there are two possibilities.

```block
function reveal () {
    // @hide
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @hide
    let leftCard: Card = theDeck.nextCard
    // @hide
    let playerCard: Card = theDeck.nextCard
    // @hide
    let rightCard: Card = theDeck.nextCard
    lowToHigh = leftCard.faceValue < playerCard.faceValue && playerCard.faceValue < rightCard.faceValue
    highToLow = leftCard.faceValue > playerCard.faceValue && playerCard.faceValue > rightCard.faceValue
    inOrder = highToLow || lowToHigh
}
```

## Which did you pick?

The player presses **A** or **B** to indicate their choice.
We need to capture that information.

```block
// @hide
function reveal () {
}
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    playerChoseInBetween = true
    reveal()
})
controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
    playerChoseInBetween = false
    reveal()
})
// @hide
let playerChoseInBetween = false
```

## Do we match?

Did we win? If so, then start a new round! If not, then end the game.

```block
// @hide
function startRound () {
}
function reveal () {
    // @hide
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    // @hide
    let leftCard: Card = theDeck.nextCard
    // @hide
    let playerCard: Card = theDeck.nextCard
    // @hide
    let rightCard: Card = theDeck.nextCard
    lowToHigh = leftCard.faceValue < playerCard.faceValue && playerCard.faceValue < rightCard.faceValue
    highToLow = leftCard.faceValue > playerCard.faceValue && playerCard.faceValue > rightCard.faceValue
    inOrder = highToLow || lowToHigh
    // @hide
    playerChoseInBetween = false
    // @highlight
    if (playerChoseInBetween == inOrder) {
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
        info.changeScoreBy(1)
        startRound()
    } else {
        pause(1000)
        game.gameOver(false)
    }
}
```

## Hide me!

Oops ... notice something wrong?
Move the block that makes the player's card invisible to the start
of `startRound()`.

```block
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
    // @hide
    let playerSprite: Sprite = sprites.create(img`.`, 0)
    // @highlight
    playerSprite.setFlag(SpriteFlag.Invisible, true)
}
```
## Done

Great work!

Now, go make it your own!

```template
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

```ghost
function setupDeck () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
}
controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
    playerChoseInBetween = false
    reveal()
})
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    playerChoseInBetween = true
    reveal()
})
function reveal () {
    playerSprite.setFlag(SpriteFlag.Invisible, false)
    lowToHigh = leftCard.faceValue < playerCard.faceValue && playerCard.faceValue < rightCard.faceValue
    highToLow = leftCard.faceValue > playerCard.faceValue && playerCard.faceValue > rightCard.faceValue
    inOrder = highToLow || lowToHigh
    if (playerChoseInBetween == inOrder) {
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
        info.changeScoreBy(1)
        startRound()
    } else {
        pause(1000)
        game.gameOver(false)
    }
}
function setupSprites () {
    leftSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    leftSprite.setPosition(40, 30)
    playerSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    playerSprite.setPosition(80, 60)
    rightSprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    rightSprite.setPosition(120, 90)
    textSprite = textsprite.create("A = In Between  B = Not", 0, 9)
    textSprite.setPosition(80, 115)
}
function startRound () {
    leftCard = theDeck.nextCard
    leftSprite.setImage(theDeck.getCardImage(leftCard, CardSpriteSize.Size32x32))
    playerCard = theDeck.nextCard
    playerSprite.setImage(theDeck.getCardImage(playerCard, CardSpriteSize.Size32x32))
    rightCard = theDeck.nextCard
    rightSprite.setImage(theDeck.getCardImage(rightCard, CardSpriteSize.Size32x32))
    playerSprite.setFlag(SpriteFlag.Invisible, true)
}
let textSprite: TextSprite = null
let rightSprite: Sprite = null
let leftSprite: Sprite = null
let inOrder = false
let highToLow = false
let rightCard: Card = null
let playerCard: Card = null
let leftCard: Card = null
let lowToHigh = false
let playerSprite: Sprite = null
let playerChoseInBetween = false
let theDeck: Shoe = null
setupSprites()
setupDeck()
startRound()
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
