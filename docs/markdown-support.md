# Markdown support

*[Deutsche Version](markdown-support.de.md)*

mdVü reads **GitHub-flavoured Markdown (GFM)**, plus the two Obsidian extensions that matter most for reading notes: callouts and wikilinks. This page lists what is actually rendered, what is rendered *differently* than in a browser, and what is deliberately left out.

The philosophy behind the omissions: mdVü renders Markdown directly into a layout tree — there is no HTML, no browser, no DOM in between. That's where the speed and the small memory footprint come from, and it's also why a handful of browser-only features don't exist here.

Want to see it all at once? Open [`samples/showcase.md`](../samples/showcase.md) in mdVü.

## Block elements

| Syntax | Notes |
|---|---|
| `# Heading` … `###### Heading` | six levels |
| `Heading` + `=====` / `-----` | Setext headings work too |
| Paragraphs | a blank line separates them |
| Two spaces or `\` at end of line | hard line break inside a paragraph |
| `- item`, `* item`, `+ item` | unordered lists, nestable |
| `1. item`, `1) item` | ordered lists; the first number is respected, so a list may start at 5 |
| `- [ ] todo`, `- [x] done` | task lists with checkboxes |
| `> quote` | block quotes, nestable |
| `> [!note] Title` | callouts — see below |
| ` ```lang … ``` ` | fenced code blocks with syntax highlighting; `~~~` works as a fence too |
| four leading spaces | indented code block |
| `\| a \| b \|` + `\|---\|---\|` | GFM tables — see below |
| `---`, `***`, `___` | horizontal rule |
| `---` … `---` at the top of the file | YAML front matter — see below |

## Inline elements

| Syntax | Result |
|---|---|
| `*italic*`, `_italic_` | *italic* |
| `**bold**`, `__bold__` | **bold** |
| `***both***` | nesting works in any combination |
| `~~struck~~` | struck through, with a real strike line |
| `` `code` `` | inline code, in its own colour |
| `[text](url)`, `[text](url "title")` | link |
| `<https://example.com>` | autolink |
| `https://example.com`, `www.example.com` | bare URLs are linked as well |
| `![alt](picture.png)` | image — see below |
| `[[Target]]`, `[[Target\|Alias]]` | wikilink |
| `![[picture.png]]` | image embed |
| 🎉 emoji | rendered in colour, not as a monochrome outline |
| `<b>raw HTML</b>` | shown as literal text — see [What is not supported](#what-is-not-supported) |

Emphasis is parsed tolerantly: an unbalanced `**bold with no end` stays plain text instead of swallowing the rest of the paragraph.

## Tables

```markdown
| Left | Centre | Right |
|:-----|:------:|------:|
| a    |   b    |     c |
```

- The alignment row (`:---`, `:---:`, `---:`) is honoured, on screen and in print.
- A table **needs a header row**. Rows without a valid `|---|` separator line stay a paragraph — that's GFM behaviour, and it stops accidental pipe characters from turning prose into a table.
- Ragged rows are tolerated: too few cells are padded, extra ones dropped, based on the header's column count.
- Cells hold inline markup (bold, code, links), not block elements.
- Very wide tables are automatically fitted when printing — see the [manual](manual.md#printing-and-pdf).

## Links and anchors

- **Relative links** (`[Manual](manual.md)`) are resolved against the folder of the current document and open that file in mdVü.
- **Anchors** (`[to the section](#tables)`) jump inside the document. The anchor name is derived from the heading: lower-cased, spaces become hyphens, hyphens and underscores are kept, everything else (punctuation, symbols) is dropped. `## Links and anchors` therefore becomes `#links-and-anchors`. Duplicate headings are numbered: `#notes`, `#notes-1`, `#notes-2`. This matches the convention GitHub uses, so the same link usually works in both places.
- **`http(s)` links** open in your default browser after a confirmation.
- Links to anything else are refused rather than followed. mdVü never opens an executable or a shell command from a document.

In a very large document that is loaded in chunks, an anchor further down may not exist yet at the moment you click it — the jump then does nothing. Scroll a bit and try again.

## Images

```markdown
![Alt text](img/screenshot.png)
![Alt text|620](img/screenshot.png)      width 620
![Alt text|620x400](img/screenshot.png)  width 620, height 400
![[diagram.svg]]                         Obsidian embed
```

- Formats: PNG, JPEG, GIF, BMP, TIFF and SVG, plus `data:` URIs.
- **An image must be a paragraph of its own.** A picture in the middle of running text (`see ![this](a.png) here`) is *not* rendered — only its alt text appears. Put it on its own line, separated by blank lines.
- Several images in one paragraph end up side by side; a hard line break between them puts them on separate rows. A link around an image works (`[![alt](pic.png)](target.md)`).
- The size suffix `|width` / `|widthxheight` is the Obsidian convention. Given a width only, the height follows proportionally. Other Markdown tools show the suffix as part of the alt text — harmless, and the reason this manual uses it too.
- Paths are resolved relative to the document.
- **Images are never fetched from the internet** — mdVü has no network access at all. An `https://…` image source stays an alt text.
- Unreadable or missing files are skipped silently, leaving the alt text.

## Code blocks and syntax highlighting

Fenced blocks are highlighted when the fence names a language:

````markdown
```python
def answer() -> int:
    return 42
```
````

Recognized names (aliases in brackets):

| Language | Fence name |
|---|---|
| Pascal / Delphi | `pascal`, `delphi`, `pas`, `dpr` |
| C / C++ | `c`, `cpp`, `h`, `hpp`, `cc` |
| C# | `cs`, `csharp` |
| Java | `java` |
| JavaScript / TypeScript | `js`, `javascript`, `jsx`, `ts`, `typescript`, `tsx` |
| Python | `python`, `py` |
| Go | `go` |
| Rust | `rust`, `rs` |
| Kotlin / Swift / PHP | `kotlin`, `kt`, `swift`, `php` * |
| Lua | `lua` |
| Shell | `sh`, `bash`, `zsh`, `shell` |
| SQL | `sql`, `tsql`, `mysql`, `pgsql` |
| VB / VBScript | `vb`, `vbs`, `vbscript`, `basic` |
| CSS | `css` |
| Markdown | `markdown`, `md` |
| JSON | `json` |
| YAML | `yaml`, `yml` |
| INI / TOML | `ini`, `conf`, `cfg`, `toml`, `properties` |

\* For these three, comments, strings and numbers are highlighted, but keywords are not yet.

An unknown language is not a problem: the block simply stays in the plain code colour rather than being coloured wrongly. Highlighting distinguishes comments, strings, numbers, keywords and identifiers — the colours come from the stylesheet, so you can [change them](css-customizing.md#code-highlighting).

[`samples/code-samples.md`](../samples/code-samples.md) shows the highlighting for a dozen languages side by side.

## Callouts

```markdown
> [!note] Worth knowing
> Callouts are quotes with a type.

> [!warning]
> The title is optional — the type alone will do.
```

The type is passed through to the stylesheet as a CSS class, so you can give `note`, `warning`, `tip` and friends their own colours in your `user.css`. Out of the box they render as ordinary block quotes: the built-in stylesheet doesn't ship colour schemes for them yet. Any type name works — mdVü doesn't police the list.

The fold marker (`> [!note]-`) is parsed but not acted upon; the content is always shown.

## Wikilinks

```markdown
[[Other note.md]]              link to a file next to this one
[[Other note.md|see there]]    with display text
![[picture.png]]               embed a picture
```

Wikilinks are shown as links and the target is resolved relative to the current document — but **the target is used verbatim, extension included**. `[[Other note]]` without `.md` therefore looks like a link and leads nowhere: mdVü does not search the folder for a matching note the way Obsidian does. Write the file name in full and it works.

`![[note.md]]` — transclusion of another *note* — is **not** supported; only image embeds are.

## Front matter

A YAML block delimited by `---` at the very beginning of the file is recognized as front matter and shown as a dimmed monospaced block, fences included. It is deliberately *not* hidden: in a viewer, metadata is content — you usually want to see the tags and the date.

It has its own style tag, so hiding it is a two-line change in your `user.css`:

```css
frontmatter { display: none; }
```

## What is not supported

| Not supported | What happens instead | Why |
|---|---|---|
| HTML blocks (`<div>…</div>`) | skipped, nothing is shown | there is no HTML pipeline — mdVü renders Markdown directly |
| Inline HTML (`<b>x</b>`) | shown as literal text | same reason |
| Reference links (`[text][id]` plus a definition block) | stays plain text | needs a second pass over the document |
| Footnotes (`[^1]`) | stays plain text | planned as an option, not implemented |
| Definition lists | stays plain text | rarely used in notes |
| Math / LaTeX (`$…$`) | stays plain text | would need a formula engine |
| Mermaid and other diagram fences | shown as a code block | rendering diagrams is a different program's job |
| Note transclusion (`![[note]]`) | stays plain text | only image embeds are resolved |

If you rely on one of these, the source view (`Ctrl+2`) always shows the file exactly as it is on disk.

## Limits

Three hard limits protect the viewer against pathological files: 50 MB per document, 200 pages for print/preview/PDF, and 100 KB per paragraph. See the [manual](manual.md#limits) for what happens when a limit is reached.

---

*[Back to the README](../README.md)*
