# War! Part 4

## Splash @showdialog

Next, we'll let the players play a card!

## What's your function?

Let's add an event handler to let Player 1 play a card.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {

})
```

## What do I have left?

Decrement the number of cards that the player needs to draw.
Update the instructions for the player.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
})
```

## Here's my card!

Create a variable to hold a card.
Then, draw the next card from the player's hand.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    // @highlight
    theCard = p1Hand.shift()
})
```

## Let's see your card!

Reveal the player's card by updating the player sprite image.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    theCard = p1Hand.shift()
    let p1Sprite: Sprite = null
    let theDeck: Shoe = null
    // @highlight
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
})
```

## What's the score?

Update the player's score with the card's value.
Also update the player's lives.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    theCard = p1Hand.shift()
    let p1Sprite: Sprite = null
    let theDeck: Shoe = null
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    // @highlight
    info.player1.setScore(theCard.faceValue)
    // @highlight
    info.player1.changeLifeBy(-1)
})
```

## Add to the discards

Add the player's card to the discard pile.
The discards will be added to the winning player's hand.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    theCard = p1Hand.shift()
    let p1Sprite: Sprite = null
    let theDeck: Shoe = null
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player1.setScore(theCard.faceValue)
    info.player1.changeLifeBy(-1)
    let discards = []
    // @highlight
    discards.push(theCard)
})
```

## Did everyone play?

Test if both players played all of the required cards.
We will populate the conditional in the next step.

```block
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    theCard = p1Hand.shift()
    let p1Sprite: Sprite = null
    let theDeck: Shoe = null
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player1.setScore(theCard.faceValue)
    info.player1.changeLifeBy(-1)
    let discards = []
    discards.push(theCard)
    // @hide
    let p2CardsToDraw = 1
    // @highlight
    if (p1CardsToDraw == 0 && p2CardsToDraw == 0) {

    }
})
```

## Let's evaluate!

Create a function that will evaluate the results of the round.
Call the function from the conditional that you created in the prior step.

```block
function eval () {

}
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p1CardsToDraw = 1
    p1CardsToDraw += -1
    let p1DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    let p1Hand = []
    let theCard: Card = null
    theCard = p1Hand.shift()
    let p1Sprite: Sprite = null
    let theDeck: Shoe = null
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player1.setScore(theCard.faceValue)
    info.player1.changeLifeBy(-1)
    let discards = []
    discards.push(theCard)
    // @hide
    let p2CardsToDraw = 1
    if (p1CardsToDraw == 0 && p2CardsToDraw == 0) {
        // @highlight
        eval()
    }
})
```

## What about Player 2?

Duplicate the event handler and modify it to apply to Player 2.

```block
// @hide
function eval () {

}
controller.player2.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    // @hide
    let p2CardsToDraw = 1
    p2CardsToDraw += -1
    let p2DrawSprite: TextSprite = null
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    let p2Hand = []
    let theCard: Card = null
    theCard = p2Hand.shift()
    let p2Sprite: Sprite = null
    let theDeck: Shoe = null
    p2Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player2.setScore(theCard.faceValue)
    info.player2.changeLifeBy(-1)
    let discards = []
    discards.push(theCard)
    // @hide
    let p1CardsToDraw = 1
    if (p1CardsToDraw == 0 && p2CardsToDraw == 0) {
        eval()
    }
})
```

## Getting setup

There are three possibilities at the end of a round.

- If Player 1 has a higher score, then Player 1 wins the round.
- If Player 2 has a higher score, then Player 2 wins the round.
- If the players tie, then start a war.

Create three functions for each of those possibilities.
Then, populate the `eval()` function with a conditional statement
that calls those three functions.

```block
function p1WinsRound () {
	
}
function p2WinsRound () {
	
}
function startWar () {
	
}
function eval () {
    if (info.player1.score() > info.player2.score()) {
        p1WinsRound()
    } else if (info.player1.score() < info.player2.score()) {
        p2WinsRound()
    } else {
        startWar()
    }
}
```

## Good work!

Next, we'll write those functions!

