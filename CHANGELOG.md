# Changelog

*[Deutsche Version](CHANGELOG.de.md)*

All notable changes to mdVü are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions are `Major.Minor.Patch`, and the fourth number in the file version of the EXE is the build counter.

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
