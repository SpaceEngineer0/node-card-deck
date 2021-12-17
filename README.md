# node-playing-cards

Simple playing card library. Deal, shuffle or create cards easily.

To install and use the module, type `npm install node-deck` in the terminal and add `const nodeDeck = require('node-deck');` in your code.

## Documentation

### Card

Card class

#### constructor

* `_rank` Rank class
* `_suit` Suit class

```js
const card = new Card(new Rank('K', 'King', 13), new Suit('Spades', '\u2664', 1));
```

#### get remainingLength

Returns the number of remaining cards in deck

### displayShort

Returns a string consisting of the card's rank `_shortName` and suit's `_shortName`

```js
card.displayShort        // K♤
```

### displayText

Returns a string consisting of the cards rank `_longName` and suits `_name`

```js
card.displayText        // King of Spades
```

### Deck

Class that epresents a deck of playing cards.

#### constructor

* `_jokerCount` the number of Jokers in the deck. Default `0`
* `_numOfDecks` number of decks in Deck instance. Default `1`
* `_deck` object with cards, ranks, suits and jokers. Default `./src/ddecks/standard`

```js
const Deck = require('node-deck');

var deck = new Deck(3, 2);        // 3 jokers, 2 times the default deck
```

#### deal

Deals a number cards to hand and marks the given cards as `held`.

Arguments:

* `count` default 1 - how many cards to give the hand.
* `hand` array to push the cards.

```js
var hand1 = [];
var hand2 = [];

deck.deal(hand1, 5);        // deals hand1 5 cards
deck.deal(hand2);        // deals hand1 1 card
```

#### dealMul

Deals a number cards to multiple hand and marks the given cards as `held`.

Arguments:

* `count` default 1 - how many cards to give the hands.
* `hands` array of hands to push the cards.

```js
var mul1 = [];
var mul2 = [];

deck.deal([mul1, mul2], 5);        // deals5 cards to both mul1 and mul2
```

#### insert

Insert `Cards` back to the end of the deck and remove them from `deck.held` array. The order of inserted elements will be unchanged.

Arguments:

* `cards` array of Cards.

```js
var cards = [
  new Card(new Rank('Q', 'Queen', 12), new Suit('Clubs', '\u2667', 2)),
  new Card(new Rank('K', 'King', 13), new Suit('Clubs', '\u2667', 2))
]

deck.insert(cards);
```

#### reset

Sets the deck back to 52 cards + Jokers, if the exist. Sets the `deck.held` to an empty array.

```js
deck.reset();
```

#### shuffle

Randomize the order of remaining cards using the **Fisher-Yates Algorithm**.

```js
deck.shuffle();
```

### Rank

Rank class

#### constructor

* `_shortName` name displayed in `displayShort` Card getter.
* `_longName` name displayed in `displayText` Card getter.
* `_sortNum` used to differentiate card ranks.

```js
const rank = new Rank('K', 'King', 13);
```

### Suit

Suit class

#### constructor

* `_name` name displayed in `displayText` Card getter.
* `_shortName` shortName character displayed in `displayShort` Card getter.
* `_sortNum` used to differentiate card suits.

```js
const suit = new Suit('Spades', '\u2664', 1);
```

### sortByRank

Sorts the hand first by ranks, then by suits in the rank. Sorts in ascending order.

```js
var hand = [8♡, 5♧, 8♤, 5♤];

nodeDeck.sortByRank(hand);
// rank phase         => [8♡, 8♤, 5♧, 5♤]
// suit phase (final) => [8♤, 8♡, 5♤, 5♧]
```

### sortBySuit

Sorts the hand first by suits, then by ranks in the suit. Sorts in ascending order.

```js
var hand = [8♡, 5♧, 8♤, 5♤];

nodeDeck.sortBySuit(hand);
// suit phase         => [8♤, 8♡, 5♧, 5♤]
// rank phase (final) => [8♤, 8♡, 5♤, 5♧]
```

## Custom Decks

All custom decks should have their own:

* suits
* ranks
* jokers (if you plan on using them)
* cards (constructed using the deck's ranks and suits)

To use your custom deck, create a new instance of the Deck class with the custom deck set as the `_deck` argument

```js
const ranks = [
  new Rank('1', '1rank', 1),
  new Rank('2', '2rank', 2),
  new Rank('3', '3rank', 3)
]

const suits = [
  new Suit('A', '§', 1),
  new Suit('B', '‡', 2)
]

var cards = [];

ranks.forEach(rank => {
  suits.forEach(suit => {
    cards.push(new Card(rank, suit));
  })
})

const joker = new Card(new Rank('Joker', 'Joker', 15), new Suit('\u00a7', '\u00a7', 0));

const deck = new Deck(0, 1, { cards, joker });
```

## Contribute

If you spot a bug, or want to improve this module, please contact me.