```template
function dealCards () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
    p1Hand = []
    p2Hand = []
    discards = []
    while (theDeck.hasMoreCards) {
        p1Hand.push(theDeck.nextCard)
        p2Hand.push(theDeck.nextCard)
    }
}
function setup () {
    p1Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p1Sprite.setPosition(40, 60)
    p1Sprite.setFlag(SpriteFlag.Ghost, true)
    p1DrawSprite = textsprite.create("Draw 1")
    p1DrawSprite.setPosition(40, 80)
    p2Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p2Sprite.setPosition(120, 60)
    p2Sprite.setFlag(SpriteFlag.Ghost, true)
    p2DrawSprite = textsprite.create("Draw 1")
    p2DrawSprite.setPosition(120, 80)
    instructions = textsprite.create("Press A to draw")
    instructions.setPosition(80, 110)
}
function startRound () {
    p1CardsToDraw = 1
    p2CardsToDraw = 1
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    info.player1.setScore(0)
    info.player2.setScore(0)
    info.player1.setLife(p1Hand.length)
    info.player2.setLife(p2Hand.length)
}
let p2CardsToDraw = 0
let p1CardsToDraw = 0
let instructions: TextSprite = null
let p2DrawSprite: TextSprite = null
let p2Sprite: Sprite = null
let p1DrawSprite: TextSprite = null
let p1Sprite: Sprite = null
let discards: number[] = []
let p2Hand: Card[] = []
let p1Hand: Card[] = []
let theDeck: Shoe = null
setup()
dealCards()
startRound()
```

```ghost
function p1WinsRound () {
	
}
controller.player1.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    p1CardsToDraw += -1
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    theCard = p1Hand.shift()
    p1Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player1.setScore(theCard.faceValue)
    info.player1.changeLifeBy(-1)
    discards.push(theCard)
    if (p1CardsToDraw == 0 && p2CardsToDraw == 0) {
        eval()
    }
})
function p2WinsRound () {
	
}
function eval () {
    if (info.player1.score() > info.player2.score()) {
        p1WinsRound()
    } else if (info.player1.score() < info.player2.score()) {
        p2WinsRound()
    } else {
        startWar()
    }
}
function dealCards () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
    theDeck.isAceHigh = true
    p1Hand = []
    p2Hand = []
    discards = []
    while (theDeck.hasMoreCards) {
        p1Hand.push(theDeck.nextCard)
        p2Hand.push(theDeck.nextCard)
    }
}
controller.player2.onButtonEvent(ControllerButton.A, ControllerButtonEvent.Pressed, function () {
    p2CardsToDraw += -1
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    theCard = p2Hand.shift()
    p2Sprite.setImage(theDeck.getCardImage(theCard, CardSpriteSize.Size32x32))
    info.player2.setScore(theCard.faceValue)
    info.player2.changeLifeBy(-1)
    discards.push(theCard)
    if (p1CardsToDraw == 0 && p2CardsToDraw == 0) {
        eval()
    }
})
function setup () {
    p1Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p1Sprite.setPosition(40, 60)
    p1Sprite.setFlag(SpriteFlag.Ghost, true)
    p1DrawSprite = textsprite.create("Draw 1")
    p1DrawSprite.setPosition(40, 80)
    p2Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p2Sprite.setPosition(120, 60)
    p2Sprite.setFlag(SpriteFlag.Ghost, true)
    p2DrawSprite = textsprite.create("Draw 1")
    p2DrawSprite.setPosition(120, 80)
    instructions = textsprite.create("Press A to draw")
    instructions.setPosition(80, 110)
}
function startWar () {
	
}
function startRound () {
    p1CardsToDraw = 1
    p2CardsToDraw = 1
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    info.player1.setScore(0)
    info.player2.setScore(0)
    info.player1.setLife(p1Hand.length)
    info.player2.setLife(p2Hand.length)
}
let instructions: TextSprite = null
let p2Sprite: Sprite = null
let p2DrawSprite: TextSprite = null
let p2Hand: Card[] = []
let p2CardsToDraw = 0
let discards: Card[] = []
let theDeck: Shoe = null
let p1Sprite: Sprite = null
let p1Hand: Card[] = []
let theCard: Card = null
let p1DrawSprite: TextSprite = null
let p1CardsToDraw = 0
setup()
dealCards()
startRound()
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
