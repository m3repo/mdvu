![mdVü|860](docs/img/welcome-banner.svg)

# mdVü — a Markdown viewer for Windows

*[Deutsche Version](README.de.md)*

**Reading is not writing.** If you just want to look up a note, skim a document or simply *view* an `.md` file someone sent you, you don't need an editor with plugins, vaults and sync — you need a program that starts instantly, shows the file and gets out of your way.

That's what mdVü is built for.

![mdVü main window (stylized)|620](docs/img/mdvu-window.svg)

*The illustration is a stylized rendering of the window layout — real screenshots will follow with the first public release.*

## What makes it different

- **Lean** — a single EXE under 15 MB. No installer, no framework, no runtime, no browser engine. Copy it anywhere and run it.
- **Fast** — a native Windows application with its own layout engine. Large documents open without a noticeable wait; a 100-page print preview is ready in seconds.
- **Light on memory** — a fraction of the RAM that Chromium-based editors need, because there is no Chromium.
- **Offline and quiet** — mdVü does not import a single networking DLL. No telemetry, no update pings, no accounts. Every release is [verified against a baseline of its own imports](#privacy-and-security) before it is signed.
- **Real print and PDF output** — a true vector PDF with selectable text, produced directly, without a detour through a browser or a PDF printer driver.
- **A companion, not a replacement** — Obsidian, Typora and VS Code stay in charge of writing. mdVü is the tool for the quick look: double-click in Explorer, read, done.

## Features at a glance

| | |
|---|---|
| **Formats** | GitHub-flavoured Markdown, plus Obsidian callouts, wikilinks and image embeds — see [Markdown support](docs/markdown-support.md) |
| **Folder view** | Tree of the current folder with live refresh, incremental search (`Ctrl+F3`) and arrow-key browsing |
| **Outline** | All headings of the document as a tree; clicking jumps to the spot and flashes the target |
| **Navigation** | Browser-style back/forward with history list, clickable path bar, working links between documents |
| **Print & PDF** | Print preview, native PDF export, automatic fitting of wide tables, orphan-aware page breaks |
| **Dark mode** | Whole UI and document; print, preview and PDF stay light on purpose |
| **Your own look** | A `user.css` layered over the built-in stylesheet — see [Customizing with CSS](docs/css-customizing.md) |
| **Windows integration** | Drag & drop, command line, per-user `.md` file association (no admin rights) |
| **Auto-reload** | The open file reloads by itself when another program changes it — scroll position preserved |

## Documentation

| Document | What's in it |
|---|---|
| [Manual](docs/manual.md) | The full manual: opening files, folder view, outline, printing, PDF, dark mode, keyboard shortcuts, settings |
| [Markdown support](docs/markdown-support.md) | Exactly which syntax is rendered — and what deliberately isn't |
| [Customizing with CSS](docs/css-customizing.md) | The supported CSS subset, the pitfalls, and worked examples for `user.css` |
| [Sample files](samples/) | Markdown files to try things out with, including a syntax-highlighting showcase |
| [Changelog](CHANGELOG.md) | What changed between versions |

The manual also ships inside the program: press `F1`.

## Requirements

- Windows 10 or 11 (64-bit Windows, 32-bit application)
- No .NET, no Visual C++ redistributable, no WebView2 — the EXE is self-contained
- Roughly 15 MB of disk space

Settings live in `%APPDATA%\m3Works\mdVu` and the one-time license acknowledgement in `HKCU\Software\m3Works\mdVu`. Nothing else is written outside the program folder; removing those two removes every trace.

## Download

Releases are published on the [Releases page](https://github.com/m3repo/mdvu/releases/latest): a single code-signed `mdvu.exe`, no installer and no setup. Download it, put it wherever you like, run it. Every release lists the SHA-256 of the file and a link to its VirusTotal report, so you can check that what you downloaded is what was published here.

The first public beta is still being finalised — until it appears there, this repository carries the documentation and the sample files only.

## Beta notice

mdVü is a **preview version**. It has been through a lot of internal testing, but features may change and malfunctions cannot be ruled out. The program is provided free of charge and "AS IS" — see [LICENSE](LICENSE.md).

Feedback is genuinely welcome, especially now: what feels wrong, what is missing, what breaks. Please [open an issue](https://github.com/m3repo/mdvu/issues) for anything reproducible — that way other testers see it too. For crash logs (`mdvu.exe.crash.log`, written next to the EXE) or anything you'd rather not post publicly, mail to `mdView@outlook.de` (the address predates the rename and still works).

## Privacy and security

- **No network access.** mdVü contains no HTTP, socket or update code. Its PE import table is checked against a versioned baseline before every release, in both the static and the delay-load table, and the binary is additionally searched for networking DLL names and COM identifiers as plain text — so a library sneaking in through a `LoadLibrary` detour would be caught too.
- **No telemetry, no accounts, no cloud.** Documents you open never leave your machine.
- **Signed releases.** Every published EXE is code-signed and timestamped. Windows SmartScreen may still warn on a freshly published build until the signature has built up reputation — that is a matter of download count, not of the signature being invalid.
- **Crash reports stay with you.** On an access violation mdVü writes a text file next to the EXE. Nothing is sent anywhere; you decide whether to mail it.

## AI assistance

mdVü is a one-person project, and AI tools are part of the everyday toolchain — they help with parts of the source code, with text, and with some of the graphics. Nothing ships unread: the design decisions are mine, and everything in the program and in this documentation is reviewed and maintained by hand.

## Licensing

Three different things live under one roof here:

| What | License |
|---|---|
| The program (`mdvu.exe`) | Free of charge, proprietary — [LICENSE](LICENSE.md) (includes third-party component notices) |
| Documentation in this repository (`README*`, `docs/`) | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |
| Sample files (`samples/`) | [MIT](https://opensource.org/licenses/MIT) — copy them into your own projects freely |

The source code of mdVü is not published.

---

© 2026 Martin Niedergesäß — m3Works
