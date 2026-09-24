# mdVü — Manual

Markdown viewer for Windows · © 2026 Martin Niedergesäß — m3Works · *[Deutsche Version](manual.de.md)*

---

This is the extended manual for readers who want the whole picture, including installation, settings and troubleshooting. A shorter version ships inside the program — press `F1`.

**Contents**

- [Why a Markdown viewer?](#why-a-markdown-viewer)
- [Installation and first start](#installation-and-first-start)
- [The window at a glance](#the-window-at-a-glance)
- [Opening files](#opening-files)
- [Folder view and search](#folder-view-and-search)
- [Outline](#outline)
- [Path bar, back and forward](#path-bar-back-and-forward)
- [The four views](#the-four-views)
- [Printing and PDF](#printing-and-pdf)
- [Dark mode](#dark-mode)
- [Customizing the display](#customizing-the-display)
- [Settings](#settings)
- [Limits](#limits)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Command line](#command-line)
- [Troubleshooting](#troubleshooting)
- [Uninstalling](#uninstalling)

## Why a Markdown viewer?

There are excellent Markdown *editors* — Obsidian, Typora, VS Code and many more. So why a viewer?

Because reading is not writing. If you just want to look up a note, skim a document or simply *view* an `.md` file someone sent you, you don't need an editor with plugins, vaults and sync — you need a program that starts instantly, shows the file and gets out of your way.

That's exactly what mdVü is built for:

- **Lean:** a single EXE under 15 MB, no frameworks or runtimes to install.
- **Fast:** a native Windows application with its own rendering engine. Even large documents open without noticeable delay.
- **Light on memory:** uses a fraction of the RAM of Chromium-based editors, which ship a complete browser with every window.
- **A companion, not a replacement:** mdVü doesn't try to displace Obsidian & co. It's the tool for the quick look — double-click a file in Explorer, read, done. Your editor stays in charge of writing.

## Installation and first start

There is no installer. mdVü is a single executable:

1. Put `mdvu.exe` wherever you like — a program folder, a USB stick, a synced folder. It runs from anywhere.
2. Start it. On the very first start the license is shown and has to be accepted once.
3. Optional: *File → Register as Markdown default* makes `.md` files open in mdVü on double-click.

Nothing is installed system-wide, no admin rights are required, and no services or scheduled tasks are created. The program writes to exactly two places outside its own folder — see [Uninstalling](#uninstalling).

**If SmartScreen warns you:** published builds are code-signed and timestamped, but Windows also considers *reputation*, which a new build has yet to earn. „More info → Run anyway" starts the program; you can verify the signature beforehand via *Properties → Digital Signatures*.

## The window at a glance

![mdVü main window (stylized)|620](img/mdvu-window.svg)

The window has no classic menu bar — the **main menu sits in the title bar** (*File*, *View*, *Help*), next to the toolbar icons.

Below that, the window is split:

- **left, top:** the **folder view** — the current folder as a tree, `.md` files only
- **left, bottom:** the **outline** of the open document — all headings as a tree
- **right, top:** the **path bar** with the location of the current file
- **right, centre:** the **document**
- **bottom:** the status bar with document information and notices

`F6` cycles the keyboard focus between the panes.

## Opening files

There are several ways to open a file:

- **Drag & drop:** drop an `.md` file or a whole **folder** onto the window. A folder opens in the folder view. If you drop several things at once, a file takes precedence over a folder.
- **Open dialog** with `Ctrl+O`.
- **Folder view:** clicking a file in the folder tree on the left shows it immediately — the view also follows as you move through the tree with the arrow keys.
- **Recently used:** the *File* menu lists recently opened files and folders. The **start page** (*File → Start page*) also shows the last five files.
- **Double-click in Explorer:** *File → Register as Markdown default* associates mdVü with `.md` files (per user, no admin rights required). Windows may ask once via "Open with" — see [Troubleshooting](#troubleshooting).
- **Command line:** `mdvu.exe "C:\Notes\Readme.md"` — see [Command line](#command-line).

If the displayed file is changed by another program, mdVü reloads it automatically — the scroll position is preserved. `F5` does the same manually. Files that appear in or disappear from the current folder show up in the tree without a manual refresh; this works recursively, for subfolders too.

Very large files are loaded up to a limit of **50 MB** — a banner at the top of the document indicates that only the beginning is shown. See [Limits](#limits).

## Folder view and search

The folder view shows the folder of the current document, filtered to `*.md`. It is not a vault and not a workspace: it's simply the folder you are in, and it follows you as you navigate.

`Ctrl+F` opens the search strip for the main pane — the view currently showing: document, source text, CSS or print preview. `F3` and `Shift+F3` step to the next and previous hit; they work from the search field as well as from the document itself, so you can keep reading and press `F3` to move on.

`Ctrl+F3` searches wherever you are — the pane holding the keyboard focus gets the strip. It is the only way to reach the folder view, and unlike `Ctrl+F` it also switches the strip off again.

In the **folder view** the strip appears above the tree. As you type, the tree is filtered to matching files and hits are highlighted in the name. The arrow-down key moves the focus from the search field into the tree, so you can type, then browse without touching the mouse.

In the **document, source text, CSS editor and print preview** the strip appears below the path bar and works like a browser's find bar: `Enter` and `Shift+Enter` step through the hits, a counter shows *hit / total*, and all hits are highlighted at once. Three toggles refine the search:

| Toggle | Meaning |
|---|---|
| `Aa` | Match case (off by default) |
| `.*` | Read the search term as a regular expression |
| `Sel` | Restrict the search to the current selection (document only; needs a non-empty selection) |

`Ctrl+F3` again, `Esc` or the `X` button closes the strip — highlights disappear, the folder filter is lifted. The search term itself is kept: `Ctrl+F` brings it back into the field, and `F3` resumes the search from the first hit. That also means `F3` can leave highlights in the document without a visible strip; `Esc` in the document clears them.

Only one strip is open at a time, and switching views closes it.

Note on the print preview: it searches what has actually been paginated. Documents cut off at the 200-page limit end there for the search as well.

## Outline

Below the folder view, mdVü shows the **outline** of the current document — all headings as a tree, nested by level. A click jumps to that position in the document; the target flashes briefly so your eye finds it right away.

For a long document, the outline is the fastest way around: no scrolling, no searching, one click.

## Path bar, back and forward

Above the document, the **path bar** shows the location of the current file. Every segment is clickable: clicking a folder opens it in the folder view.

mdVü navigates its history like a browser: the arrow icons in the toolbar or `Alt+←` / `Alt+→` step back and forward. **Right-clicking the arrows** opens the history list, so you can jump straight to any earlier document instead of stepping through them.

Links inside documents work as you'd expect: a relative link to another `.md` file opens that file; a link to a heading (`#section`) jumps within the document; an `http(s)` link opens in your browser after a confirmation. Links that lead nowhere sensible are refused rather than followed.

## The four views

The document area holds four interchangeable views:

| View | Shortcut | What it's for |
|---|---|---|
| **Markdown** | `Ctrl+1` | the rendered document — the normal view |
| **Source** | `Ctrl+2` | the raw Markdown text, syntax-highlighted, read-only |
| **CSS** | `Ctrl+4` | your own stylesheet, see [Customizing the display](#customizing-the-display) |
| **Print preview** | `Ctrl+F2` or `Ctrl+3` | the paginated document as it will print |

Switching back from CSS to the Markdown view applies your changed stylesheet immediately.

## Printing and PDF

mdVü comes with its own print and PDF output — no detour through a browser or a PDF printer driver:

- **Print preview** (`Ctrl+F2`): even for long documents, 100 pages are ready in a few seconds.
- **Page setup:** a strip at the top of the print preview selects the printer, the paper size (A3, A4, A5, A6, Letter, Legal) and portrait or landscape. The preview is laid out anew right away, and print and PDF use exactly this format — what you see in the preview is what comes out of the printer. *Printer setup…* opens the Windows printer settings without printing; printer, paper size and orientation chosen there are taken over. Show or hide the strip with `Ctrl+Shift+P` (*View → Page setup*), close it with `Esc`. The choice is remembered. Paper sizes outside the list above are not supported yet; if the printer dialog returns one, mdVü keeps the size set in the strip.
- **Native PDF:** *View → Export as PDF* produces a true vector PDF with selectable text and a PDF outline built from the document's headings. The files are usually smaller than "Print to PDF" via a printer driver.
- **Clean page breaks:** orphaned lines are taken into account — a single line of a paragraph is never left alone at the top or bottom of a page.
- **Wide tables** are fitted automatically: the font shrinks moderately (down to 70 %), anything still wider is cut off at the right page edge — so put the important columns first. Long-text columns are capped at 30 % of the page width when space is tight. The previous behaviour (squeeze all columns onto the page) is available via the setting `print/tableFit = squeeze`.
- **Print** straight from the view with `Ctrl+P`. The print dialog starts with the printer and paper from the page setup, and changes made there flow back into the preview.

Print and PDF output is always light, regardless of the dark mode setting — a dark page background would waste toner and read badly on paper. Preview, print and PDF are limited to the first **200 pages**; a note appears in the status bar when a document is cut off.

## Dark mode

*View → Dark Mode* switches the whole UI including the document. The setting is remembered.

Dark mode in the document is entirely CSS-driven: the built-in dark stylesheet is layered on top of the light one. This matters when you write your own CSS — see [Customizing with CSS](css-customizing.md), which explains why a colour you set only for dark mode can "stick" when you switch back.

## Customizing the display

*View → CSS* (`Ctrl+4`) opens your own stylesheet, which is applied on top of the built-in defaults. Use it to adjust things like font, font size, colours and spacing. The file (`user.css`) lives in the settings folder and survives updates.

On first start it is pre-filled with a comment and one line:

```css
@import "builtin:default.css";
```

That line is the switch for the built-in design. Keep it and your rules are layered on top of the defaults. Delete it from a non-empty `user.css` and mdVü loads neither the default stylesheet nor its dark counterpart — you are designing from scratch.

Good to know: mdVü deliberately supports only a **subset** of CSS — not everything a browser can do with HTML5. The scope is intentionally kept small; that's exactly where mdVü's speed and low memory footprint come from. Tip: specify font sizes in `pt` so the display scales cleanly with screen DPI.

The full reference with worked examples is in [Customizing with CSS](css-customizing.md).

## Settings

There is no settings dialog yet. *Help → Setting* opens a small note with a clickable link to the settings folder:

```
%APPDATA%\m3Works\mdVu
```

It contains `settings.ini` (values) and `user.css` (your stylesheet). Values are written through immediately — mdVü never loses a setting on a crash, but it also means **you should close the program before editing `settings.ini` by hand**, otherwise your changes will be overwritten.

Keys are hierarchical: everything before the slash is the INI section, everything after is the key name. `doc/maxLoadMB = 80` therefore looks like this in the file:

```ini
[doc]
maxLoadMB=80
```

The values worth knowing about:

| Key | Meaning |
|---|---|
| `doc/maxLoadMB` | load limit for a single document in MB (default 50) |
| `print/paper` | paper size: `A3`, `A4` (default), `A5`, `A6`, `Letter`, `Legal` — written by the page setup strip |
| `print/orientation` | `portrait` (default) or `landscape` |
| `print/printer` | printer name; empty means the Windows default printer |
| `print/tableFit` | how wide tables are fitted: `shrink` (default) or `squeeze` |
| `print/tableMaxColPct` | maximum width of a long-text column in percent of the page (default 30) |
| `print/tableMinFontPct` | how far the font may shrink when fitting, in percent (default 70) |
| `ui/theme`, `ui/mode` | named stylesheet and light/dark/system — written by the Dark Mode command |
| `ui/currentFolder` | folder restored on the next start |
| `ui/pageSetupBar` | show the page setup strip in the print preview (on by default) |
| `ui/fileMru`, `ui/folderMru` | recently used files and folders |
| `ui/resizeBudgetMs`, `ui/resizeSettleMs`, `ui/resizeRefreshMs` | timing of the re-layout while a window is being resized |

## Limits

mdVü has a few deliberate hard limits. They exist so that an unusual file cannot freeze the program:

| Limit | Value | What happens |
|---|---|---|
| File size | 50 MB | only the beginning is displayed, with a yellow banner at the top; adjustable via `doc/maxLoadMB` |
| Pages in preview / print / PDF | 200 | output is cut off, with a note in the status bar |
| Single paragraph | 100 KB | an over-long paragraph is split (this affects generated files, not hand-written prose) |

## Keyboard shortcuts

| Key | Function |
|---|---|
| `Ctrl+O` | Open file |
| `F1` | Manual |
| `Ctrl+F` | Search in the main pane |
| `F3` / `Shift+F3` | Next / previous hit |
| `Ctrl+F3` | Search in the focused pane on/off (incl. folder view) |
| `Esc` | Close the search strip / clear the highlights |
| `F5` | Reload document |
| `F6` | Switch between panes (tree / document / editor) |
| `Alt+←` / `Alt+→` | Back / forward |
| `Ctrl+1` | Markdown view |
| `Ctrl+2` | Source view |
| `Ctrl+3` / `Ctrl+F2` | Print preview |
| `Ctrl+4` | Edit CSS |
| `Ctrl+P` | Print |
| `Ctrl+Shift+P` | Page setup strip in the print preview on/off |

## Command line

```
mdvu.exe "C:\Notes\Readme.md"     open a file
mdvu.exe "C:\Notes"               open a folder
mdvu.exe -accepteula              accept the license non-interactively
```

The first parameter may be a file or a folder; a file is opened, a folder shown in the folder view. This is also the mechanism behind the Explorer file association.

`-accepteula` is meant for unattended setups where the first-start dialog would be in the way — it records the acknowledgement exactly as clicking *Accept* would.

## Troubleshooting

**Double-clicking an `.md` file still opens the old program.**
Windows keeps its own user choice for file types, which takes precedence over an application's registration. Right-click the file → *Open with* → *Choose another app* → mdVü → *Always*. After that the association sticks.

**A picture in the document isn't shown.**
mdVü resolves relative image paths against the document's own location, so a picture must be reachable from there. Images from the internet are not fetched — the program has no network access at all. Supported formats are the usual Windows ones (PNG, JPEG, GIF, BMP, TIFF, SVG); an unreadable file is skipped rather than reported.

**My CSS rule has no effect.**
The most common causes are: a unit the engine cannot resolve (use `pt`, `px`, `mm`, `cm` or `in` — *not* `em` or `%` for sizes), a selector for something the document doesn't produce, or the `@import` line having been removed from `user.css`. The [CSS documentation](css-customizing.md) has a checklist for exactly this.

**The document looks fine on screen but wrong on paper.**
Print, preview and PDF use a separate stylesheet and are always light. Rules that only exist in your dark-mode block have no effect there.

**The window is dark but the document stayed white** (or vice versa).
Switch dark mode off and on again. If it persists, it's worth reporting — please mention whether it happened right after the first start.

**The program crashed.**
mdVü writes `mdvu.exe.crash.log` next to the executable. The file contains the error location and a stack dump, no document content. Nothing is sent anywhere — mailing it in is entirely your decision, and it makes fixing the bug much more likely.

## Uninstalling

Delete `mdvu.exe`. Optionally also:

- the settings folder `%APPDATA%\m3Works\mdVu` (settings and your `user.css`)
- the registry key `HKCU\Software\m3Works\mdVu` (the license acknowledgement)
- the file association, via *File → Remove Markdown registration* **before** deleting the EXE

That's everything mdVü ever touches.

---

*mdVü is in beta. The program is provided free of charge and "AS IS"; no warranty is given for freedom from defects or fitness for a particular purpose. See [LICENSE](../LICENSE.md).*
