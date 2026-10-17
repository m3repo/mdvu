# mdVü — Manual

Markdown viewer for Windows · © 2026 Martin Niedergesäß — m3Works · *[Deutsche Version](manual.de.md)*

---

This is the extended manual for readers who want the whole picture, including installation, settings and troubleshooting. A shorter version ships inside the program — press `F1`.

**Contents**

- [Why a Markdown viewer?](#why-a-markdown-viewer)
- [Installation and first start](#installation-and-first-start)
- [Portable use](#portable-use)
- [The window at a glance](#the-window-at-a-glance)
- [Opening files](#opening-files)
- [Folder view and search](#folder-view-and-search)
- [Outline](#outline)
- [Reading with the keyboard](#reading-with-the-keyboard)
- [Path bar, back and forward](#path-bar-back-and-forward)
- [The four views](#the-four-views)
- [Printing and PDF](#printing-and-pdf)
- [Converting an HTML file to Markdown](#converting-an-html-file-to-markdown)
- [Dark mode](#dark-mode)
- [Frontmatter](#frontmatter)
- [Screen readers](#screen-readers)
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

Nothing is installed system-wide, no admin rights are required, and no services or scheduled tasks are created. The program writes to exactly two places outside its own folder — see [Uninstalling](#uninstalling). If you want it to write to none, use the [portable mode](#portable-use).

**If SmartScreen warns you:** published builds are code-signed and timestamped, but Windows also considers *reputation*, which a new build has yet to earn. „More info → Run anyway" starts the program; you can verify the signature beforehand via *Properties → Digital Signatures*.

## Portable use

mdVü can also run without leaving anything in your user profile or the registry — from a USB stick, a synced folder or a tools folder you carry from computer to computer. The portable download (`mdvu-<version>-portable.zip`) contains `mdvu.exe` and an empty `settings.ini`; unpack both into the same folder.

**How it works:** if a file named `settings.ini` lies next to `mdvu.exe`, mdVü runs in portable mode and keeps everything in that folder — `settings.ini` (values), `user.css` and `favorites.yaml`. Any existing `.exe` becomes portable the same way: just create an empty `settings.ini` next to it. Delete the file (or move the EXE away from it) and mdVü uses the normal settings folder again; the two never mix. Settings are not carried over between the modes — copy `user.css` and `favorites.yaml` by hand if you want them in both.

**The folder must be writable.** If it is not (for example below *Program Files*, or a write-protected stick), mdVü says so at startup and runs anyway, but cannot save anything — not even the license acceptance, so you would be asked again on every start.

**License acceptance:** in portable mode it is stored in `settings.ini`, tied to the computer and the Windows user. On a computer or user account where you have not accepted it yet, the license is shown once — a `settings.ini` copied from someone else does not count. Each computer you use keeps its own entry.

**What is not available:** *File → Register as Markdown default* — the association would point to a folder that may move or carry another drive letter next time. *File → Remove Markdown registration* still works, for cleaning up after an earlier installed copy.

*Help → Diagnostics* shows the settings folder as *Settings (portable)*.

## The window at a glance

![mdVü main window |620](img/mdvu-screenshot-main-en.png)

The window has no classic menu bar — the **main menu sits in the title bar** (*File*, *View*, *Help*), next to the toolbar icons.

Below that, the window is split:

- **left, top:** the **folder view** — the current folder as a tree, `.md` files only
- **left, bottom:** the **outline** of the open document — all headings as a tree
- **right, top:** the **path bar** with the location of the current file
- **right, centre:** the **document**
- **bottom:** the status bar with document information and notices, and where the file lives (Obsidian vault, Git repository)

`F6` cycles the keyboard focus between the panes.

## Opening files

There are several ways to open a file:

- **Drag & drop:** drop an `.md` file or a whole **folder** onto the window. A folder opens in the folder view and shows its folder page. If you drop several things at once, a file takes precedence over a folder.
- **Open dialog** with `Ctrl+O`.
- **Start page** (*File → Start page*): the files you opened last and your favorites, one click away. As soon as you have opened a file once, mdVü starts with this page; the welcome page of the first start is in the *Help* menu.
- **Folder view:** clicking a file in the folder tree on the left, or moving through the tree with the arrow keys, shows it right away — just a **peek**: it does not end up in the history (*Back*) or among the recent files, and the path bar shows its name in *italics*. `Enter` or a double-click opens the file for real and moves the focus into the document; clicking into the document or `F6` does the same for a peeked file. `Ctrl+Shift+E` takes you back to the folder view. A **folder** shows up as a page of its own: its subfolders and Markdown files with size, date and the first lines of each file. `Enter` (or clicking into the page) moves into it ready for the keyboard — the arrow keys go from link to link, `Enter` opens a file or subfolder. Opening a file or folder that belongs to an Obsidian vault or a Git repository — from the command line, the file dialog, drag & drop, a link, the path bar or the recent files — shows the **whole vault or repository** in the folder view, with the file or folder selected; if they are nested, the innermost one. As long as you stay inside it, the folder view stays put. Files and folders whose name starts with a dot (`.git`, `.obsidian` …) are not shown (setting `ui/folderTreeHideDot`).
- **Recently used:** the *File* menu lists recently opened files and folders. The **start page** (*File → Start page*) also shows the last five files.
- **Double-click in Explorer:** *File → Register as Markdown default* associates mdVü with `.md` files (per user, no admin rights required). Windows may ask once via "Open with" — see [Troubleshooting](#troubleshooting).
- **Explorer context menu:** the same registration adds *Open with mdVü*, *Print with mdVü* (opens the print preview) and *Export as PDF with mdVü* to every `.md` file — even if another program is the default — and *Open in mdVü* to folders. On Windows 11 they are under *Show more options* (`Shift+F10`). If you registered with an earlier version, register once more to get them.
- **Command line:** `mdvu.exe "C:\Notes\Readme.md"` — see [Command line](#command-line).
- **Several windows:** *File → New window* (`Ctrl+N`) opens the current document in a second window; *Open in new window* in the menu of a file or folder (right-click in the folder view or on the path in the status bar) does the same for that file or folder, and so does `Ctrl`+click or the middle mouse button on a link or in the folder view. Each window has its own folder view, history and search; recent files and favorites are shared. The program ends with the last window.
- **mdVü already running:** a file opened from Explorer or the command line stays in the running program. If it lies in a vault or repository open in one of the windows, or in the folder shown in a folder view, it opens there and the window comes to the front. A file outside any vault or repository goes to the window that already shows such a file, so stray files don't pile up windows. Anything else opens a new window. *Print with* and *Export as PDF with* always run on their own. If a dialog is open in mdVü, the file opens in a separate mdVü instead.

If the displayed file is changed by another program, mdVü reloads it automatically — the scroll position is preserved. `F5` does the same manually. Files that appear in or disappear from the current folder show up in the tree without a manual refresh; this works recursively, for subfolders too.

Very large files are loaded up to a limit of **50 MB** — a banner at the top of the document indicates that only the beginning is shown. See [Limits](#limits).

## Folder view and search

The folder view shows the folder of the current document, filtered to `*.md`. It is not a vault and not a workspace: it's simply the folder you are in, and it follows you as you navigate. Inside an Obsidian vault or a Git repository the tree shows all subfolders; elsewhere it goes two levels deep, so that opening something like `C:\` doesn't scan the whole drive.

**Recently changed.** A coloured dot behind a file shows how long ago it was changed — red within 10 minutes, orange within an hour, yellow within a day, grey within a week. A folder shows the dot of the most recently changed file inside it, even when it is collapsed. The dots update while mdVü is open, also for changes made by other programs, and a file that has just been changed or added lights up briefly. The clock ⏱ in the header of the folder view filters the tree: show only files changed in the last 10 minutes, 30 minutes, hour, day or week. The filter stays on while you search the folder view or open another folder; it is not kept for the next start.

`Ctrl+F` opens the search strip for the main pane — the view currently showing: document, source text, CSS or print preview. `F3` and `Shift+F3` step to the next and previous hit in the main pane, wherever the focus is: in the search field, in the document, even in the folder view or the outline. So you can keep reading and press `F3` to move on.

`Ctrl+F3` searches wherever you are — the pane holding the keyboard focus gets the strip. It is the only way to reach the folder view and the outline, and unlike `Ctrl+F` it also switches the strip off again.

In the **folder view** and the **outline** the strip appears above the tree. As you type, the tree is filtered — to matching files or headings — and hits are highlighted. The arrow-down key moves the focus from the search field into the tree, so you can type, then browse without touching the mouse. When you close the strip, the tree is expanded the way it was before the search.

In the **document, source text, CSS editor and print preview** the strip appears below the path bar and works like a browser's find bar: `Enter` and `Shift+Enter` step through the hits (in the document, a further `Enter` moves into the text instead — see *Reading with the keyboard*), a counter shows *hit / total*, and all hits are highlighted at once. Three toggles refine the search:

| Toggle | Meaning |
|---|---|
| `Aa` | Match case (off by default) |
| `.*` | Read the search term as a regular expression |
| `Sel` | Restrict the search to the current selection (document only; needs a non-empty selection) |

In the **document**, mdVü always searches the whole text — including parts of very large files that haven't been displayed yet; it finds what you see (`foo` also matches `**fo**o`, but not a link address). While you type, mdVü waits until you pause briefly (0.3 seconds) and until you've entered **3 characters**, so typing stays smooth even in large documents. `Enter` and `F3` search right away, shorter terms too. A term in quotes (`"ab"`) searches for exactly that text, even if it is short or has spaces at the edges. With a very large number of hits, the first 10,000 are highlighted; the status bar tells you.

`Ctrl+F3` again, `Esc` or the `X` button closes the strip — highlights disappear, the folder filter is lifted. The search term itself is kept: `Ctrl+F` brings it back into the field, and `F3` resumes the search from the first hit. That also means `F3` can leave highlights in the document without a visible strip; `Esc` in the document clears them.

While a document search is running — the strip is open, or `F3` has left highlights — it **moves along when you open another document**: the term is searched there right away and the hits are highlighted. The view does not jump to the first hit; `Enter` or `F3` takes you there. A search you closed stays closed.

Only one strip is open at a time; switching views closes the main pane's strip (the strips above the trees stay).

Note on the print preview: it searches what has actually been paginated. Documents cut off at the 200-page limit end there for the search as well.

## Search in files

`Ctrl+Shift+F` opens a strip that searches **all Markdown files** of an area at once. Next to the search field you pick the area:

| Area | What it covers |
|---|---|
| Vault | the Obsidian vault of the current document |
| Repository | the Git repository of the current document |
| Folder | the folder shown in the folder view, with all subfolders |
| All favorites | every folder among your favorites at once; the hits are grouped by favorite |

The narrowest area is preselected — inside a vault the vault, inside a repository the repository, otherwise the folder. Selected text or the term of a running document search is filled in. `Enter` starts the search; once the result list for exactly this search is showing, `Enter` moves the focus into the list instead (`F5` searches again). `↓` always ends up in the list — if the term or the options have changed since, it searches first, so you never land in stale results. `Aa` matches case; a term in quotes (`"ab"`) searches for exactly that text. Two more toggles set word boundaries — only one of them can be on:

| Toggle | Meaning |
|---|---|
| `ab…` | Beginning of a word, also after a hyphen or punctuation: `der` finds *derzeit* and *Nord-der*, but not *oder* |
| `\|ab\|` | Whole words only |
| `.*` | Read the term as a regular expression; the word-boundary toggles do not apply then (use `\b` in the pattern). The links of the result list carry it along |

There is no search-as-you-type here: a search across thousands of files only starts when you ask for it.

The result is a **document of its own**, with its own place in the history:

- files whose **name** matches come first, even without a hit in the text;
- then the hits, grouped by folder — each file with its number of hits and up to three lines of context, the hit highlighted;
- clicking a file name opens the file at its first hit, clicking a line number opens it at exactly that hit. The document search is already filled in there, so `F3` walks on through the file. The list opens ready for the keyboard: arrow keys or `Tab` move between the hit links, `Enter` opens one (see *Reading with the keyboard*).

**Back** (`Alt+←`) returns to the result list at the place you left. The list is kept — the last five result lists are held in memory — so it looks exactly as before, even if files have changed since. `F5` on the result list searches again. Because the list is a document, you can search in it (`Ctrl+F`), print it or save it as PDF, and its outline lists the folders and files.

Large folders are searched in the background: the list grows while you read, and the footer shows the progress. Opening another document stops a running search; going back to it then searches again. Files larger than the load limit (`doc/maxLoadMB`) are searched up to that limit, like the display; the list marks them.

mdVü searches **the text you see** — in files exactly as in the document, so both count the same hits: front matter (properties) is included and marked as such in the list, but `%%comments%%`, link targets and Markdown markup are not. Obsidian's own search does find comments. Hidden folders (starting with a dot, like `.obsidian` or `.git`) are skipped, and only `*.md` files are searched.

## Outline

Below the folder view, mdVü shows the **outline** of the current document — all headings as a tree, nested by level. A click jumps to that position in the document; the target flashes briefly so your eye finds it right away. Like the folder view, a click or the arrow keys only peek; `Enter` or a double-click makes the jump part of the history, so *Back* returns to that chapter.

For a long document, the outline is the fastest way around: no scrolling, no searching, one click. With very many headings, press `Ctrl+F3` with the focus in the outline: the strip filters it to the headings containing the search text — together with their parent headings, so you can see where they are.

## Reading with the keyboard

mdVü is a reader, so the document doesn't need a text cursor all the time — the keys are free for moving through it in **units**, much like a browser lets you tab through links. The footer always shows the active unit:

| Key | Unit | Footer | Arrow keys |
|---|---|---|---|
| `0` | Scroll | `SCROLL` | scroll like in a browser, as do `Page Up`/`Page Down` and `Home`/`End` (default) |
| `1` | Caret | `CARET` | move a text cursor by character and line, as after a click into the text |
| `L` | Links | `LINK 3/41` | `←`/`→` previous/next link in reading order, `↑`/`↓` nearest link in the line above/below |
| `H` | Hits | `HIT 2/17` | walk through the hits of the document search (`Ctrl+F`) |

A click on the unit in the footer opens a menu with all units.

`F7` switches between scrolling and the caret (as *caret browsing* does in browsers). `Tab` and `Shift+Tab` always go to the next/previous link, whatever unit is active, and `Enter` follows the active link — or the link at the caret. The first link is the first one **on screen**, not the first one in the document; the active link is highlighted (CSS: `highlight.nav`). `↑`/`↓` really move vertically: they skip the other links of the same line and go to the closest link in the next line above or below that has one.

The way in from the search: in the document search strip, the first `Enter` searches, every further `Enter` — and `↓` at any time — puts the focus into the document with the unit *Hits*, so `←`/`→` continue through the hits. The result list of *Search in files* opens with the unit *Links*: as soon as you move into it, the first link on screen is highlighted and `Enter` opens it. The highlight stays on its target while a large search is still adding results.

A click into the text switches to the caret. `Esc` steps back the way you came: from links or hits into the field of the open search strip (document search or search in files) — a second `Esc` there closes the strip and returns you to the document in scroll mode — and without a strip straight to scrolling. The unit belongs to the place in the history: **Back** brings it back, including the active link. Following a link in the unit *Links* keeps you in it — the next document starts at its first link on screen. A link that carries a search (like the hits of *Search in files*) opens with that search instead. Keys `2` to `5` are reserved for words, sentences, paragraphs and headings. Links work in very large documents too, also in parts that haven't been displayed yet.

## Favorites

Folders you return to often — your vaults, your repositories — can be kept as **favorites**. `Ctrl+D` adds the folder shown in the folder view, or removes it again; the **star** in the toolbar is filled when the current folder is a favorite. Clicking the star (or `Ctrl+Shift+D`) opens the list: arrow keys and `Enter` open a favorite, `Del` removes the selected one. The favorites also appear in the **File** menu, and the menu of a file or folder (right-click in the folder view) adds or removes them. Search in files can search **all favorites** at once. mdVü keeps them in `favorites.yaml` next to its other settings.

## Path bar, back and forward

Above the document, the **path bar** shows the location of the current file. Every segment is clickable: clicking a folder opens it in the folder view and shows its folder page.

**The file's own menu.** Clicking the file path in the status bar opens a menu for that file: copy the path, show it in Explorer, open it in Obsidian (inside a vault) or with another program installed for `.md` files. Right-clicking a file or folder in the folder view, or the **Obs**/**Git** badge in the status bar, opens the same menu — in the folder view also by keyboard with `Shift+F10` or the context-menu key.

mdVü navigates its history like a browser: the arrow icons in the toolbar or `Alt+←` / `Alt+→` step back and forward. **Right-clicking the arrows** opens the history list, so you can jump straight to any earlier document instead of stepping through them.

**Back takes you to where you were** — not to the top of the document. mdVü remembers the topmost visible line of text rather than a pixel position, so this still fits when the window width or zoom has changed in the meantime or the document is loaded in pieces. If the file has become shorter, you land at its end. A running search in the document comes back too: search term, options, active hit and the strip. If you closed the search with `Esc` before moving on, it won't come back either.

Links inside documents work as you'd expect: a relative link to another `.md` file opens that file; a link to a heading (`#section`) jumps within the document; an `http(s)` link opens in your browser after a confirmation. Links that lead nowhere sensible are refused rather than followed. A link of the form `mdvu:open?uri=…&find=…` or `&mark=…` opens a document and highlights matches or lines in it — see [Linking to places](markdown-support.md#linking-to-places).

**Jumps within a document are part of the history.** Following a link to a heading in the same document adds an entry, so *Back* returns you to the place the link was — with the link you came from highlighted for a moment, so your eye finds it again. The same happens when you come back from another document. The history list (right-click on the arrows) shows the heading of such an entry after the file name.

**Where a link leads.** Links that leave mdVü — web addresses and e-mail links — have their own color, so you can tell them from links within your documents before you click; mdVü still asks before it opens the browser. While the mouse is on a link, the status bar shows its target instead of the file name; in the link unit (`L`) it shows the target of the active link. The color can be changed with `a.external` in your [CSS](css-customizing.md).

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
- **Page setup:** a strip at the top of the print preview selects the printer, the paper size (A3, A4, A5, A6, Letter, Legal) and portrait or landscape. The preview is laid out anew right away, and print and PDF use exactly this format — what you see in the preview is what comes out of the printer. *Printer setup…* opens the Windows printer settings without printing; printer, paper size and orientation chosen there are taken over. Show or hide the strip with `Ctrl+Shift+P` (*View → Page setup*), close it with `Esc`. The choice is remembered. In a narrow window the printer list gets narrower first; then *Printer setup…*, *PDF…* and *Print…* move into a menu behind **»**. Paper sizes outside the list above are not supported yet; if the printer dialog returns one, mdVü keeps the size set in the strip.
- **Native PDF:** *View → Export as PDF* produces a true vector PDF with selectable text and a PDF outline built from the document's headings. The files are usually smaller than "Print to PDF" via a printer driver.
- **Clean page breaks:** orphaned lines are taken into account — a single line of a paragraph is never left alone at the top or bottom of a page.
- **Wide tables** are fitted automatically: the font shrinks moderately (down to 70 %), anything still wider is cut off at the right page edge — so put the important columns first. Long-text columns are capped at 30 % of the page width when space is tight. The previous behaviour (squeeze all columns onto the page) is available via the setting `print/tableFit = squeeze`.
- **Print** straight from the view with `Ctrl+P`. The print dialog starts with the printer and paper from the page setup, and changes made there flow back into the preview.

Print and PDF output is always light, regardless of the dark mode setting — a dark page background would waste toner and read badly on paper. Preview, print and PDF are limited to the first **200 pages**; a red message appears in the status bar when a document is cut off.

**Messages.** Messages appear in the status bar in place of the file name: red ones matter (something is missing from the output or has failed) and stay a little longer, orange ones are hints, blue ones just confirm a key press. A small flag at the right end of the status bar opens the list of earlier messages — all red ones and the last few orange ones; it turns red while there is a red message you have not looked at yet.

## Line breaks, Obsidian and Git

By default, mdVü follows the Markdown standard (CommonMark): a single line break inside a paragraph becomes a space. A line only breaks where it ends with two spaces or a backslash `\`. Apps like Typora and Obsidian break at every line instead.

If a file lies in an **Obsidian vault** (a folder containing `.obsidian`), mdVü uses the vault's setting *Strict line breaks*, so the note looks the way it does in Obsidian. For all other files, `doc/lineBreaks = newline` in `settings.ini` switches to one line, one break.

The status bar shows where a file lives: **Obs** for an Obsidian vault, **Git** for a Git repository, **Obs/Git** if both share the same folder. A click opens that folder in the folder view.

**Wikilinks** such as `[[Note]]` and embeds such as `![[picture.png]]` are resolved inside a vault the way Obsidian does it: by name, anywhere in the vault. `[[Note#Heading]]` opens the note and jumps to the heading — so does a Markdown link like `[details](note.md#installation)`. A link to a picture or a PDF, such as `[[photo.jpg]]`, opens the file in its default application after a confirmation; it does not become part of the back/forward history. See [Markdown support](markdown-support.md#wikilinks) for the details.

## Converting an HTML file to Markdown

> [!WARNING]
> The converter is a preview. The menu command, the `/convert` switch and the format of `mdvu-converter.yaml` may change before the final version, or the converter may be removed again. Do not build on it for anything that has to last.

*Tools → Convert HTML file to Markdown* turns a web page you have saved on your computer into a Markdown file. Choose the HTML file, then where to save the result — mdVü suggests the same folder, so that relative images and links of the page keep working — and the new file opens right away. mdVü reads only the file you picked: nothing is downloaded, images and links stay as references. Scripts, styles and comments are left out. Pages that build their content with scripts convert poorly — save them from the browser as "web page, HTML only" after they have loaded.

**Links within the page** keep working as far as Markdown allows. Markdown can only jump to headings, so a link to a definition or a paragraph leads to the heading of the section that contains it; a link whose target lies before the first heading becomes plain text.

**Settings for a page.** Web pages mark notes, warnings and code languages in their own ways — HTML has no standard for them. To carry such details over, put a file named `mdvu-converter.yaml` next to the HTML file:

```yaml
callouts:            # element.class → callout type
  p.note: note
  p.warning: warning
  div.example: example
languages:           # class on <pre>/<code> → language of the code block
  js: javascript
  idl: webidl
skip:                # leave these elements out entirely
  - div.advert
links:               # address of another page → its HTML file in this folder
  - url: https://example.org/other/
    file: other.html
```

- A **selector** is `element.class`, or just the class name for any element; class names are case-sensitive.
- **Callouts** work for block elements such as `p` and `div`, not inside tables. The types are the ones mdVü knows from Obsidian (`note`, `warning`, `example`, `tip`, `danger` …).
- **Languages** are looked up on `<pre>` and the `<code>` inside it; the usual `language-…` classes are recognized without an entry.
- With **links**, a link to another page you have also saved points to its Markdown version afterwards (`other.md`), including the heading its anchor belongs to. mdVü reads the other HTML file for that, so the order in which you convert the pages does not matter — but convert all of them with the same settings file. A link matches when its address starts with `url`. If the file is missing, the link stays as it is.
- **skip** also removes elements inside a line of text, such as `a.logo` or `img.icon`.

**Relative links and images.** If the address of the page is known, relative targets of links and images are resolved against it: `/images/a.svg` becomes `https://example.org/images/a.svg`, so they still lead somewhere from the Markdown file. The address comes from `base:` or, without it, from the `links` entry whose `file` is the page being converted — a settings file that lists the page itself under `links` therefore turns its relative links into absolute ones. Links within the page (`#section`) and targets such as `mailto:` stay as they are; a link to the page itself without an anchor keeps the address of the original.

**Header and note.** Three more sections add a header and a note to every converted page:

```yaml
base: https://example.org/doc/      # address of the page, if "links" does not name it
vars:                               # your own values, for all pages
  publisher: Example Org
frontmatter:                        # YAML header of the Markdown file
  title: "{{ title }}"
  source: "{{ url }}"
  tags: [reference, example]
banner:                             # a note at the top of the page
  callout: info                     # optional; without it a plain paragraph
  title: Unofficial copy            # optional title line of the callout
  position: after-title             # after-title (default) or top
  text: |
    Converted from [{{ title }}]({{ url }}) on {{ date }}.
```

- **frontmatter** becomes the YAML header of the Markdown file, with your keys in your order. Values are texts or lists of texts; mdVü adds quotation marks where YAML needs them.
- The **banner** `text` is Markdown and may have several paragraphs, but no headings. `after-title` puts it right after the first level-1 heading, or at the top if the page has none; `title` only counts together with `callout`.
- **Placeholders** work in `frontmatter` values and in the banner: `{{ title }}` (the `<title>` of the page, otherwise its first heading), `{{ url }}` (address of the page, empty if unknown), `{{ file }}` (name of the HTML file), `{{ date }}` (day of the conversion) and `{{ retrieved }}` (day the HTML file was last changed, both as `YYYY-MM-DD`), plus every name from `vars`. A name that does not exist stops the conversion with a message.
- A `links` entry can carry its own `vars:` for values that differ from page to page, such as the version a page was saved at.
- Filters and conditions work too, for example `{{ snapshot[:7] }}` or `{% if url %}…{% endif %}`. In the settings file, put a value that starts with `{{` in quotation marks.

If the settings file contains a mistake, the conversion stops with a message instead of silently ignoring it.

The same conversion is available from the [command line](#command-line), for scripts that rebuild a set of pages.

## Dark mode

*View → Dark Mode* switches the whole UI including the document. The setting is remembered.

Dark mode in the document is entirely CSS-driven: the built-in dark stylesheet is layered on top of the light one. This matters when you write your own CSS — see [Customizing with CSS](css-customizing.md), which explains why a colour you set only for dark mode can "stick" when you switch back.

## Frontmatter

*View → Show Frontmatter* shows or hides the YAML header at the top of a file; the setting is remembered. When it is hidden, a single line — `--- frontmatter (5 lines) ---` — stays in its place, so you can see that the file has one; a click on that line shows it again. While you step through search hits (unit `HIT`), the frontmatter is always shown in full, so a hit inside it is never invisible. Print, preview and PDF leave a hidden frontmatter out completely.

## Screen readers

mdVü draws the document itself, and screen readers (NVDA, JAWS, Narrator) cannot read that view yet. Until they can, `Ctrl+Shift+B` (*View → Read in browser*) opens the current document as a web page in your default browser — with headings, lists, tables and links that every screen reader handles well. The page is written to a temporary folder; nothing leaves your computer. The folder view and the outline already work with screen readers: they announce the name of the selected file or heading.

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

In [portable mode](#portable-use) it is the program folder instead. It contains `settings.ini` (values), `user.css` (your stylesheet) and `favorites.yaml` (your favorites). Values are written through immediately — mdVü never loses a setting on a crash, but it also means **you should close the program before editing `settings.ini` by hand**, otherwise your changes will be overwritten.

Keys are hierarchical: everything before the slash is the INI section, everything after is the key name. `doc/maxLoadMB = 80` therefore looks like this in the file:

```ini
[doc]
maxLoadMB=80
```

The values worth knowing about:

| Key | Meaning |
|---|---|
| `doc/maxLoadMB` | load limit for a single document in MB (default 50) |
| `doc/showFrontmatter` | show the YAML header in full (`true`, default) or collapse it to one line — written by *View → Show Frontmatter* |
| `doc/zoom` | document zoom in percent (default 100); the closest step applies — written when you zoom |
| `doc/lineBreaks` | line breaks outside an Obsidian vault: `standard` (default, Markdown standard) or `newline` (every line break breaks, as in Typora). Inside a vault, the vault's own setting applies. Takes effect on the next start |
| `doc/tableImageMaxWidth` | maximum width of an image in a table cell, in pixels (default 400); `0` shows images at their natural size. Applies only to images without a width of their own (`![[image.png\|300]]`). Takes effect on the next start |
| `perf/textCacheMinMB`, `perf/textCacheMaxMB` | memory for the text cache in MB (defaults 8 and 16): up to the lower value nothing is discarded, the upper value is a fixed limit (`0` = no limit). A larger cache keeps pages you return to fast. Takes effect on the next start |
| `perf/textCacheIdleMinutes` | after this many minutes without navigation the text cache shrinks one step, at most to halfway between the two values, so a window left open gives memory back (default 5, `0` = off) |
| `perf/imageCacheMB` | memory for decoded images in MB (default 64, at least 8). Images are kept at the size they are shown, so scrolling and returning to a page do not decode them again. Takes effect on the next start |
| `perf/imageWicDecoder` | decode PNG and JPEG with the Windows image decoder, which is considerably faster (default `true`); `false` uses the previous built-in decoders — a way out if an image looks wrong |
| `open/inOpenVault`, `open/inShownFolder`, `open/loose`, `open/other` | what happens when mdVü is already running and a file or folder is opened from outside — one key per case: it lies in a vault or repository open in the window; it lies in the folder shown in the folder view; it lies in no vault or repository; it lies in a vault or repository that is not open. Values: `match` (into the window the case refers to), `reuse` (into the most recently used window), `loose` (into the window that shows a file outside any vault or repository, otherwise a new one), `window` (a new window), `instance` (a separate mdVü). Defaults: `match`, `match`, `loose`, `window` |
| `print/paper` | paper size: `A3`, `A4` (default), `A5`, `A6`, `Letter`, `Legal` — written by the page setup strip |
| `print/orientation` | `portrait` (default) or `landscape` |
| `print/printer` | printer name; empty means the Windows default printer |
| `print/tableFit` | how wide tables are fitted: `shrink` (default) or `squeeze` |
| `print/tableMaxColPct` | maximum width of a long-text column in percent of the page (default 30) |
| `print/tableMinFontPct` | how far the font may shrink when fitting, in percent (default 70) |
| `ui/theme`, `ui/mode` | named stylesheet and light/dark/system — written by the Dark Mode command |
| `ui/currentFolder` | folder restored on the next start |
| `ui/folderTreeHideDot` | hide files and folders whose name starts with a dot (`.git`, `.obsidian`, `.trash` …) in the folder view; mdVü then doesn't look inside them either, which keeps large vaults and repositories fast. `true` (default) or `false`. Takes effect on the next start |
| `ui/footerWindowSize` | show the window size (`w: … h: …`) as the first item of the status bar — a help for screenshots and testing. `false` (default) or `true`. Takes effect on the next start |
| `ui/windowSize` | window size from last time as `width,height,maximized` (at 100 % scaling); the position is left to Windows. Next to it mdVü keeps one entry per screen size, such as `ui/windowSize.2560x1440`, so each of your screens gets its own size back |
| `ui/startPage` | page shown at start, as a link such as `mdvu:open?uri=m3-mdvu:start.md&nav=links` — any file or page works, e.g. `mdvu:open?uri=C:/Notes/Index.md`. Empty means the welcome page; after the first session in which you opened a file, mdVü fills in the start page once and never touches the value again. A file passed on the command line (double-click in Explorer) always wins |
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
| Search in files | 500 files | the result list stops there, with a note to narrow the search |
| Folder view depth | 2 levels below the opened folder | deeper folders are not shown; no limit inside an Obsidian vault or a Git repository |

## Keyboard shortcuts

| Key | Function |
|---|---|
| `Ctrl+O` | Open file |
| `Ctrl+N` | New window with the current document |
| `F1` | Manual |
| `Ctrl+F` | Search in the main pane |
| `F3` / `Shift+F3` | Next / previous hit in the main pane |
| `Ctrl+F3` | Search in the focused pane on/off (incl. folder view and outline) |
| `Ctrl+Shift+F` | Search in files (vault, repository or folder) |
| `Esc` | Close the search strip / clear the highlights / back to scrolling |
| `0` / `1` / `F7` | Document: scroll / caret / switch between them |
| `L` / `H` | Document: walk through links / search hits with the arrow keys |
| `Tab` / `Shift+Tab` | Document: next / previous link |
| `Enter` | Document: follow the active link |
| `Ctrl+C` | Document: copy the selection — as text, and with formatting for Word, Outlook & Co. Images go along as links to the original files (in their original format); Word embeds them when pasting |
| `Ctrl+Shift+C` | Document: copy the selection as Markdown |
| Right mouse button | Document: menu with Copy, Copy as Markdown, Back and Forward |
| `Ctrl+mouse wheel` | Document: zoom (50–200 %). A click on the zoom value in the footer offers all steps; the zoom is kept for the next start |
| `F5` | Reload document / search again on the result list |
| `F6` | Switch between panes (tree / document / editor) |
| `Ctrl+Shift+E` | Go to the folder view |
| `Alt+←` / `Alt+→` | Back / forward (also `AltGr+←` / `AltGr+→`, one-handed next to the arrow keys) |
| Mouse side buttons | Back / forward |
| `F10` / `Alt` | Menu bar by keyboard: `←`/`→` choose a menu, `Enter` opens it, `↑`/`↓` + `Enter` run an entry, a letter jumps to it, `Esc` steps back. `Alt`+initial letter opens a menu directly |
| `Ctrl+D` | Add/remove the current folder as favorite |
| `Ctrl+Shift+D` | Show favorites |
| `Ctrl+1` | Markdown view |
| `Ctrl+2` | Source view |
| `Ctrl+3` / `Ctrl+F2` | Print preview |
| `Ctrl+4` | Edit CSS |
| `Ctrl+P` | Print |
| `Ctrl+Shift+P` | Page setup strip in the print preview on/off |
| `Ctrl+Shift+B` | Read the document in the browser (for screen readers) |

## Command line

```
mdvu.exe "C:\Notes\Readme.md"     open a file
mdvu.exe "C:\Notes"               open a folder
mdvu.exe -accepteula              accept the license non-interactively
mdvu.exe /convert page.html       convert an HTML file to Markdown, no window
```

The first parameter may be a file or a folder; a file is opened, a folder shown in the folder view. This is also the mechanism behind the Explorer file association.

If mdVü is already running, a file or folder may go to the open window instead — see *mdVü already running* under [Opening files](#opening-files) and the `open/…` settings. `/print` and `/pdf` always run in a process of their own, so a script can wait for them.

`/convert` writes the Markdown file next to the HTML file (`page.md`), or to the path given as a second parameter, and then ends without opening a window: exit code 0 means converted, 1 the conversion failed, 2 the call was incomplete or the file is missing. A `mdvu-converter.yaml` next to the HTML file applies as in the menu command — see [Converting an HTML file to Markdown](#converting-an-html-file-to-markdown). The converter is a preview; the switch may change or be removed. mdVü is a window program, so a script should wait for it explicitly, for example `Start-Process mdvu.exe -ArgumentList '/convert','page.html' -Wait -PassThru` in PowerShell.

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
mdVü writes `mdvu.crash.log` next to the executable. If that folder is read-only (for example below *Program Files*), the file goes to `%LOCALAPPDATA%` instead — type that into the Explorer address bar to get there. The file contains the error location and a stack dump, no document content. Nothing is sent anywhere — mailing it in is entirely your decision, and it makes fixing the bug much more likely.

### Performance page

*Help → Performance* shows what mdVü measured in the current session: how long pages took to load and to appear (last page, average of the last ten, whole session), how much of that went into images, how long scanning an Obsidian vault took, and for each of the last ten pages its size, images, chunks and layout elements. Below that are the caches and the memory in use. `F5` refreshes the values. The page is handy to attach when you report that something feels slow.

### Diagnostics page

*Help → Diagnostics* lists the history of the current session — every place you can go back to, with the reading position stored for it — and the folders mdVü uses (settings, folder view, temporary files). The entries are links. `F5` refreshes the page. Like the performance page, it is meant for looking into a problem or attaching to a report.

## Uninstalling

Delete `mdvu.exe`. Optionally also:

- the settings folder `%APPDATA%\m3Works\mdVu` (settings and your `user.css`)
- the registry key `HKCU\Software\m3Works\mdVu` (the license acknowledgement)
- the file association, via *File → Remove Markdown registration* **before** deleting the EXE

That's everything mdVü ever touches. In [portable mode](#portable-use), deleting the program folder is all there is to it — unless you removed a registration from an earlier installed copy, nothing was written elsewhere.

---

*mdVü is in beta. The program is provided free of charge and "AS IS"; no warranty is given for freedom from defects or fitness for a particular purpose. See [LICENSE](../LICENSE.md).*
