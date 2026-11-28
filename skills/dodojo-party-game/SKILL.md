---
name: dodojo-party-game
description: Make a party game for a group of two to ten people in one room, as one webpage - a guessing, drawing, bluffing, push-your-luck, reflex, voting or truth-or-dare game, with one phone passed around, laid in the middle of the table or held up, or each player on their own phone in a dodojo team space or game room - readable from across the table, with secrets that stay hidden when the phone changes hands, a clock people hear, a tally across the evening and prompts written natively for each language - saved into dodojo as a webpage Note, or as a standalone .html file. Use for 聚会游戏, 派对游戏, 团建, 酒桌游戏, 家庭游戏, 你画我猜, 比划猜词, 真心话大冒险, 谁是卧底 and any game for a group.
license: MIT
---

# dodojo-party-game

A party game is for the people around the table, not for the screen. The
phone is a prop: it keeps time, holds the secret, deals the prompt and keeps
score, while the fun happens between the players. Everything that matters is
readable from arm's length or across a table, and the game works the first
time with people who have never seen it. Its look comes from a prop the game
could have been made of. Nothing here is a layout to copy.

It is one self-contained `.html` file. In [dodojo](https://www.dodojo.ai) it is
shown inside a Note, full height; the top of the page becomes the Note's cover
in the person's library, and an evening left halfway opens on the same round
on any of their devices. Outside dodojo the same file opens in any browser.

## Workflow

1. **Picture the table** - who plays, how many, where the phone sits during play, how long a round and an evening last, and the languages at the table.
2. **Find the engine** - one simple action with social tension around it: guess, bluff, push your luck, race, vote or draw lots.
3. **Write the rules and the content** - setup in under a minute, turns, scoring, how the evening ends, and hundreds of prompts written natively for each language.
4. **Lay it out for the table** - the word that matters is the biggest thing on the page, one big button, a cover screen before every secret, a pad for each player at their edge.
5. **Run the room** - a clock people hear, rounds that end on a moment, a tally across the evening, turns that rotate fairly and something to do while waiting.
6. **Keep the evening** - names, the tally, prompts already used and the round in progress kept with the page; seats through dodojo.game in a team space.
7. **Play it with a pretend table, then save** - whole evenings at the smallest and largest group, every hand-off, timer and language, screenshots at phone width, then a dodojo Note.

## 1. Picture the table

- **Who plays.** Two to ten people: friends, a family with children,
  colleagues who just met, a drinking game. The group sets the content and
  the pace: nothing suggestive for a family, nothing that singles someone out
  among colleagues, alcohol only when asked.
- **Where the phone sits during play.** This decides most of the design:
  - *Passed hand to hand*: one person at a time sees the screen (a secret
    word, a role, a call). Every hand-off needs a cover screen.
  - *Flat in the middle*: everyone reaches it at once (a slap race, fingers
    down for drawing lots). People sit on every side, so text faces more than
    one way and each player has a pad at their edge.
  - *Held up*: one person holds it facing themselves (the describer in
    charades) or turns it to the group (a drawing shown around).
  - *Read by a host*: one person runs the game and reads aloud (a quiz night,
    the narrator of a hidden-role game).
  - *On everyone's own phone*: only when the Note is in a dodojo team space,
    or opened as a game room that friends join by typing its code in the
    dodojo app, where the page's state is shared live and `dodojo.game`
    keeps seats and turns, with `min` for however many come
    ([references/frame.md](references/frame.md)). Elsewhere one device plays
    every seat; say so in one line if the person asked for online play.
- **How long.** Rounds of one to five minutes, an evening of fifteen to sixty.
  Anyone who waits more than about two minutes for a turn needs a part
  meanwhile: guessing, judging, timing, voting.
- **Languages.** A mixed table may need two or three languages on one page.
  Take the default from `navigator.languages`, offer a small switch
  (`EN · 中文 · 日本語`) under the controls, and remember the choice. The static
  HTML carries the first language; every language gets its own prompts
  (section 3).
- With the dodojo connector, search the person's memories first
  (`search_memories`): the group's names, an earlier version of the game, a
  trip or a story they share. A round built from the group's own places and
  jokes beats any word list; ask before putting other people's photos or
  private stories into a page.

## 2. Find the engine

Party games that last rest on one simple action with social tension around
it. Choose one and build the whole page around it:

| Engine | What people do | Where the tension comes from | Phone |
| --- | --- | --- | --- |
| Guess | one knows, the others shout | the clock | held up, passed |
| Bluff and deduce | one has a different word or a hidden role | talking, then a vote | passed, then laid down |
| Push your luck | each turn is safe until it is not | the next turn | passed |
| Race and react | everyone at once, false alarms cost | reflexes | in the middle |
| Judge and vote | the group picks the best, the most likely | opinions | host, passed |
| Draw lots | chance picks who does what | the moment before the pick | in the middle |

- The action must work for the smallest and the largest group you claim. Two
  players often need their own mode (co-op against the clock instead of two
  teams); ten need short turns.
- One twist at most on top of the engine (look-alike words that punish a
  false slap, a range that shrinks toward the bomb). A second twist is a
  second game.
- Make original games or folk games nobody owns: charades, truth or dare,
  the odd-word-out game, hidden-role games, counting games such as "sevens".
  Never recreate a commercial party game's name, cards, art or exact rules.

## 3. Write the rules and the content

- **Setup in under a minute.** How many players (names optional, with
  defaults such as "Player 3"), one choice of mode, Start. Every other setting
  has a good default and lives under the game.
- **Write the rules down before any code**: who goes first, what a turn is,
  how points are scored, what ends a round and the evening, what happens when
  someone breaks a rule (a false slap, a word said aloud, a peek). The page's
  "how to play" is two or three lines a newcomer reads while others wait; the
  full rules sit lower, in `<details>`.
- **Content is the game.** A word game needs hundreds of prompts, not twenty:
  enough that an evening never repeats (about 150 or more per level for a
  describe-the-word game), in two or three levels. Read the lists once for
  duplicates, for a prompt that contains its own answer and for anything
  unkind.
- **Write each language for its own players.** Words people of that language
  know and can act out (a Chinese pack gets 火锅 and 广场舞, a Japanese one
  こたつ and 満員電車, not translations of "Thanksgiving"); puns and
  look-alikes that only work in that script (拍 / 柏 / 怕, SLAP / SLAB / CLAP,
  パン / バン / ペン). Never translate a pack word for word, and fit the
  longest word in each language to the play area.
- **Dares and questions** are playful, doable in the room in under a minute,
  and never humiliate, cost money, touch someone without asking, or reach
  outside the room (no calling, posting or messaging). A spicier deck, when
  the group wants one, is off by default.
- Keep the prompts in the HTML (a list in `<details>` at the bottom), so
  search and the apps that cannot run scripts still read them. In a game
  where knowing the list helps a bluffer (word pairs, roles), keep that
  `<details>` closed and say on its summary that it holds spoilers.
- No prompt may appear in the page's own interface text (a button, an
  example in the rules): check every word against the page's other text.

