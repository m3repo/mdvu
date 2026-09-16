# Customizing the display with CSS

*[Deutsche Version](css-customizing.de.md)*

mdVü renders your documents with a small, built-in stylesheet. `Ctrl+4` opens **your own** stylesheet on top of it — change the font, the colours, the spacing, the code highlighting. The file is called `user.css`, lives in the settings folder (`%APPDATA%\m3Works\mdVu`) and survives updates.

This page is the reference: how the cascade works, which selectors and properties exist, and where the traps are.

> **The short version:** keep the `@import` line at the top, write your rules below it, use `pt` for sizes, and switch back to the Markdown view (`Ctrl+1`) to see the result.

A complete, commented starting point is in [`samples/example-user.css`](../samples/example-user.css).

## The cascade

Your stylesheet is not the only one. mdVü assembles the sheet for every document like this:

1. **A minimal fallback** — fonts only, no colours. Always present.
2. **`builtin:default.css`** — the built-in design, *only* if the `@import` line below is in your `user.css` (or your `user.css` is empty).
3. **`builtin:default-dark.css`** in dark mode, or **`builtin:print.css`** for print, preview and PDF.
4. **Your `user.css`** — last, and therefore the winner on equal specificity.

The switch for step 2 is this line, which a fresh `user.css` comes pre-filled with:

```css
@import "builtin:default.css";
```

Keep it and your rules are layered on top of the built-in design. Remove it from a non-empty `user.css` and you get neither the default sheet nor its dark counterpart — a blank canvas, which is exactly what you want if you're designing from scratch and exactly what you don't want if you just wanted to bump the font size.

Two consequences worth knowing:

- **There is no separate stylesheet for dark mode.** Your `user.css` applies to light *and* dark. If you hard-code `color: #202020` for paragraphs, you get dark grey text on a dark background when you switch. Better: only set what you actually need, and let the built-in dark sheet handle the colours.
- **Your rules also apply to print and PDF.** The print stylesheet comes *before* yours in the cascade, so it loses against your rules. A coloured heading in `user.css` therefore prints in colour. There is no `@media print` — if you want different output on paper, that's not currently possible in one file.

## Selectors

Every block element in the document carries a style tag; those are your selectors.

| Selector | Applies to |
|---|---|
| `body` | the document surface — background colour and inherited base font |
| `frame` | the outer frame around the page area (follows `body` unless set) |
| `p` | paragraphs |
| `h1` … `h6` | headings |
| `a` | links (colour only) |
| `code` | inline code *and* the base colour of code blocks |
| `pre` | the box around a code block |
| `blockquote` | block quotes and callouts |
| `frontmatter` | the YAML block at the start of the file |
| `table`, `tr`, `th`, `td` | tables, rows, header cells, data cells |
| `ul`, `ol`, `li` | lists and list items |
| `hr` | horizontal rules |
| `img` | images |

What works beyond plain tags:

```css
.klasse { … }              /* a style class, e.g. .code-comment */
blockquote.warning { … }   /* tag plus class — callouts land here */
* { … }                    /* everything */
tr:nth-child(2n+3) { … }   /* nth-child, counting ALL children */
```

What does **not** work — the rule is ignored, without an error message:

- combinators `>`, `+`, `~`, and descendant chains longer than one level
- pseudo-elements (`::before`, `::after`), attribute selectors (`[href]`)
- `!important` — precedence is decided by specificity and, on a tie, by source order (yours is last, so yours wins)
- `@media` queries of any kind

Specificity: a tag counts 1, a class counts 10. On a tie, the later rule wins.

## Properties

### Text (inherited)

