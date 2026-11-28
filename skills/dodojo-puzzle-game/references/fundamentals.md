# Fundamentals

- **Theme.** Define every color as a token; components use only tokens, never a
  literal that works in one theme only. Give dark the same care as light: keep
  contrast and keep the accent working on both backgrounds.
- **Phone first.** Most people open the page on a phone (about 360-390px
  wide); on a computer it sits in a column about 920px wide. A 16px side
  gutter, one column at phone width, rows that wrap, `min-width: 0` on flex and
  grid children that hold text, `max-width: 100%` on images. Nothing scrolls
  sideways except a wide table or diagram inside its own `overflow-x: auto`
  box, and a layer moved with `transform` counts: a full-width layer slid
  right widens the page as surely as content does, so move a marker with
  `left` or `right` on a small box. Use relative units.
- **Type.** A set scale kept to; `text-wrap: balance` on headings; running text
  near 65 characters wide on a computer; 16px body on a phone; a little
  letter-spacing on uppercase labels; `font-variant-numeric: tabular-nums`
  where digits line up. For Chinese and Japanese, `line-break: strict`, no
  letter-spacing on body text, and a line height around 1.7; break a
  two-line Chinese heading yourself with `<br>` at a phrase boundary, since
  `text-wrap: balance` can split a word.
- **Spacing with layout.** Flex or grid with `gap`, not per-element margins.
  Repeated elements share edges, baselines, padding and the position of their
  recurring parts. Let content set heights; pick column counts the items fill.
- **Cards by role.** Border, fill, radius and shadow mark a separate object.
  Use them to set off what needs it, not on every block.
- **Structure is information.** Numbering, eyebrows and dividers must say
  something true (day 1, day 2 is a real sequence; 01/02/03 on unrelated
  sections is decoration).
- **Interaction.** Controls look like controls; tap targets at least 44px tall
  on a phone; visible keyboard focus; state shown in form as well as words (a
  chip, a check, a stripe). Tabs and filters work without scrolling to find
  their result.
- **Motion.** One orchestrated moment beats scattered effects, and less is
  often more. Everything rests visible. Respect `prefers-reduced-motion`.
- **Charts.** To scale, with labels that name values the chart reaches, text
  colored from the tokens. Inline SVG is usually enough.
- **Copy.** Write in the person's language (set `<html lang>`), from their side
  of the screen, plainly and specifically. Active voice; a control says what
  happens. No mannered asides, no "not X but Y", no stock phrases. Units and
  currencies as the place uses them, joined to their number with a no-break
  space (`93&nbsp;°C`, `1&nbsp;200&nbsp;¥`) so they never wrap apart.
- **Several languages on one page.** When a page carries more than one
  language, keep every sentence of each in the HTML, so search and the apps
  that cannot run scripts still read them: mark each copy with its language
  and show only the chosen one with CSS.
  ```html
  <p class="howto"><span lang="en">Tap a pit to sow.</span><span lang="zh">点一个坑开始播种。</span><span lang="ja">穴をタップして種をまく。</span></p>
  <style>:root[data-lang="en"] [lang="zh"], :root[data-lang="en"] [lang="ja"], :root[data-lang="zh"] [lang="en"], :root[data-lang="zh"] [lang="ja"], :root[data-lang="ja"] [lang="en"], :root[data-lang="ja"] [lang="zh"] { display: none; }</style>
  ```
  Pick the default from `navigator.languages`, offer a small switch, keep the
  choice with `setState`, and set `data-lang` and `lang` on `<html>`. Short
  labels that script rewrites (a button's state) may live in a dictionary in
  the script. Write each language for its readers rather than translating
  word for word, and fit the longest label in each.
- **Sources.** Link the source of every fact that could be wrong, with the
  date you checked it. When the primary source is closed (a members-only
  standard, a paywall), cite the public page that quotes it and say so; never
  cite what you could not read.
- **Clean build.** Close every element, quote attributes, give every image alt
  text, and keep the file small.
