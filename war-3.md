# War! Part 3

## Splash @showdialog

Next, let's get a round started!

## What's your function?

Let's start by creating a function that starts a round.
Remember to call your new function in `on start`!

```blocks
// @hide
function setup () {
	
}

// @hide
function dealCards () {

}

function startRound () {

}

setup()
dealCards()
// @highlight
startRound()
```

## How many cards?

There will be times when the players need to play a single card.
At other times, though, the players need to playe more than that.
Let's create some variables that track how many cards each player
needs to play.

```block
function startRound() {
    let p1CardsToDraw = 1
    let p2CardsToDraw = 1
}
```

## Wait, how many cards again?

Now, let's let the player know how many cards to draw.

```block
function startRound() {
    let p1CardsToDraw = 1
    let p2CardsToDraw = 1
    let p1DrawSprite: TextSprite = null
    let p2DrawSprite: TextSprite = null
    // @highlight
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    // @highlight
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
}
```

## Watch my back!

Let's reset the player sprites to show a default image.
We have provided one for you. Feel free to draw your own!

```block
function startRound() {
    let p1CardsToDraw = 1
    let p2CardsToDraw = 1
    let p1DrawSprite: TextSprite = null
    let p2DrawSprite: TextSprite = null
    p1DrawSprite.setText("Draw " + p1CardsToDraw)
    p2DrawSprite.setText("Draw " + p2CardsToDraw)
    let p1Sprite: Sprite = null
    let p2Sprite: Sprite = null
    // @highlight
    p1Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
    // @highlight
    p2Sprite.setImage(playing_card_skillmap_assets.cardBack32x32)
```

## Scores and lives

We're going to use the players' scores to keep track of the cards
that they play.
We are going to use the players' lives to indicate how many cards
they have in their hands.

```block
function startRound() {
    let p1CardsToDraw = 1
    let p2CardsToDraw = 1
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
    // @highlight
    info.player1.setScore(0)
    // @highlight
    info.player2.setScore(0)
    // @highlight
    info.player1.setLife(p1Hand.length)
    // @highlight
    info.player2.setLife(p2Hand.length)
}
```

## Good work!

Next, we'll let the players play a card!

```template
function dealCards () {
    theDeck = PlayingCards.createPokerDeck()
    theDeck.shuffle()
    p1Hand = []
    p2hand = []
    discards = []
    while (theDeck.hasMoreCards) {
        p1Hand.push(theDeck.nextCard)
        p2hand.push(theDeck.nextCard)
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
let instructions: TextSprite = null
let p2DrawSprite: TextSprite = null
let p2Sprite: Sprite = null
let p1DrawSprite: TextSprite = null
let p1Sprite: Sprite = null
let discards: number[] = []
let p2hand: Card[] = []
let p1Hand: Card[] = []
let theDeck: Shoe = null
setup()
dealCards()
```

```ghost
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

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
