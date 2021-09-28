# Rootlog

A unified notation system for tracking turn activity in the board game [Root](https://ledergames.com/products/root-a-game-of-woodland-might-and-right), produced by Leder Games inc.

## About

This is a WIP. Current version: V2.8 (updated ???). Questions and Feedback are greatly appreciated.

This system is inspired in part by algebraic notation in Chess. It's also inspired by and heavily draws on Nevakanezah's original [Rootlog](https://boardgamegeek.com/thread/2543149/article/36304225) notation.

To handle different factions having very different moves and abilities, Rootlog eschews recording the names of each faction-specific action, and instead records the movement of game pieces incurred by those actions. This means that readers must employ some intuition to understand what happens and why during each turn.

## Goals

1. To track legal changes to board state.
2. To allow quick recording of actions by hand during a game.
3. To allow easy reading of actions, by both machines and humans.

Future changes will be evaluated based on whether they get Rootlog closer to these goals.

## Improvement Space

- Not all Draft systems may be included by this notation.
- There's no notation for ADSET (Advanced Setup) Draft.
- There's no notation for hirelings.
- There's no notation for Spy cards.
- Ministers do not yet have abbreviations (for instance, `#duchessofmud` takes a bit long to write).

## General Syntax

### Brackets in Syntax

- `[X]` = optional, can be omitted, often has a default value
- `<X>` = required, but variable
- `X` = write as shown (i.e. an actual "X")

### Separating Actions and Turns

- In the syntax on this page, "current player" means the player who's currently taking their turn.
- `/` or `;` separates actions recorded within the same turn.
- Each turn must be on its own line.
- You may optionally add an empty line after each round (when everyone's taken a turn), to make the game more human-readable.
- Commentary can be put at the end of a line like this: `// [Commentary]`.

#### Start Turn

`<Faction>:`

This syntax is at the beginning of each line that represents a turn, not on its own line.  

#### End of Game

`Winner: <Factions...>`

### Game Setup (including Draft, if any)

The following lines must be included at the beginning of the notation, in the order they're shown here.

`Map: <Map Name>`  
`Deck: <Deck Name>`  
`[Clearings: <Suit>1, <Suit>2... <Suit>12]` *This records the clearing suits. Omitted only on the Fall map.*  
`[Pool: <Faction 1>[Faction 2...]]` *Include this line if players will Draft from a limited pool of factions.*  
`<Faction>: <Player Name>` *Repeat this line once for each player, in order of draft, if relevant.*

- `Map Name` = `Fall`, `Winter`, `Lake`, or `Mountain`  
- `Deck Name` = `Standard` or `E&P`  

Record faction setup steps using game notation. Each faction takes a "Setup" turn (in the notation), so the first turn recorded can always be read as the setup.

### Suits

- `B` = Bird
- `F` = Fox
- `M` = Mouse
- `R` = Rabbit

### Factions

- `C` = Marquise de Cat
- `E` = Eyrie Dynasties
- `A` = Woodland Alliance
- `V` = Vagabond
- `G` = 2nd Vagabond
- `L` = Lizard Cult
- `O` = Riverfolk Company
- `D` = Underground Duchy
- `P` = Corvid Conspiracy
- `H` = Lord of the Hundreds
- `K` = Keepers in Iron

### Piece Types

- `w` = warrior
- `p` = pawn
- `b` = building
- `t` = token
- `r` = raft (Lake map only)

### Pieces

`[Faction]<piece type>[_<letter>]`

- `Faction` = If omitted, it's the current player's faction.
- `letter` = Specifies a certain piece of that type. For example, for the Marquise, `b_s` would be a Sawmill.

### Cards

`[Suit]#[card name or abbreviation]`

- `Suit` = Suit of the card. If empty, it's either any suit or unknown. Suits can be combined and grouped if desired (see section and examples below).
- `card name or abbreviation` = The name of the card (all lower case with no spaces) or the abbreviation of the card listed in the Card Name Abbreviations section below. Card names and abbreviations can both be used within the same game's notation. If omitted, it's assumed it doesn't matter.

**Card Examples:**  
`F#` *One Fox card.*  
`2R#` *Two Rabbit cards.*  
`#sappers` *The Sappers card.*  
`#sap` *Also the Sappers card.*  
`(2F+M)#` *Two Fox cards and one Mouse card.*  
`R#favor` *Favor of the Rabbits*  

### Item Types

- `s` = sword
- `b` = bag
- `c` = coin
- `x` = crossbow ("xbow")
- `h` = hammer
- `t` = tea
- `r` = to"r"ch
- `f` = boot (for "foot")

### Items

`%<item type>`  

- `item type` - type of the item

`%_`  *All items in that Location.*

### Item States

When used as a Start in Move (below), it specifies which item to move (refreshed or exhausted). When used as a Destination in Move, the item stays where it is and flips to the given side.  

- `r` = Face-up ("refreshed")
- `e` = Face-down ("exhausted")

### Clearings

`<Number>`

- `Number` = 1-12, according to the Law of Rootbotics map diagrams.

### Forest

`<First Clearing>_<Second Clearing>_<Third Clearing>[_<Other Clearings>...]`

- `Clearings` = All clearings adjacent to the forest, in order from lowest number to highest number.

### Faction Boards

`[Faction]$`

- `Faction` = If omitted, it's the current player's faction.

For all players, Crafted Improvement cards are on their Faction Board.

### Player Hands

`<Faction>`

- `Faction` = Faction whose hand this is.

### Locations

A term for reference in other syntax. Includes Clearings, Forests, Faction Boards, Player Hands, Item States, and other locations named under Special Faction Syntax.

### Battles

`[Attacker Faction]X<Defender Faction><Clearing>[<Suit>@[<Suit>@]][(<Attacker Roll>,<Defender Roll>)]`

- `Attacker Faction` = If omitted, it's the current player's faction.
- `<Suit>@` = An ambush card. First one is defender's, second one is attacker's.
- `Attacker Roll` and `Defender Roll` = Rolls can always be omitted entirely, and are completely aesthetic if included. If you include them, these are the numbers rolled by the Attacker and Defender, not including extra hits. For example, an unfortunate attack on a Woodland Alliance's base might read `(0,3)`.

### Move

`[Number]<Piece, Card, or Item>[Start]->[Destination]`

- `Number` = How many of the Piece, Card, or Item are involved. If omitted, it's one.
- `Piece, Card, or Item` = See Piece, Card, and Item sections above.
- `Start` = The Location where the Pieces, Cards, or Items are. If omitted...

  - For a card, it's the draw pile.
  - For a warrior, building, or token, it's the supply.
  - For a pawn, it's always omitted, and it's the pawn's current location.
  - For an item, it's the current player's faction board.
- `Destination` = The Location where they will be moved to. If omitted...
  - For a card, it's the discard pile.
  - For a piece, it's the supply, unless the Law of Root says that it's removed from play, in which case it's removed from play.
  - For an item, it's removed from play.

**Move Examples:**  
`2Dw3->5` *Move 2 of the Underground Duchy's warriors from clearing 3 to clearing 5.*  
`4w10->4` *Move 4 of the current player's warriors from clearing 10 to clearing 4.*  
`b->3` *Place a building (from the current player's supply) in clearing 3.*  
`p->12` *Move the current player's pawn to clearing 12.*  
`At5->` *Remove the Woodland Alliance's sympathy token from clearing 5.*  
`F#domO->C` *The Riverfolk give a Fox Dominance card to the Marquise.*  
`M#E->P` *The Eyrie give a Mouse card to the Corvids.*  
`#V->C` *The Vagabond gives an unspecified card to the Marquise.*  
`F#C->` *The Marquise discards a Fox card.*  
`#->C` *The Marquise draws a card from the deck.*  
`3#A->$` *The Woodland Alliance mobilizes 3 supporters.*  
`3F#$->` *The Woodland Alliance spends 3 Fox supporters.*  
`#E->A$` *The Eyrie give the Woodland Alliance one supporter.*  
`%sO$->V$` *The Riverfolk give a sword to the Vagabond.*  
`%s12->$` *Take a sword from the ruin in clearing 12. The ruin piece is assumed to be removed when the ruin is empty.*  
`%s->e` *The current player exhausts a sword.*  
`%fe->` *The current player removes one of their exhausted boots from play.*  

#### Discard Pile Start Location

`*` *The Discard Pile, when it's drawn from.*

Can only be used as a Start Location in Move.

**Examples:**  
`F#@*->P` *Use Informants to draw an Ambush from the Discard Pile.*  
`M#favor*->V` *The Tinker uses Day Labor to draw Favor of the Mice from the Discard Pile.*  

### Reveal

`[Number][Card][Faction]^[Target Faction]`

- `Number` = How many cards are revealed. If omitted, it's one.
- `Card` = The card(s) being revealed. If omitted, it's their whole hand.
- `Faction` = The faction revealing the card(s) from their hand. If omitted, it's the current player's faction.
- `Target Faction` = The faction the card is revealed to. If omitted, it's the entire table.

**Reveal Examples:**  
`^A` *The current player reveals their whole hand to the Woodland Alliance.*  
`F#^P` *The current player reveals one Fox card to the Corvids.*  
`2M#^` *The current player reveals two Mouse cards to the whole table.*  
`V^O` *The Vagabond reveals their whole hand to the Riverfolk.*  

### Optional Move and Reveal Notations

These aren't necessary, but you can use them for faster, clearer notation.

#### Combine Multiple Pieces, Cards, Items, or Clearings in Move or Reveal Notation

Shows simultaneous or immediately sequential movement. If Clearing Destinations are combined, that means that the shown number of Pieces went to *each* Clearing.

`<Side>+<Side>+...`  

- `Side` = The left side or the right side of the `->` or `^` in the Move or Reveal syntax.

**Combining Examples:**  
`w->3+11` *Place 1 warrior each on clearings 3 and 11.*  
`t1+t2+t5->` *Remove the tokens on clearings 1, 2, and 5.*  
`w+t_r->10` *Place 1 warrior and a rabbit trade post on clearing 10.*  
`F#+2M#^` *Reveal one fox card and two mouse cards.*  
`%h+%c+%s->r` *Refresh a hammer, coin, and sword.*

#### Group Combined Pieces, Cards, or Items in Notation

Group combined things together to make them easier to track, both when writing and reading.

`([Number]<Piece>+[Number]<Piece>+...)`  

- `Number` = Number of pieces. If omitted, it's one.
- `Piece` = Pieces in the clearing.

`([Number]<Card>+[Number]<Card>+...)`  
`([Number]<Suit>+[Number]<Suit>+...)#`  

- `Number` = Number of cards. If omitted, it's one.
- `Card` = Cards in the player's hand or faction board.

`([Number]<Item>+[Number]<Item>+...)`  

- `Number` = Number of items. If omitted, it's one.
- `Item` = Items on the player's faction board.

**Grouping Examples:**  
`(w+2Cw+Cb_s)3->` *Remove one of your warriors, 2 Marquise warriors, and 1 sawmill from Clearing 3.*  
`(2R+B)#A$->` *Discard 2 Rabbit cards and 1 Bird card from the Woodland Alliance's supporters.*  
`(M+2F)#^` *Reveal a Mouse card and 2 Fox cards from the current player's hand to the whole table.*  
`(2%c+%h)V$->d` *Damage 2 coins and a hammer on the Vagabond's board.*

### Craft

`Z<Item>`  
`Z<card name>`  

- `card name` = All lowercase, no spaces.

### Score or Lose Points

`[Faction]++[Number]` *Score points.*  
`[Faction]--[Number]` *Lose points.*

- `Faction` = The faction scoring points. If omitted, it's the current player's faction.
- `Number` = Number of points to score. If omitted, it's one.

### Move VP Token to Faction Board (for Dominance or Coalition)

`++-><Faction Board>`

- `Faction Board` = The faction board your VP token is moving to.

### Closed Path Marker (Mountain Map only)

`<Lower Clearing>_<Higher Clearing>->`

- `Lower Clearing` = The lower number of the two clearings adjacent to the Closed Path.
- `Higher Clearing` = The higher number of the two clearings adjacent to the Closed Path.

## Special Faction Syntax

### Marquise de Cat

When notating Field Hospitals, notate that the warriors moved from the clearing they were removed from into the keep's clearing. Don't remove them to the supply.

- `b_s` = Sawmill
- `b_w` = Workshop
- `b_r` = Recruiter
- `t_k` = Keep
- `t` = Wood

### Eyrie Dynasties

The following actions can only be notated on the Eyrie Dynasties's turn:

- Move cards to the Decree
- Discard the Decree
- Appoint a new Leader

#### Decree Columns

- `r` = Recruit
- `m` = Move
- `x` = Battle
- `b` = Build

#### Decree

This is a Location.  
`$_<decree column>`

- `decree column` = The column that cards are being added to or removed from.

#### Discard the Decree, including Viziers and Leader

`$_->`

That is, discard the whole board.  

#### New Leader

`#<leader name>->$`

- `leader name` = all lower case

Example: `#commander->$`

### Woodland Alliance

The Woodland Alliance's Faction Board is its supporters and officers.

- `b_f` = Fox base
- `b_r` = Rabbit base
- `b_m` = Mouse base

### Vagabond

The Vagabond's Faction Board is its Satchel (undamaged).

#### Board Areas

These are Locations. When used as a Destination in Move, the item stays on its current board and moves to the new area unchanged.  

- `s` = Satchel (undamaged)
- `d` = Damaged
- `t` = Track (appropriate to the Item)

#### Item Locations

These are Locations.  
`<board area>[item state]`

- `board area` = The area the item is either in or moving to.
- `item state` = If omitted...
  - For the Start, the item can be in either state.
  - For the Destination, the item doesn't get flipped.

Examples:  
`%sde->r` *Refresh an damaged, exhausted sword.*  
`(%r+%t+%s)d->s` *Repair three items.*  
`%rde->s` *Repair a damaged, exhausted torch.*  
`%ct->s` *Move coin from track to satchel.*  
`%fr->d` *Damage an unexhausted boot.*  

#### Available Quests

This is a Location.  
`Q`

#### Relationship Marker

`[Vagabond Faction]$_<Faction>`

- `Vagabond Faction` = The Vagabond whose relationship is changing (`V` or `G`). If omitted, it's the current player.
- `Faction` = The faction the relationship is with.

##### Relationship Status

This is a Location, on the `Vagabond Faction`'s board above.  

- `h` = Hostile
- `0` = Indifferent
- `1` = One to the right of Indifferent
- `2` = One to the left of Allied
- `a` = Allied

### Riverfolk Company

The following action can only be notated on the Riverfolk Company's turn:

- Set prices

Committed funds are not notated, just the actions those funds allow. The Riverfolk's Faction Board is its Funds and Payments. When using Export, *don't* use the craft notation; just discard the card from the Player Hand. Remember: other players buy cards from the Riverfolk's Player Hand, *not* their Faction Board!

- `t_f` = Fox trade post
- `t_r` = Rabbit trade post
- `t_m` = Mouse trade post

The Riverfolk have no buildings.

#### Price Type

- `h` = Hand card
- `r` = Riverboats
- `m` = Mercenaries

#### Set Prices

`$_[price type]-><New Price>`

- `price type` = If omitted, *all* prices are set to the new price.
- `New Price` = 1-4, the new price of the service

If this is omitted from the Riverfolk's turn, prices stay the same.

#### Funds

Don't use this to record changes in funds *during* the Riverfolk's turn. Only use this at the *end* of their turn and when their funds are removed on *others'* turns. If this action is omitted at the end of the Riverfolk's turn, funds are assumed to be zero.  
`$_f-><Number>`

- `Number` = The number of funds on the Riverfolk's board.

### Lizard Cult

The following actions can only be notated on the Lizard Cult's turn:

- Set the Outcast suit
- Set the Hated Outcast suit

When the Lizard Cult's revealed cards return to their hand, it's not notated. When cards are placed in the Lost Souls pile, notate it as though they were discarded (i.e. `#C->`). The Lizard Cult's Faction Board is its acolytes.

- `b_f` = Fox garden
- `b_r` = Rabbit garden
- `b_m` = Mouse garden

#### Outcast

After the Outcast or Hated Outcast is set, all Lost Souls are moved to the discard pile; this is not notated.

##### Set the Outcast Suit

`$_o-><Suit>`

##### Set the Hated Outcast Suit

`$_ho-><Suit>`

### Underground Duchy

The following action can only be notated on the Underground Duchy's turn:

- Sway a Minister

When the Underground Duchy's revealed cards return to their hand, it's not notated. The Underground Duchy's Faction Board is its swayed ministers.

- `b_c` = Citadel
- `b_m` = Market
- `0` = Burrow (Clearing Number)

#### Minister Cards

`#<minister name>`

- `minister name` = all lower case, no spaces

### Corvid Conspiracy

Notate that Bomb plots are removed immediately after flipping them.

- `t` = Facedown plot
- `t_b` = Bomb plot
- `t_s` = Snare plot
- `t_r` = Raid plot
- `t_e` = Extortion plot

#### Exposure

`?P<plot token><Clearing>`  

- `plot token` = The type of plot token guessed by the current player, for example, `t_e`.
- `Clearing` = The clearing the plot token is in
Success or failure of the guess is conveyed by the actions that follow (give card or remove token).

#### Flip Plot

`[P]t<Clearing>^<plot token>`

- `P` = Omitted when the Corvid Conspiracy is the current player
- `Clearing` = The clearing the plot token is in
- `plot token` = The plot token the plot is revealed to be

#### Trick

`t<Clearing><->t<Clearing>`

Note: The `<->` in the middle of this action is written as is. For example, `t12<->t4` means that the plots on clearings 4 and 12 switch places.

### Lord of the Hundreds

The following action can only be notated on the Lord of the Hundreds's turn:

- Choose mood

The Lord of the Hundreds's Faction Board is its hoard. Do not notate the mob die roll.

- `w_w` = Warlord warrior

#### Choose Mood

`#<mood name>->$`

- `mood name` = all lower case, no spaces

### Keepers in Iron

The following actions can only be notated on the Keepers in Iron's turn:

- Add cards to the retinue
- Move cards in the retinue
- Remove cards from the retinue
- Reveal relic token's point value

The Keepers in Iron's Faction Board is its relics.

- `t_f` = Figure relic token
- `t_t` = Tablet relic token
- `t_j` = Jewelry relic token
- `b_f` = Waystation building, figure side up
- `b_t` = Waystation building, tablet side up
- `b_j` = Waystation building, jewelry side up
- `#faith` or `B#faith` = Faithful retainer card

#### Retinue Locations

`$_<Number>`

- `Number` = Position of the Retinue column: `1`, `2`, or `3`; `1` is leftmost, `3` is rightmost.

#### Reveal Relic Token's Point Value

`<relic token><Clearing>^<Number>`

- `Number` = Number of points the relic is worth.

Notate this after a delve when the relic token is flipped face up.

## Card Name Abbreviations (Optional)

See Cards section above. These abbreviations are not necessary, but can optionally be used in place of the full card name.

### Both Decks

- `@` = Ambush
- `dom` = Dominance

### Standard Deck

- `armor` = Armorers
- `bank` = Better Burrow Bank
- `brutal` = Brutal Tactics
- `command` = Command Warren.
- `cob` = Cobbler
- `codeb` = Codebreakers
- `favor` = Favor of the *Suit*s (use `F#favor`—or `ffavor` for crafting—to specify suit)
- `royal` = Royal Claim
- `sap` = Sappers
- `scout` = Scouting Party
- `stand` = Stand and Deliver
- `tax` = Tax Collector

### Exiles & Partisans Deck

- `boat` = Boat Builders
- `charm` = Charm Offensive
- `coffin` = Coffin Makers
- `cplans` = Corvid Planners
- `emi` = Eyrie Emigre
- `false` = False Orders
- `part` = Partisans (use `F#part`—or `fpart` for crafting—to specify suit)
- `inform` = Informants
- `league` = League of Adventurous Mice
- `engrave` = Master Engravers
- `murine` = Murine Broker
- `prop` = Propaganda Bureau
- `sabo` = Saboteurs
- `soup` = Soup Kitchens
- `swap` = Swap Meet
- `tun` = Tunnels

### Quest Cards

- `errand` = Errand
- `bandits` = Expel Bandits
- `bear` = Fend Off a Bear
- `escort` = Escort
- `funds` = Fundraising
- `speech` = Give a Speech
- `guard` = Guard Duty
- `logs` = Logistics
- `shed` = Repair a Shed

## Common Questions

**Q:** Are card activations (such as Partisans, Arbiter, or Ronin) notated?  
**A:** No; only changes to game state are notated. Notate the result of the effect activation, but not the activation itself. For instance, if a card is discarded when activated, notate that it's discarded. Feel free to add commentary (`//`) to include information that isn't notated.

**Q:** Why does `B#C->` mean that the Marquise discards a Bird card? Why can't I write `CB#->`?  
**A:** In the correct syntax (`B#C->`), `C` is a *Location*: the Marquise's Player Hand. The card *starts* in the Marquise's hand and *moves to* the discard pile. In `CB#->`, the `C` means nothing (since cards aren't faction pieces), and the Bird card moves from the draw pile to the discard pile, which is nonsense.

**Q:** How do I notate warriors moving to the Coffin Makers card?  
**A:** If the Coffin Makers card has been crafted and is still in play, when warriors are moved to the supply (for example, `3w9->`), they're assumed to move to the Coffin Makers card. No additional notation is made.

## Examples

### Example Actions

- `#->O` *The Riverfolk draw one card from the deck.*
- `M#C->` *The Marquise discards one Mouse card. Note: the `C` is **after** the card (`M#`), because it represent the Player's Hand, which is where the card starts before it's discarded.*
- `F#V->C` *The Vagabond gives one Fox card to the Marquise, for example, when Aiding them.*
- `#V->C` *The Vagabond gives one unspecified card to the Marquise, for example, in Swap Meet.*
- `%r->r` *Refresh an undamaged torch.*
- `%xd->` *Remove an damaged crossbow from play.*
- `%s12->$` *Take a sword from a ruin. The ruin piece is assumed to be removed when the ruin is empty.*
- `w->5+6+12` *Recruit one warrior each to clearings 5, 6, and 12.*
- `b_j->12` *Keepers build a waystation.*
- `(3w+r)1->12` *Move 3 warriors and the raft from clearing 1 to clearing 12.*
- `(4Lw+2Lb_r)4->` *Remove 4 Lizard warriors and 2 Rabbit gardens from clearing 4.*
- `R#@*->A` *The Woodland Alliance uses Informants to draw an Ambush card at the end of their turn.*
- `#brigadier->$` *The Underground Duchy sways the Brigadier.*
- `#brigadierD$->` *The Underground Duchy loses the Brigadier; the price of failure.*
- `%_d->s+r` *The Vagabond takes An Evening's Rest, repairing and refreshing all damaged items. Damaged track items go to the satchel.*

### Example Sequences

Common sequences of multiple actions in a row.

- `XE3/(w+2Ew+Eb)3->/++` *The current player battles and takes out a defended Eyrie roost.*
- `F#C->/F#dom->C` *The Marquise swaps out a Dominance card.*
- `XA9/At9->/#E->A$/++2` *The Despot-led Eyrie attack and remove a defenseless sympathy token, triggering Outrage.*
- `%_d->s+r/%t+%c->t` *The Vagabond takes An Evening's Rest, with tea and coins going back to their tracks.*
- `XP12/Pt12^t_r/w->4+7+9+10/++` *The current player attacks and removes a Corvid Raid plot token.*
- `3Cw->O$/B#saboO->C` *The Marquise buys a Bird card from the Riverfolk.*
- `2R#$->/(2Cw+Cb_s+Dw)3->/++/b_r+w->3/w->$` *The Woodland Alliance revolts in a Rabbit clearing with Marquise and Duchy pieces.*
- `XK9/2Kw9->/Kt_f9->2_3_7_12/$_K->h/++4` *The Vagabond removes a defended relic in battle.*
- `w12->/w_w->12` - *The Hundreds anoint a new Warlord.*
- `#sabo$->/#boatE$->` *The current player activates Saboteurs to discard the Eyrie's Boat Builders.*
- `R#O->/Pw10->/w->10` *The Riverfolk activate Propaganda Bureau to convert a Corvid warrior.*
- `XE8/V++/(3w+2Ew)8->` *The Eyrie enlist the Arbiter Vagabond to help them defend.*
- `#bankO->/w->$` *The Riverfolk use Export to gain a warrior in Payments. Note: Don't use the "craft" notation in this case, since the card isn't added to Crafted Improvements and the item isn't added to the faction board.*
- `%r->e/CXO12/(2Cw+3Ow)12->/$_O+$_C->h/++3` *The Vagrant Vagabond instigates a battle between the Marquise and the Riverfolk.*
- `t_t7_10_11->10/t_t10^2/#faith$_2->` - *The Keepers delve a relic (possibly foolishly).*
- `t_f5->$/++5` - *The Keepers recover a 3 point relic which also completes a relic column.*
- `#^P/?Pt3^t_e/#C->P` *The Marquise guesses the Corvids' plot (incorrectly, oh well) using Exposure.*
- `XC9/R#C->/2Cw9->2/(2w+Cb_s)9->/++` *The Marquise uses Field Hospitals after being attacked.*
- `#false$->/3Dw8->9/t9^t_b/3Dw9->/++3` *Corvids play False Orders into a bomb. D:*

### Example Turns

```rootlog
Map: Fall
Deck: E&P
Pool: CDOPA // Faction pool to draft from.  
A: Guerric
P: Justin
O: Billy
C: Edu

C:t_k->2/w->1+2+3+5+6+7+8+9+10+11+12/b_s->2/b_w->5/b_r->10 // Marquise sets up Keep in the top right corner.
O:w->10+11/2w->5/$_->3 // Riverfolk spread out warriors a bit, set all prices to 3.  
P:w->4+8+9 // Corvids place into the bottom left corner of the board.  
A:3#->$ // Start with 3 supporters.

C:3w->O$/B#O->C/t->2/Zrpart/t2->/b_r->6/++/w->6+10/M#C->/t->2/B#C->/t2->/b_s->3/++/#->C // Buys a Bird card from Riverfolk to Overwork, Recruit, and do two Builds.  
O:3#->O/w10->5/2w$->/t_r+w->5/++2 // Fill up their card shop, put out a trade post.  
P:F#P->/w->1+6+12+8/w1->9/2w9->4/w4->/t->4/#->P // One plot goes out.  
A:3w->O$/B#O->A/3B#$->/t->12+11+9/++2/Zmurine/Zh/++2/2#A->$/#->A // Lucky 3 Bird Supporters stack gives them lots of options.
```

*... game was continued ...*

## Credits & Contributors

[Rootlog initial concept](https://boardgamegeek.com/thread/2543149/article/36304225) by Nevakanezah (licensed under [WTFPL](http://www.wtfpl.net/about/))

Quest Card abbreviations by Waterman121.

Special thanks to feedback and testing from:

- Waterman121
- starlite
- Seiyria
- Kyle Werntz

## Changelog

- Version 2.7 (23 Jan 2021):
  - Added Corvid Bomb plot spec
- Version 2.6 (12 Dec 2020):
  - Added Riverfolk Export spec and example.
  - Cleaned up redundant Ministers information and added examples.
  - Added Spy cards as limitation.
- Version 2.5 (11 Dec 2020):
  - Clarified that certain actions can only be notated on certain Factions' turns.
  - Added examples and clarifications throughout.
- Version 2.4 (7 Dec 2020):
  - Added Field Hospitals spec, to work with Coffin Makers.
  - Added Discard Pile Start Location, thanks starlite
  - Added more examples and clarifications throughout.
- Version 2.3 (3 Dec 2020):
  - Changed ambush symbol to `@`, to make it more noticeable.
  - Removed `//` from beginning of Start of Turn.
  - Line breaks are now required between turns.
  - Changed the Game Setup syntax.
  - Simplified the `favor` and `part` cards syntax.
  - Added optional and aesthetic rolled hits syntax to Battle.
  - Added to and solidified the card abbreviations list, thanks Waterman121.
  - Added more examples and explanations throughout, and clarified language.
  - Added Common Questions.
  - Added Credit and Changelog sections.
- Version 2.2 (29 Nov 2020):
  - First version released publicly.
- Version 2.1:
  - Internal changes.
- Version 2.0:
  - Initial draft.