| Property | Values |
|---|---|
| `font-family` | a fallback list: `'Lora', Georgia` — the first **installed** family wins |
| `font-size` | `12pt`, `16px` — **prefer `pt`**, see [Units](#units) |
| `font-weight` | `bold`, `normal`, or a number (600 and up counts as bold) |
| `font-style` | `italic`, `normal` |
| `line-height` | `normal`, or a **factor** like `1.4` (recommended), or a length |
| `color` | any colour, see below |
| `text-align` | `left`, `right`, `center`, `justify` (currently falls back to left) |

### Box (not inherited)

| Property | Notes |
|---|---|
| `background-color` | `background` is accepted as a shorthand for the colour |
| `padding`, `margin` | 1–4 lengths. **Margins add to the container's `gap`** — no collapsing |
| `border` | shorthand: `1px solid #888`; styles `solid dashed dotted double none` |
| `border-width`, `-color`, `-style`, `-radius` | also per side or corner (`border-top`, `border-top-left-radius`) |
| `width`, `height` | absolute length or `auto`; **border-box** — border and padding come out of the content |
| `min-width`, `max-width`, `min-height`, `max-height` | absolute lengths |
| `gap`, `row-gap`, `column-gap` | space between the children of a container |
| `justify-content` | `start`, `center`, `end`, `space-between`, `space-around` |
| `align-self` | `start`, `center`, `end` — note there is **no `align-items`** |
| `overflow` | `visible`, `hidden`, `clip` (the engine doesn't scroll inside boxes) |
| `vertical-align` | `top`, `middle`, `bottom` |
| `line-clamp` | `N` — at most N lines, ending in "…" |
| `display` | `none` hides an element completely; anything else shows it |

**Colours:** hex (`#fff`, `#ffffff`), CSS names (`rebeccapurple`), `rgb()` / `rgba()`, and `transparent`.

## Units

This is the one thing worth memorising:

| Works | Doesn't work |
|---|---|
| `px` (96-dpi reference pixels), `pt`, `mm`, `cm`, `in` | `em`, `rem`, `%`, `vw`, `vh`, `ch` |

Relative units cannot be resolved and the whole declaration is dropped. `font-size: 1.2em` doesn't make the text bigger — it does nothing at all.

Use `pt` for font sizes. Point sizes scale correctly with the screen DPI, so the same document looks right on a 4K laptop and on a 1080p monitor. `line-height` is the exception: give it a plain number (`1.45`), which is a factor and behaves as you'd expect.

## Worked examples

### A different reading font

```css
body, p, li, td {
  font-family: 'Georgia', 'Times New Roman';
  font-size: 12pt;
  line-height: 1.5;
}
```

Font size and family are inherited, but headings and code carry their own rules from the default sheet, so they stay put unless you change them too.

### Calmer headings

```css
h1 {
  font-size: 20pt;
  border-top: none;
  border-bottom: 1pt solid #d0d0d0;
  padding: 0 0 4px 0;
}
h2 { border-left: none; font-size: 15pt; }
```

### Code highlighting

Token colours come from six classes. Overriding them is the tidiest way to get your own code theme:

```css
.code-comment { color: #6a737d; font-style: italic; }
.code-string  { color: #032f62; }
.code-number  { color: #005cc5; }
.code-keyword { color: #d73a49; font-weight: bold; }
.code-ident   { color: #24292e; }
.code-plain   { color: #24292e; }
pre { background-color: #f6f8fa; padding: 8px; }
```

Only `color`, `font-weight` and `font-style` are evaluated per token — a background belongs on `pre`, not on a token class.

### Colouring callouts

Callout types arrive as a class on the block quote, so each type can look different:

```css
blockquote.note    { background-color: #eaf2fb; border-left: 3pt solid #4a80c0; }
blockquote.warning { background-color: #fdf0e6; border-left: 3pt solid #d08030; }
blockquote.tip     { background-color: #eaf7ee; border-left: 3pt solid #3d9a5c; }
```

The type name is whatever you wrote in `> [!name]` — mdVü doesn't keep a list of allowed ones.

### Hiding front matter

```css
frontmatter { display: none; }
```

### Zebra striping in tables

Row index 1 is the header, so the data rows are the odd indices from 3 onwards:

```css
tr:nth-child(2n+3) { background-color: #f2f6fa; }
th { background-color: #dde5ee; }
```

### Tighter spacing

```css
body { gap: 4px; }        /* space between blocks */
ul, ol { row-gap: 2px; }  /* space between list items */
```

Remember that margins add on top of the gap rather than collapsing into it. If you port CSS from a browser, either subtract the gap from your margins or set `row-gap` explicitly.

## Why my rule doesn't apply — a checklist

1. **Is the `@import` line still there?** Without it — and with a non-empty `user.css` — the entire default design is gone, which usually looks like "everything broke", not like "one rule is missing".
2. **A relative unit?** `em`, `%`, `rem` are dropped silently. Use `pt` or `px`.
3. **A selector the document doesn't produce?** There is no `strong`, `em`, `span` or `div` — inline markup is rendered inside a text run, not as its own element. Bold and italic cannot be styled separately.
4. **A combinator?** `blockquote > p` is ignored. One descendant level (`blockquote p`) is the maximum.
5. **`!important`?** Not supported — and not needed, because your sheet comes last anyway.
6. **Did you switch back to the Markdown view?** The stylesheet is applied when you leave the CSS view (`Ctrl+1`).
7. **Dark mode on?** The dark sheet is loaded *before* yours, so your rules win — but a colour you only meant for light mode will also apply in dark mode.

## Where the file lives

`%APPDATA%\m3Works\mdVu\user.css`

The CSS view writes it through immediately, so an external editor sees your changes right away. In the other direction — editing the file from outside while mdVü is running — close the program first, otherwise the running instance overwrites your edits.

---

*[Back to the README](../README.md)*