## 4. Lay it out for the table

Declare it a game in the head with
`<meta name="dodojo-page-kind" content="game">` (references/frame.md). On a
computer the page sits in the Note under its title and scrolls with the Note.
On a phone or tablet the Note shows it as a preview that one tap opens on a
screen of its own: the whole screen below a slim bar, where the page scrolls
inside itself and nothing floats over it. So the first screen is what is
played: about 700px tall on a phone. From the top:

1. **A status strip**, one line about 48-56px tall: whose turn it is (their
   name in their colour), the round, the score or what is left.
2. **The play area**, as large as the column allows. It is also the Note's
   cover, so it shows the game ready to start (the bomb armed, the stack of
   cards face down, the cup of sticks), never a menu or a splash screen.
3. **The controls**, right under it: one main action (Start, Got it, Next
   player) the full width of the play area and at least 56px tall, then the
   few others (skip, undo, sound) in one row.
4. **Then what is read**: two or three lines on how to play, the players and
   their names, the settings, the evening's tally, the full rules and the
   prompt lists. Never put rules, an introduction or settings above the game.

- **Readable from a distance.** The one thing everyone looks at (the secret
  word, the number called, the name drawn) is the largest thing on the page,
  96px at most and 36px at least, shrunk to fit the play area's width rather
  than wrapped. Names and scores are at least 20px where they stand alone
  and 16px in a two-column list of players.
- **Secrets stay secret.** Before a secret shows, a cover screen names who
  should look ("Pass to Mia - only Mia looks"); the secret appears while the
  person holds a button, or after a tap, and covers itself again on release
  or after a few seconds; then the cover names the next person. Nothing
  secret is on screen when the phone changes hands, and nothing on the cover
  gives it away (not its length, not its colour). The finger that held the
  secret is still down when it covers itself: ignore clicks for about half a
  second after a press, and presses for about half a second after each
  hand-off, so the release never passes the phone on by accident.
