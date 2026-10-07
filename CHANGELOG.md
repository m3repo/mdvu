# Changelog

*[Deutsche Version](CHANGELOG.de.md)*

All notable changes to mdVü are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions are `Major.Minor.Patch`, and the fourth number in the file version of the EXE is the build counter.

## [Unreleased]

### Fixed

- When the window is made wider, narrow strips of document content no longer flash up between the folder view and the document.

## [0.14.0] — 2026-10-07

### Added

- **Copy with formatting:** `Ctrl+C` in the document now puts the selection on the clipboard as text *and* as HTML, the way a browser does. Pasted into Word, Outlook or OneNote, headings, bold and italics, lists, tables and links arrive as such — with the fonts and colours of the print layout. A heading or list you only partly selected keeps its format. Images go along as links to the original files in their original format (Word embeds them when pasting); relative links and Obsidian embeds are resolved to absolute paths. Callout backgrounds don't arrive in Word yet.
- **Copy as Markdown:** `Ctrl+Shift+C` copies the Markdown source of the selection — starting at a heading or list item, including its `##` or `-`.
- **Context menu in the document:** a right click (or the context-menu key) offers Copy, Copy as Markdown, Back and Forward.
- **Line breaks with `<br>`:** `<br>`, `<br/>` and `<br />` start a new line — inside table cells, too, where Markdown has no other way. See [Inline HTML](docs/markdown-support.md#inline-html).
- **Zoom menu and persistent zoom:** a click on the zoom value in the footer offers all steps from 50 to 200 %. The zoom is kept for the next start (`doc/zoom` in `settings.ini`).
- **Unit menu:** a click on `SCROLL`/`CARET`/`LINK`/`HIT` in the footer opens a menu with all reading units.

### Changed

- In *Search in files*, the scope list is narrower; when opened it is as wide as the longest entry.

### Fixed

- In caret mode, the hover highlight in the footer no longer flickers between the element under the mouse and another one.
- In narrow windows, the buttons of the search strips no longer slide to the left into the folder view.

## [0.13.0] — 2026-10-06

### Added

- **Charts from Mermaid code blocks:** pie charts (`pie`), bar/line charts (`xychart-beta`, also horizontal) and sequence diagrams (`sequenceDiagram` with activations, notes, frames, numbering and participant symbols) are drawn by mdVü itself — a deliberately slimmed-down subset of Mermaid, without JavaScript. The charts follow dark mode and `user.css` and stay vector graphics in print and PDF. Other diagram types remain code blocks; a faulty chart shows its code block with a note naming the line. See [Charts](docs/markdown-support.md#charts-mermaid-subset).
- **Flowcharts from Mermaid code blocks:** `flowchart`/`graph` in all four directions, with the common node shapes, dotted and thick edges, circle and cross ends, edge labels and loops. mdVü arranges the nodes in levels like Mermaid's default renderer, so nodes and labels never overlap and edges cross as rarely as possible. `subgraph` frames and styling statements are skipped for now. See [Flowcharts](docs/markdown-support.md#flowcharts).
- **Reading with the keyboard:** the arrow keys move in a unit you choose, shown in the footer — `0` scroll (as in a browser), `1` caret (`F7` switches between the two), `L` links, `H` search hits. In the link unit `←`/`→` go through the links in reading order, `↑`/`↓` to the nearest link in the line above or below, and `Enter` follows it; `Tab`/`Shift+Tab` always go to the next/previous link. It starts at the first link on screen and works in very large documents too, also in parts not displayed yet. The unit belongs to the place: Back brings it back, including the active link. See [Reading with the keyboard](docs/manual.md#reading-with-the-keyboard).
- **Favorites:** `Ctrl+D` keeps the current folder as a favorite (the star in the toolbar shows it), `Ctrl+Shift+D` opens the list — arrow keys and `Enter` open one, `Del` removes it. Favorites are also in the *File* menu and in the menu of a file or folder, and *Search in files* can search all favorites at once, grouped by favorite. See [Favorites](docs/manual.md#favorites).
- **The file's own menu:** clicking the file path in the status bar opens a menu for that file — copy the path, show it in Explorer, open it in Obsidian (inside a vault) or with another program. A right-click on a file or folder in the folder view, or on the Obs/Git badges, opens the same menu.
- **Menu bar by keyboard:** `F10` or a single `Alt` puts the menu bar into keyboard mode — `←`/`→` choose a menu, `Enter` opens it, `↑`/`↓` and `Enter` run an entry, a letter jumps to it, `Esc` steps back. `Alt`+initial letter opens a menu directly.

### Changed

- **From the search into the document:** in the document search, the first `Enter` searches and every further `Enter` — and `↓` at any time — moves into the document with the unit *hits*, so `←`/`→` walk on through them. In *Search in files*, `Enter` on the result list that is already showing, and `↓` at any time, move into the list with the unit *links*; if the term or options have changed, `↓` searches first. `Esc` steps back one at a time: from the links or hits into the search field, from there out of the strip into the document, scrolling.

### Fixed

- `Enter` and `Esc` in the search fields no longer sound the Windows beep.

## [0.12.1] — 2026-10-03

### Added

- **Links to missing notes or files are shown paler**, like Obsidian's unresolved links — wikilinks and relative Markdown links alike. They stay clickable. Inside a vault the marking follows along when you add or delete a note. The colour can be changed via `a.unresolved` in `user.css`.

## [0.12.0] — 2026-10-03

### Added

- **Search in files:** `Ctrl+Shift+F` searches all Markdown files of the current Obsidian vault, Git repository or folder. The result is a document of its own: files whose name matches first, then the hits grouped by folder with up to three lines of context. A click on a line number opens the file at exactly that hit, with the document search filled in so `F3` walks on. Back returns to the list at the place you left; `F5` searches again. Large folders are searched in the background. Options: match case, beginning of words (`der` finds *derzeit* and *Nord-der*, not *oder*) and whole words. See [Search in files](docs/manual.md#search-in-files).
- **Highlights and inline HTML:** `==text==` highlights like a text marker, as in Obsidian — in print and PDF too. A short list of HTML formatting tags is understood: `<u>`, `<mark>`, `<s>`, `<b>`, `<i>`, `<kbd>` (key caps) and `<span class="…">` for your own styles; every other tag stays literal text. See [Highlights](docs/markdown-support.md#highlights) and [Inline HTML](docs/markdown-support.md#inline-html).
- **Links jump to a section in another document:** `[[Note#Heading]]` and `[details](note.md#installation)` open the document and scroll to the heading. The target may be the anchor name or the heading's text; `[[Note#Chapter 2#Details]]` picks "Details" under "Chapter 2" when the title occurs twice. A link to the document that is already open just jumps. The outline takes the same route: after Back, Forward returns to the heading you last picked there. In large files mdVü jumps as soon as the heading has been loaded; if it is missing, the document opens at the top with a notice in the status bar.
- **Linking to places:** a link `mdvu:open?uri=…&find=term` opens the document, highlights every match like the search does and shows the search strip (`&case`, `&word`, `&hit=3` as in the search). `&mark=12-14` or `&mark=12:5-20` highlight lines or ranges of the source text, as often as you like and in colour if you wish (`~warn`, `~ffcc00`); the colour classes can be changed in `user.css`. `Esc` clears them. See [Linking to places](docs/markdown-support.md#linking-to-places).
- **Back takes you to where you were:** back/forward restores the reading position instead of landing at the top of the document — anchored to the line of text, not to pixels, so it still fits after a change of window width, zoom or piecewise loading. A running search comes back too: term, options, active hit and the search strip.
- **Search in the outline:** `Ctrl+F3` with the focus in the outline filters it to matching headings (with their parents) and highlights the search text — just like the folder view. When you close the search, it is expanded the way it was before.

### Changed

- **The document search covers the whole text**, including parts of large files that haven't been displayed yet. Until now it only found what had already been built — hits further down only showed up once you had scrolled there.
- **Search as you type:** mdVü searches after a short pause (0.3 seconds) and from 3 characters on, so typing stays smooth in large documents too. `Enter` and `F3` search right away, shorter terms as well; a term in quotes (`"ab"`) searches for exactly that text.
- **`F3` / `Shift+F3` always act on the main pane**, even with the focus in the folder view or the outline. Only `Ctrl+F3` depends on where you are.

### Fixed

- Markdown links to another document with an anchor (`other.md#section`) led nowhere.
- Percent-encoded links, as Obsidian writes them (`My%20Note.md`), were not found.
- In very large documents, anchors and the outline could not reach headings that hadn't been loaded yet, and duplicate headings far apart could share the same anchor.
- Crash in very large documents when searching with `F3` or selecting text after scrolling far.
- Crash when dragging with the mouse button held down after clicking a link that jumps far.
- After closing the search in the folder view, the tree was collapsed down to the selected file; it now looks the way it did before the search.

## [0.11.0] — 2026-10-02

### Added

- **Callouts look like in Obsidian:** a coloured box with a title line in the type's colour, in light and dark mode. Without a title, the type name stands in (`> [!warning]` → "Warning"). The colours are Obsidian's defaults; aliases such as `caution` or `tldr` share their group's colour, and unknown types are drawn like `note`. Your `user.css` can restyle every type and its title line (`callout-title`) — see [Colouring callouts](docs/css-customizing.md#colouring-callouts).

### Fixed

- The title of a callout (`> [!note] My title`) was dropped.
- Strikethrough and the underline of links were missing from PDF exports.

## [0.10.1] — 2026-09-30

### Fixed

- **Obsidian comments** (`%%…%%`, inline and as blocks) were shown — and printed. They are now hidden everywhere, including print and PDF.

## [0.10.0] — 2026-09-30

### Added

- **Wikilinks and embeds work like in Obsidian:** inside a vault, `[[Note]]` and `![[picture.png]]` are resolved by name anywhere in the vault — no path, no `.md` needed; with duplicate names the same folder wins, then the one closest to the vault root. mdVü reads the vault's file names in the background and keeps them up to date, so a note or picture added in Obsidian is found right away. `[[#Heading]]` jumps within the document. Outside a vault, `[[Note]]` finds `Note.md` next to the current file.
- **Obsidian vaults and Git repositories are recognised:** the status bar shows **Obs**, **Git** or **Obs/Git** with the folder name; a click opens the vault or repository in the folder view.
- Inside an Obsidian vault, line breaks follow the vault's *Strict line breaks* setting, so notes look as they do in Obsidian. Outside a vault, the new setting `doc/lineBreaks = newline` breaks at every line.

### Fixed

- `[[Note]]` without `.md` used to lead nowhere.
- Line breaks marked by two trailing spaces or a backslash (`\`) were shown as a space; they now break the line, as the Markdown standard requires.

## [0.9.0] — 2026-09-24

### Added

- **Page setup** in the print preview: a strip at the top selects printer, paper size (A3, A4, A5, A6, Letter, Legal) and portrait/landscape. The preview re-paginates immediately, and print and PDF use exactly the format shown. *Printer setup…* opens the Windows printer settings without printing. `Ctrl+Shift+P` shows or hides the strip; the choice is remembered (`print/paper`, `print/orientation`, `print/printer`).

### Changed

- Printing goes through the page setup: the print dialog starts with the chosen printer and paper, and changes made there flow back into the preview — so printer driver and preview always agree on the format.
- The search strip now uses native Windows controls: it follows dark mode and scales cleanly with the display DPI.

### Fixed

- Printouts sit exactly on the paper: the printer's non-printable margin is now taken into account instead of shifting the page by that amount.

## [0.8.0] — 2026-09-16

The first public beta, and the first release under the name **mdVü**. Until version 0.6 the program was called *mdView* and lived inside the m3 library repository; it now has a repository, a version scheme and a release process of its own.

### Added

- **Outline pane** — all headings of the open document as a tree below the folder view; clicking jumps to the spot and flashes the target.
- **Path bar** above the document, with clickable path segments.
- **History** like a browser: back and forward via toolbar icons or `Alt+←` / `Alt+→`, right-click on the arrows opens the history list.
- **Search in every pane**: `Ctrl+F` opens the search strip for the view you are reading, `F3` and `Shift+F3` step through the hits, and `Ctrl+F3` searches wherever the keyboard focus is — the only way to reach the folder view, whose tree is filtered down while you type. `Esc` closes the strip; the search term survives it, so `F3` picks the search up again.
- **Start page** listing the last five documents.
- **PDF export** with a bookmark tree built from the document headings.
- **Crash report**: on an access violation, mdVü writes `mdvu.crash.log` next to the executable. Nothing is sent anywhere — the file is yours to mail in or ignore.
- **Import baseline check** in the release process: the DLL imports of the EXE are compared against a versioned baseline before signing, so that a networking library sneaking in would be caught. mdVü imports no socket DLL at all.
- **Signed releases**: published builds are code-signed and timestamped.

### Changed

- **Renamed to mdVü.** Along with it: the settings folder (`%APPDATA%\m3Works\mdVu`), the file-type identifier for the `.md` association, and the internal URL scheme.
- The document lifecycle moved into the rendering library, which makes loading large files noticeably smoother (the beginning of the document appears immediately, the rest streams in).
- Dark mode is now entirely CSS-driven, so your own `user.css` rules survive a mode switch.
- Wide tables in print and PDF are now *fitted* rather than squeezed: the font shrinks up to 30 %, long-text columns are capped, the rest is cut off at the right margin. The old behaviour is available via `print/tableFit = squeeze`.

### Notes for testers coming from mdView 0.6

The rename is a clean break, on purpose:

- Settings from `%APPDATA%\m3Works\MarkdownView` are **not** migrated — folder, MRU list and your `user.css` need to be set up again.
- An existing `.md` file association still points at the old program. Re-register via *File → Register as Markdown default*.
- The license has to be accepted once more.

## Earlier history

Versions up to 0.6 were released as *mdView* and are not documented here. They brought the core of what mdVü is today: the Markdown renderer with its own layout engine, print and print preview, the folder view, the CSS editor, dark mode, drag & drop, the `.md` file association and the license mechanism.
