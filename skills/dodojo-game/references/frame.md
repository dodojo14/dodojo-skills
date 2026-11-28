# The frame a webpage note lives in

dodojo shows the page in a locked sandbox inside a Note. The same file must
also open on its own in any browser. Build around these limits instead of
detecting them.

## Skeleton

```html
<!doctype html>
<html lang="en">           <!-- the page's language -->
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="color-scheme" content="light dark">
<meta name="dodojo-page-id" content="PAGE-ID">
<meta name="dodojo-page-kind" content="game">
<title>WHAT THIS PAGE IS</title>
<style>
/* layout: ONE LINE ON THE LAYOUT CONCEPT FOR THIS SUBJECT */
/* The values below are placeholders showing where each token goes.
   Choose every color for the subject; never keep these. */
:root {
  --paper: var(--dodojo-bg, #f5f5f4);
  --panel: var(--dodojo-surface, #ffffff);
  --ink: var(--dodojo-fg, #1c1c1c);
  --soft: var(--dodojo-muted-fg, #5f6061);
  --line: var(--dodojo-border, rgba(28, 28, 28, .12));
  --accent: #345;             /* the subject's own color */
  --accent-ink: #fff;         /* text on the accent */
}
:root[data-dodojo-theme="dark"] {
  --paper: var(--dodojo-bg, #131313);
  --panel: var(--dodojo-surface, #1c1c1c);
  --ink: var(--dodojo-fg, #ececea);
  --soft: var(--dodojo-muted-fg, #a2a3a4);
  --line: var(--dodojo-border, rgba(236, 236, 234, .12));
  --accent: #9ab;
  --accent-ink: #111;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-dodojo-theme]) {
    --paper: #131313; --panel: #1c1c1c; --ink: #ececea; --soft: #a2a3a4;
    --line: rgba(236, 236, 234, .12); --accent: #9ab; --accent-ink: #111;
  }
}
[hidden] { display: none !important; }
img { max-width: 100%; height: auto; }
body { margin: 0; padding: 16px; background: var(--paper); color: var(--ink);
  font-family: var(--dodojo-font-sans, system-ui, -apple-system, "PingFang SC", "Noto Sans SC", sans-serif); }
</style>
</head>
<body>
  <!-- real content here -->
  <script>
  // Outside dodojo, show the attached photos from the folder beside the page.
  if (!window.dodojo) document.querySelectorAll('[src^="attachment:"]').forEach(el => { el.src = el.getAttribute('src').slice(11); });
  </script>
</body>
</html>
```

- `color-scheme` with `dark` tells dodojo the page follows the app's light
  and dark. dodojo then sets `data-dodojo-theme="light"` or `"dark"` on
  `<html>` and supplies its palette as `--dodojo-bg`, `--dodojo-fg`,
  `--dodojo-surface`, `--dodojo-muted`, `--dodojo-muted-fg`,
  `--dodojo-border`, `--dodojo-accent`, `--dodojo-accent-fg`,
  `--dodojo-radius`, `--dodojo-font-sans` and `--dodojo-font-mono`.
- Build neutrals on those variables, always with your own fallback, so the
  page sits naturally in the app and still looks finished on its own. Put the
  subject's accent on top.
- Dark values go twice: under `:root[data-dodojo-theme="dark"]` (inside
  dodojo, which may differ from the system setting) and under
  `prefers-color-scheme: dark` guarded by `:root:not([data-dodojo-theme])`
  (on its own).
- `dodojo-page-id` (letters, numbers, dots, underscores, hyphens) names the
  page's saved state. Keep it when you revise the page.
- `dodojo-page-kind` `game` says the page is a game. On a phone or tablet
  dodojo then shows it in the Note as a preview that one tap opens on a screen
  of its own: the page fills the screen below a slim bar and scrolls inside
  itself, the edges do not navigate, the screen stays on, and a held finger
  does not select text or raise a menu, nor do two quick taps zoom (text
  fields still select). On a computer it plays in the Note. Without the meta
  the game is shown as an ordinary page that scrolls with the Note.
- The closing script is the only line that cares where the page runs; keep it
  last.

## Rules

- **One self-contained file.** CSS and JavaScript inline. Libraries only from
  cdnjs.cloudflare.com, cdn.jsdelivr.net, unpkg.com, esm.sh,
  cdn.tailwindcss.com or code.jquery.com, pinned to an exact version at least
  two weeks old, loaded before the script that uses them. Stylesheets only from
  those and Google Fonts (fonts.googleapis.com, with its font files from
  fonts.gstatic.com). Any other host is blocked. Use a library only when it
  does substantial work (a chart, a date library).
