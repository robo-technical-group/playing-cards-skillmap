# War! Part 5

## Splash @showdialog

Time to finish the game!

## Super-duper version of starting a round

If the players tie, then we need to start a war,
where the players play four cards each.

Let's update `startRound()` to accept a number of cards for each player to draw.

```block
function startRound (cardsToDraw: number) {
    // @highlight
    let p1CardsToDraw = cardsToDraw
    // @highlight
    let p2CardsToDraw = cardsToDraw
    let p1DrawSprite: TextSprite = null
    let p2DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    let p1Sprite: Sprite = null
    let p2Sprite: Sprite = null
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    let p1Hand = []
    let p2Hand = []
    info.player1.setScore(0)
    info.player2.setScore(0)
    info.player1.setLife(p1Hand.length)
    info.player2.setLife(p2Hand.length)
}
```

## Player 1 wins!

If Player 1 wins the round, then add the discards to the player's hand.
Clear the discards pile, and then start a new round.

```block
// @hide
function startRound (cardsToDraw: number) {

}
function p1WinsRound () {
    let discards = []
    let p1Hand = []
    for (let value of discards) {
        p1Hand.push(value)
        info.player1.changeLifeBy(1)
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
    }
    discards = []
    startRound(1)
}
```

## Player 2 wins!

Duplicate the code from `p1WinsRound()` and make it apply to Player 2.

```block
// @hide
function startRound (cardsToDraw: number) {

}
function p2WinsRound () {
    let discards = []
    let p2Hand = []
    for (let value of discards) {
        p2Hand.push(value)
        info.player2.changeLifeBy(1)
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
    }
    discards = []
    startRound(1)
}
```

## War!

To begin war, just start a new round with four cards.
Add a sound effect and some instructions, if you like.

```block
// @hide
function startRound (cardsToDraw: number) {

}
function startWar () {
    music.play(music.melodyPlayable(music.bigCrash), music.PlaybackMode.UntilDone)
    game.showLongText("War! Draw 4!", DialogLayout.Bottom)
    startRound(4)
}
```

## Who won?

We don't have a way to end the game yet.
At the end of `startRound()`, make sure players have enough cards to play.
If not, then end the game.

```block
function startRound (cardsToDraw: number) {
    let p1CardsToDraw = cardsToDraw
    let p2CardsToDraw = cardsToDraw
    let p1DrawSprite: TextSprite = null
    let p2DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    let p1Sprite: Sprite = null
    let p2Sprite: Sprite = null
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    let p1Hand = []
    let p2Hand = []
    info.player1.setScore(0)
    info.player2.setScore(0)
    info.player1.setLife(p1Hand.length)
    info.player2.setLife(p2Hand.length)
    // @highlight
    if (info.player1.life() < cardsToDraw) {
        game.gameOver(true)
    }
    // @highlight
    if (info.player2.life() < cardsToDraw) {
        game.gameOver(true)
    }
}
```

## Good work!

You've complete the base game! Now, make it your own!

```template
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

```ghost
function p1WinsRound () {
    for (let value of discards) {
        p1Hand.push(value)
        info.player1.changeLifeBy(1)
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
    }
    discards = []
    startRound(1)
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
    for (let value of discards) {
        p2Hand.push(value)
        info.player2.changeLifeBy(1)
        music.play(music.melodyPlayable(music.baDing), music.PlaybackMode.UntilDone)
    }
    discards = []
    startRound(1)
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
info.player1.onLifeZero(function () {
	
})
info.player2.onLifeZero(function () {
	
})
function startWar () {
    music.play(music.melodyPlayable(music.bigCrash), music.PlaybackMode.UntilDone)
    game.showLongText("War! Draw 4!", DialogLayout.Bottom)
    startRound(4)
}
function startRound (cardsToDraw: number) {
    p1CardsToDraw = cardsToDraw
    p2CardsToDraw = cardsToDraw
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    info.player1.setScore(0)
    info.player2.setScore(0)
    info.player1.setLife(p1Hand.length)
    info.player2.setLife(p2Hand.length)
    if (info.player1.life() < cardsToDraw) {
        game.gameOver(true)
    }
    if (info.player2.life() < cardsToDraw) {
        game.gameOver(true)
    }
}
let instructions: TextSprite = null
let p2Sprite: Sprite = null
let p2DrawSprite: TextSprite = null
let p2Hand: Card[] = []
let p2CardsToDraw = 0
let theDeck: Shoe = null
let p1Sprite: Sprite = null
let theCard: Card = null
let p1DrawSprite: TextSprite = null
let p1CardsToDraw = 0
let p1Hand: Card[] = []
let discards: Card[] = []
setup()
dealCards()
startRound(1)
```

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
