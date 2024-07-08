# War! Part 2

## Splash @showdialog

Now, let's add a deck of cards to the game!

## What's your function?

Let's start by creating a function that we will use to deal the cards.
Remember to call your new function in `on start`!

```blocks
// @hide
function setup () {
	
}

function dealCards () {

}

setup()
// @highlight
dealCards()
```

## Where are the cards?

Now, let's add a deck of cards to the game and shuffle it.

```block
function dealCards () {
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    theDeck.shuffle()
}
```

## What's in a hand?

Let's add a couple of arrays to represent the player hands. We also will need
a discard pile, so we'll create that, too.

```block
function dealCards () {
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    theDeck.shuffle()
    let p1Hand = []
    let p2hand = []
    let discards = []
    // @highlight
    p1Hand = []
    // @highlight
    p2hand = []
    // @highlight
    discards = []
}
```

## Deal the cards!

Now, let's deal the cards to the players. We deal all of the cards in the deck
to the two players evenly.

```block
function dealCards () {
    let theDeck: Shoe = PlayingCards.createPokerDeck()
    theDeck.shuffle()
    let p1Hand = []
    let p2hand = []
    let discards = []
    p1Hand = []
    p2hand = []
    discards = []
    // @highlight
    while (theDeck.hasMoreCards) {
        p1Hand.push(theDeck.nextCard)
        p2hand.push(theDeck.nextCard)
    }
}
```

## Good work!

Next, let's get a round started!

```template
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
setup()
```

```ghost
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

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