- **Pictures are attachments.** Images, video and audio from other websites do
  not load. Download what the page shows, keep it in the folder beside the
  page, and refer to it as `src="attachment:<file name>"`. Never base64-inline
  photos, never hotlink. Give every image alt text and fixed dimensions or an
  `aspect-ratio`, and credit photos you did not take in small text.
- **Nothing live.** No requests except to the CDNs above: no weather, traffic,
  exchange-rate or other APIs. Put the facts in the page with the date you
  checked them, and link to the live source.
- **Nothing that leaves the page.** No iframes, embeds, map widgets, forms that
  submit anywhere, downloads, print, `alert`/`confirm`/`prompt`, `localStorage`
  or `sessionStorage` (they throw inside dodojo), and never set `location`.
- **Remembered state.** Put `data-dodojo-key="<name>"` on an input, textarea,
  select or checkbox and dodojo keeps its value for the Note's owner and puts
  it back when the page opens. A checkbox keeps `true`/`false`; give every
  radio in a group the same key and dodojo keeps the checked one's `value`.
  For anything else (a custom segmented control, a timer's last setting):
  - `window.dodojo?.getState()` returns the saved values at once (an object);
  - `window.dodojo?.setState({ name: value })` saves and returns a Promise
    (keys of letters, digits, `.`, `_`, `:` or `-`; values are strings up to
    4000 characters, numbers, booleans or null; about 32 KB in all);
  - `window` receives a `dodojo-state-change` event, `detail` holding all the
    values, when they change while the page is open (from another device,
    say). Read `getState()` at start and listen for the event as well.
  Outside dodojo `window.dodojo` is undefined and the values last for the
  visit only, so guard every call with `?.`.
  The page's own `setState` does not send `dodojo-state-change` back to
  it: the event comes only for a change from outside (another device, a
  team member, a conditional write that lost). So render from your own
  variables after you save, and let the listener only redraw, never save.
  `data-dodojo-key` fields are filled once the page has loaded, just before
  `window` receives `dodojo-ready`; script that depends on them reads
  `getState()` at start and draws again on that event.
- **Whose state.** Only the owner's values are kept: on a page shared with
  someone else, their changes last for the visit. In a dodojo **team space**
  the values are the team's: everyone who can edit the Note changes the same
  values and sees each change live. `window.dodojo.viewer` is `{ id, name }`
  for whoever is looking, or null (the id is the same for one person on every
  device and differs on every Note); `dodojo.writable` is false for someone
  who may only watch. `setState(patch, { expect: { name: value } })` writes
  only while each named value is still that (null = absent) and resolves
  false otherwise, the page already holding the current values.
- **Several players on their own devices.** A game for several people uses
  `window.dodojo.game`; never keep seats, turns, rounds or restarts in the
  page's own keys.
  ```js
  const game = window.dodojo?.game?.({ seats: ["A", "B"], fresh: round => ({ board: "" }) });
  ```
  `game.state` holds `seats`; `players` (`{ id, name }` or null per seat);
  `mine`; `status` (`"seating"`, `"playing"` or `"over"`); `round`; `first`
  (the seat that starts this round, which moves on every round); `turn`;
  `myTurn`; `winner` (a seat or `"draw"`); `restartBy`; `spectator`; and
  `alone` (true when one device plays every seat). The calls are `sit(seat)`,
  `leave(seat)` (between rounds only), `move(patch, { next, winner })`,
  `update(patch, { turn })` (an undo the rules allow), `resign(patch)`,
  `restart()` (at once when the round is over or nobody else plays; mid-round
  it asks the others) and `answerRestart(yes)`. Each resolves true, or false
  when someone acted first (the page then already holds the current state: say
  so and redraw); `onChange(listener)` follows every change. Write the game's
  own values only through these calls, draw from `game.state`, and say on the
  page whose turn it is, who is waiting for a seat and who asked to restart.
  In a team space, or a game room friends join by typing its code in the
  dodojo app, each player plays from their own device, the last seat taken
  starts the first round, and closing the app does not leave the game;
  elsewhere one device plays every seat. When `dodojo.game` is missing (an
  older app, or outside dodojo), the game is played on one device.
  A party game for however many come passes `min`:
  `dodojo.game({ seats: ["p1", …, "p8"], min: 2, … })` (at most 8 seats).
  Then `game.state.seated` lists the seats taken, `ready` says enough have
  sat, `canStart` says this person may start, and `start()` begins the round
  for those seated; turns go round the seats taken, and someone who arrives
  mid-round sits for the next round. An app whose `game.state.min` is
  undefined predates this: play on one device there. Keep a per-device
  choice (language, sound) out of shared state.
  In detail, as the runtime does it:
  ```js
  game.state === {
    seats: ["A", "B"],
    players: { A: { id: "k3f…", name: "Mia" }, B: null },  // keyed by seat
    me: { id: "k3f…", name: "Mia" },                        // dodojo.viewer, or null
    mine: ["A"],               // the seats this person holds
    shared: true,              // a team space
    status: "seating",         // "seating" | "playing" | "over"
    round: 0, first: null, turn: null, myTurn: false,      // turn: a seat
    winner: null,              // a seat, "draw" or null
    restartBy: null,           // the seat that asked for a restart
    spectator: false, alone: false,
  };
  ```
  - The game's own values (the board, the moves) are ordinary page keys:
    `fresh(round)` returns them, they are written when a round starts, and
    the page reads them with `getState()`. `move(patch, …)` and
    `update(patch, …)` write the page keys in `patch` together with the
    turn, so a result or a record can go in the same `move` as the winning
    move.
  - In a team space `status` is `"seating"` until every seat is taken
    (nobody can move); the last `sit` deals round 1 with `fresh(1)`, and the
    first seat (`seats[0]`, or what `first(round)` returns) moves first. The
    first seat moves on by one every round. Outside a team space round 1 is
    playing at once and `myTurn` is always true: the page moves for every
    seat.
  - A computer opponent is a seat the page moves for: outside a team space
    call `move` for it after the person's move; in a team space the person
    sits in both seats (then `alone` is true) and their device plays the
    computer's.
  - `update` works only while a round is playing: once `move` ends it with
    a winner, the round stays over, so offer review and play again rather
    than undo.
  - `onChange` listeners run after each of the page's own calls (and again
    if one is refused) and on every change from another device.