- **A secret vote** passed round works the same way: a cover per voter, the
  ballot showing only that voter's choice, and no running tally until the
  last vote is in.
- **A phone in the middle.** Each player's pad sits at their edge, at least
  64px, numbered and coloured. Text meant for the far side is turned to face
  it, or drawn twice, once each way. Track every finger by its `pointerId`;
  a phone follows about five fingers at once (a tablet more), so a game that
  needs every finger down at the same time caps the players or takes turns,
  and says so.
- **Whose turn it is, in form**: their colour floods the strip or the play
  area's frame, their name is the biggest name on screen. Player colours
  come with a number or a shape, never colour alone.
- **Nothing moves during play.** A status of fixed height, results laid over
  the play area, controls that change their labels but not their size. People
  tap while looking at each other.
- **The narrowest phone.** On a 360px phone a Note gives the page 328px;
  inside the page's own 16px gutters about 296px remain. Names are cut with an ellipsis after about ten
  characters, and every button's label stays on one line in every language.
- On a computer the Note's 920px column can put the players and the tally
  beside the play area; on a phone they stack in the order above.

## 5. Run the room

- **A clock people hear and see.** A tick that quickens in the last ten
  seconds, a distinct end sound, and the time as a shape (sand, a fuse, a
  shrinking bar) as well as a number. It pauses on a pause button and while
  the page is hidden.
- **Every round ends on a moment**: the bang, the reveal, the culprit named.
  One strong sound, the result laid over the play area, then the next
  player's name on the main button.
- **The evening has a shape**: a tally per player or team kept across rounds,
  a goal that ends the evening (first to five, three rounds each), a final
  ranking with one line about each player, and "play again" that keeps the
  names.
- **Fair turns**: seats go round in order; the custom decides who starts the
  next round (often the one who lost); the same prompt never comes twice in
  an evening; skips are limited and counted.
- **A part for everyone**: co-op modes for two or three, a judge or timer for
  those waiting, a pass that costs little for the shy.
- **Sound made with Web Audio**, from the first tap, quiet, with a switch that
  is remembered ([references/build.md](references/build.md)). Rooms are
  loud: important sounds are short and distinct, not long.
- **No device features** inside dodojo: no vibration, camera, microphone or
  screen wake lock. Design rounds that do not need the screen to stay on; if
  a timer runs past a minute, a line suggests keeping the screen awake.

## 6. Keep the evening

- After every change, save the names, the settings, the tally, the prompts
  already used and the round in progress with `window.dodojo.setState`, in
  compact strings (a value holds at most 4000 characters). The evening
  survives a phone that locks, a reload or a switch to another app.
- A secret in progress (the bomb's number, the roles) is kept too, so a
  reload never reshuffles: keep the seed and the position in the deck.
- In a team space or a game room with everyone on their own phone, use
  `dodojo.game` for seats, turns and rounds. The page's state is readable by
  everyone playing, so a secret kept there is hidden from the screen, not from someone
  determined: honest enough for a party, not for stakes, and the rules say so.
- Outside dodojo keep everything in memory and carry on.

The page's frame (one file, no network requests, what is blocked, the state
API, `dodojo.game`) is in [references/frame.md](references/frame.md); the look
is in [references/design.md](references/design.md); theme, phone layout, type
and copy are in [references/fundamentals.md](references/fundamentals.md).

## 7. Play it with a pretend table, then save

- Play whole evenings in a browser at the smallest and the largest group you
  claim: every mode and every language; a round ended by the clock, by a win
  and by the main button pressed twice quickly; every hand-off, checking that
  no secret is on screen while the cover shows; a reload in the middle of a
  round; several fingers at once on a phone in the middle.
  [references/build.md](references/build.md) has a Playwright pattern for
  several touches and a stand-in for `window.dodojo`.
- Read each prompt list once more for duplicates, giveaways and anything
  unkind.
- Look at the page at 360 and 390px wide and in the Note column, in both
  themes and every language: the word that matters reads at arm's length,
  labels stay on one line, nothing shifts during play, and the first screen
  makes a good cover. Use `preview_webpage` in the dodojo desktop app, or
  `node <this skill's folder>/scripts/shoot.mjs <page.html> <prefix> --width 360 --top`
  (it needs Playwright). Fix what you find, then look again at what changed.
- Save it as [references/save-to-dodojo.md](references/save-to-dodojo.md)
  describes, with a short Markdown body: what the game is, how many play, how
  to start. Without the dodojo connector, write the `.html` and tell the person
  where it is.
