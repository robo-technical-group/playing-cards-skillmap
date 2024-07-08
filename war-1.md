# War! Part 1

## Splash @showdialog

Let's get things started with some sprites!

## Setup sprites

Let's start by creating a function that we will use to get our sprites setup.
Remember to call your new function in `on start`!

```blocks
function setup () {
	
}
setup()
```

## Create sprites

Create two sprites that represent each of the players.

```block
function setup () {
    let p1Sprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p1Sprite.setPosition(40, 60)
    p1Sprite.setFlag(SpriteFlag.Ghost, true)
    let p2Sprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p2Sprite.setPosition(120, 60)
    p2Sprite.setFlag(SpriteFlag.Ghost, true)
}
```

## How do I play?

Let's add some instructions to the screen.

```block
function setup () {
    let p1Sprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p1Sprite.setPosition(40, 60)
    p1Sprite.setFlag(SpriteFlag.Ghost, true)
    let p2Sprite: Sprite = sprites.create(playing_card_skillmap_assets.cardBack32x32, SpriteKind.Player)
    p2Sprite.setPosition(120, 60)
    p2Sprite.setFlag(SpriteFlag.Ghost, true)
    // @highlight
    let p1DrawSprite: TextSprite = textsprite.create("Draw 1")
    // @highlight
    p1DrawSprite.setPosition(40, 80)
    // @highlight
    let p2DrawSprite: TextSprite = textsprite.create("Draw 1")
    // @highlight
    p2DrawSprite.setPosition(120, 80)
    // @highlight
    let instructions: TextSprite = textsprite.create("Press A to draw")
    // @highlight
    instructions.setPosition(80, 110)
}
```

## Good work!

Now, let's add a deck of cards to the game!

```ghost
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

```package
playing_card_skillmap_assets=github:robo-technical-group/playing_card_skillmap_assets.git
PlayingCards=github:robo-technical-group/pxt-arcade-playing-cards.git
textsprite=github:microsoft/arcade-text.git
```