- **Asking twice without `confirm()`.** A control that throws work away
  (restart, a new game mid-round) changes its label on the first tap ("Tap
  again to restart") and acts on a second tap within about three seconds,
  or acts at once and offers undo.
- **No device features.** Camera, microphone, location, clipboard, screen
  wake lock and vibration are not available inside dodojo. Do not build on
  them; guard any optional use with `try`.
- **Links.** Ordinary `<a href="https://…">` links with text that says where
  they go. dodojo opens websites in the browser and map links in the Maps app.
  `mailto:`, `tel:`, `javascript:` and relative links open nothing. Link a place
  as `https://www.google.com/maps/search/?api=1&query=<place, city>`.
- **The Note scrolls, not the page.** Size by content: no `100vh`, no
  full-screen layouts, no `position: fixed` or `sticky` (they stick to the top
  of the page, not the screen). Do not repeat the Note's title as a big header;
  dodojo shows it above the page. Start with what the page is for.
- **The first screen is the cover.** The library card shows the top square of
  the page (about 400 × 400 CSS px). Make it worth seeing: a strong image or a
  typographic opening with the key facts, never a blank band, a spinner or a
  "loading" state. Nothing waits at `opacity: 0` for an observer.
- **Text without script.** An app that cannot run scripts shows the page's
  plain text instead, and search reads that text. Keep the content in the HTML
  and use script for behavior. Script may switch what is shown and rewrite
  numbers that depend on input (a calculator's results, a schedule's grams),
  but every step, row and sentence is written in the HTML.
- **Size.** Keep the file well under a few megabytes; photos are separate
  files.

## Testing with a stand-in

Outside dodojo, test the page with a stand-in for `window.dodojo` installed
before the page's script runs (Playwright's `addInitScript`). Set the theme
attribute once `<html>` exists, not in the init script itself, where
`document.documentElement` may still be null.

```js
await page.addInitScript(({ saved, theme }) => {
  const state = { ...saved };
  window.__saved = [];
  window.dodojo = {
    getState: () => ({ ...state }),
    setState(patch, options) {
      if (options?.expect && Object.entries(options.expect).some(([k, v]) => (state[k] ?? null) !== v)) return Promise.resolve(false);
      Object.assign(state, patch); window.__saved.push(patch); return Promise.resolve(true);
    },
    viewer: null, writable: true,
  };
  if (theme) document.addEventListener("readystatechange", () => document.documentElement.setAttribute("data-dodojo-theme", theme), { once: true });
}, { saved: { /* a position to start from */ }, theme: "dark" });
```

`scripts/shoot.mjs` installs the same stand-in: `--state '<json>'` opens the
page on a saved position, and `--dodojo-theme` sets `data-dodojo-theme` as
dodojo does instead of relying on `prefers-color-scheme`.
