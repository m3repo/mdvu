# Änderungsverlauf

*[English version](CHANGELOG.md)*

Hier stehen alle nennenswerten Änderungen an mdVü. Das Format folgt [Keep a Changelog](https://keepachangelog.com/de/1.1.0/); Versionen sind `Major.Minor.Patch`, die vierte Stelle in der Dateiversion der EXE ist der Build-Zähler.

## [1.0.1] — 2026-10-28

### Neu

- **Dokumentation und Beispiele kommen mit dem Installer:** wenn Sie es nicht abwählen, legt das Setup diese Dokumentation und die Beispieldateien in den Unterordner `Documentation` des Programmordners. Der Startmenü-Eintrag *mdVü Dokumentation* öffnet sie in mdVü — so gibt es gleich etwas zum Ausprobieren. Bei jedem Update werden sie erneuert, bei der Deinstallation entfernt. Siehe [Installation](docs/manual.de.md#installation-und-erster-start).

## [1.0.0] — 2026-10-28

Die erste Version nach der Beta.

### Neu

- **Einstellungsseite:** *Hilfe → Settings*, das Zahnrad in der Leiste oder `Strg+,`. Jede Einstellung mit kurzer Erklärung, nach Themen gruppiert, selten gebrauchte unter *Advanced*; Änderungen wirken sofort, `↺` stellt die Vorgabe wieder her. Ein Filterfeld oben lässt nur die passenden Einstellungen stehen (Name, Erklärung, Schlüssel und die Wahlmöglichkeiten einer Liste). Mit der Tastatur führt `↓` in die Liste, die Pfeiltasten gehen von Einstellung zu Einstellung, `Enter` oder `Tab` in ihre Bedienelemente und `Enter`/`Esc` zurück; die Statuszeile zeigt, wo man steht (`FILTER`, `SETTING 3/27`, `EDIT`). Im Filter leert `Esc` zuerst den Text und schließt danach die Seite. Siehe [Einstellungen](docs/manual.de.md#einstellungen).
- **Installer:** `mdvu-1.0.0-setup.exe` installiert nur für den eigenen Windows-Benutzer, ohne Admin-Rechte, mit Startmenü-Eintrag und auf Wunsch der `.md`-Verknüpfung; Deinstallieren unter *Einstellungen → Apps* entfernt die Verknüpfung wieder. Die einzelne `mdvu.exe` und das portable ZIP gibt es weiterhin. `mdvu.exe /register` und `/unregister` erledigen die Dateiverknüpfung über die Kommandozeile. Siehe [Installation](docs/manual.de.md#installation-und-erster-start).
- **Kopier-Knopf an Codeblöcken:** Mit der Maus über einen Codeblock, und ein Knopf in seiner Ecke kopiert den Code.
- **TOML-Frontmatter** (`+++` … `+++`, wie bei Hugo und Zola) wird wie YAML-Frontmatter erkannt — gezeigt, eingeklappt oder ausgeblendet, und in der Ordnervorschau ausgelassen.
- **Suchtreffer in der Druckvorschau:** `↓` oder ein weiteres `Enter` im Suchfeld, und die Pfeiltasten gehen durch die Treffer; die Statuszeile zeigt `HIT 3/12`.
- **Namen statt Adressen:** Pfadleiste und Verlaufsmenü zeigen Seiten wie *Settings*, *Manual* oder *Search in files* mit Namen.
- **Tooltips in den Farben des Themes**, im Dunkelmodus dunkel.
- **Sprachausgabe:** Die Knöpfe der Suchleiste lassen sich vorlesen (UI Automation).

### Geändert

- **Einstellungen liegen jetzt in `settings.yaml` und `state.yaml`** statt in der `settings.ini` — mit einer kurzen Beschreibung über jedem Wert, nur Werte, die von der Vorgabe abweichen, und Änderungen von Hand bleiben auch bei laufendem mdVü erhalten. Änderungen wirken sofort, in allen Fenstern. Eine vorhandene `settings.ini` wird beim ersten Start übernommen und in `settings.ini.bak` umbenannt. **Die Schlüssel heißen neu**, gruppiert wie auf der Einstellungsseite: aus `doc/…` wird `document/…`, aus `perf/…` wird `performance/…`, aus `ui/theme` und `ui/mode` werden `appearance/theme` und `appearance/mode`, aus `ui/startPage` wird `start/page`; die ganze Liste steht im [Handbuch](docs/manual.de.md#einstellungen).
- **Alle Leisten zeichnet mdVü selbst** — Suche, Suchen in Dateien, Schnell öffnen, Seiteneinrichtung. Kein Flackern mehr beim Ändern der Fenstergröße.
- **Suche ist ein Modus:** `Esc` im Dokument oder auf einem Knopf einer Suchleiste führt zuerst zurück ins Suchfeld; `Esc` im Feld schließt die Leiste.
- **Die Druckleiste gehört zur Vorschau:** Schließen (`×`, `Esc`) beendet die Vorschau, ebenso `Esc` in der Vorschau.
- **Der Fenstertitel** zeigt nur noch den Datei- oder Ordnernamen — das Symbol nennt das Programm schon, und Taskleisten-Vorschau und `Alt+Tab` haben wenig Platz.
- **Die Ladegrenze von 50 MB je Dokument** lässt sich nicht mehr ändern.
- **Keine Beta mehr:** Der Beta-Abschnitt der Lizenz ist entfallen.

### Behoben

- mdVü konnte beim Beenden eine Reihe von Fehlermeldungen zeigen, nachdem Theme oder Dunkelmodus mehrfach umgeschaltet worden waren.
- `Enter` in einem Textfeld der Einstellungen zeigt in der Statuszeile nicht mehr „Unknown URL“.

## [0.21.0] — 2026-10-20

### Neu

- **Schnell öffnen (`Strg+O`)**, wie Obsidians Quick Switcher: unter der Pfadleiste erscheint ein Streifen; tippen Sie einen Teil eines Dateinamens, eines Alias (`aliases` im Frontmatter) oder eines Ordnernamens, und die Treffer erscheinen darunter in einer Liste — die besten zuerst, rechts der Ordner. `↓` wechselt in die Liste, `Enter` öffnet (im Eingabefeld: den ersten Treffer), `Esc` geht einen Schritt zurück. Mehrere Wörter müssen alle passen; passt nichts zum Namen, prüft mdVü die Ordnernamen und zuletzt die Buchstaben der Reihe nach (`mdrd` findet `mdvu-readme`). Bei leerem Feld zeigt die Liste die zuletzt geöffneten Dateien. Ein **Ordner** (📁) öffnet direkt in der Liste — seine Unterordner und Dateien, Tippen sucht darin, `Backspace` geht eine Ebene hoch; mit `quickOpen/folder = open` zeigt er stattdessen die Ordnerseite. Siehe [Datei öffnen](docs/manual.de.md#dateien-öffnen).
- **Taste nochmal = Bereich wechseln:** *Schnell öffnen* und *Suche in Dateien* beginnen beim Ort des aktuellen Dokuments — seinem Vault, sonst seinem Repository, sonst dem Ordner der Ordneransicht. Haben Sie Favoriten, wechselt ein zweites `Strg+O` bzw. `Strg+Umschalt+F` auf **alle Favoriten**, das nächste zurück; der Knopf im Streifen zeigt, wo Sie sind.
- **Suchsprache für die Suche in Dateien:** `rechnung OR mahnung`, `rechnung -entwurf`, `(a OR b) c`, `"offene Posten"`, `/regex/`, `#todo`, `file:readme`, `path:2026`, `content:…`, `line:( … )` und `section:( … )` für Wörter in derselben Zeile bzw. demselben Abschnitt, `modified:>=-7d`, `created:2026-10`, `size:>1mb`, Frontmatter-Eigenschaften in eckigen Klammern (`[status:entwurf]`, `[prio>=2]`, `[kunde.name:müller]`) und `scope:`, um woanders zu suchen (`scope:#tag`, `scope:repo` …). Ohne Wort gibt es eine reine Liste der passenden Dateien. Fehler meldet die Statuszeile. Siehe [Suchsyntax](docs/manual.de.md#suchsyntax).
- **Emoji-Zwischenspeicher auf der Platte:** Farb-Emojis werden einmal gezeichnet und in einer kleinen Cache-Datei gehalten, Dokumente voller Emojis erscheinen ab dem zweiten Start schneller. Einstellung: `perf/emojiDiskCacheMB` (Standard 16, `0` = aus). Die Performance-Seite zeigt die Zeit für Emojis.
- **Emojis in PDFs** lassen sich jetzt im PDF-Betrachter kopieren und suchen (Microsoft Edge macht beim Kopieren noch Platzhalter daraus — ein Edge-Fehler), und Schriften aus Schriftsammlungen (`.ttc`, etwa manche CJK-Schriften) werden korrekt eingebettet.
- **Diagnose-Seite:** die dort genannten Ordner öffnen per Klick im Explorer (nach einer Rückfrage), und der Cache-Ordner steht mit drin.

### Geändert

- **Der Datei-Dialog liegt jetzt auf `Strg+Umschalt+O`**; `Strg+O` ist *Schnell öffnen*.
- **Suche in Dateien** bietet im Streifen zwei Bereiche — den Ort des Dokuments und alle Favoriten — statt einer Liste aller Vaults, Repositorys, Ordner und Tags. Tag-Bereiche und die übrigen erreichen Sie mit `scope:` im Suchtext; Links auf frühere Trefferlisten funktionieren weiter.
- `Strg`+Klick in der Ordneransicht öffnet kein neues Fenster mehr — er bleibt frei für eine spätere Mehrfachauswahl. Die mittlere Maustaste tut es dort weiterhin, ebenso `Strg`+Klick auf einen Link im Dokument.

### Behoben

- Der Bereichs-Knopf eines offenen Suchstreifens folgt jetzt, wenn Sie einen anderen Ordner wählen oder ein Dokument in einem anderen Vault öffnen.

## [0.20.0] — 2026-10-17

0.19 wurde nicht veröffentlicht; ihre Änderungen sind Teil dieser Version.

### Neu

- **Tags:** Dateien und Ordner lassen sich mit eigenen Tags versehen — ohne dass sich eine Datei ändert: mdVü legt sie in `tags.yaml` bei den Einstellungen ab, ein Git-Repository oder ein fremder Vault bleibt also unberührt. Rechtsklick auf eine Datei oder einen Ordner (in der Ordneransicht, auf den Pfad in der Statuszeile oder im geöffneten Dokument), dann **Tags…**. Ein Tag an einem Ordner gilt für alles darunter. Tags aus dem Frontmatter eines Dokuments (`tags:`) zählen ebenso — ein gemeinsamer Satz. Eine Tag-Zeile oben im Dokument zeigt sie, `#3` in der Statuszeile ihre Anzahl, *File → Show tags* listet alle Tags mit ihren Orten, und die *Suche in Dateien* durchsucht alle Orte eines Tags auf einmal oder beschränkt jede Suche mit `tag:name`. Siehe [Tags](docs/manual.de.md#tags).
- **Zoom der Druckvorschau:** solange die Vorschau vorn ist, gilt ihr der Zoom-Eintrag der Statuszeile — *Fit page* (Standard), *Fit width* oder eine feste Stufe; beide Einpassungen folgen der Fenstergröße. Einstellung: `print/previewZoom`.
- **Mehrere Fenster:** *File → New window* (`Strg+N`), *Open in new window* im Menü einer Datei oder eines Ordners, `Strg`+Klick oder mittlere Maustaste auf einen Link oder in der Ordneransicht. Jedes Fenster behält seine eigene Ordneransicht, seinen Verlauf und seine Suche; zuletzt geöffnete Dateien und Favoriten sind gemeinsam, und das Programm endet mit dem letzten Fenster.
- **Dateien landen im laufenden Fenster:** ist mdVü schon offen, erscheint eine aus dem Explorer oder per Kommandozeile geöffnete Datei bzw. ein Ordner in diesem Fenster, wenn sie zum dort gezeigten Vault, Repository oder Ordner gehört — kein zweites Fenster, und die Zwischenspeicher sind schon warm. Dateien außerhalb jedes Vaults oder Repositorys teilen sich ein Fenster, alles andere öffnet ein neues Fenster im selben Programm. Einstellungen: `open/inOpenVault`, `open/inShownFolder`, `open/loose`, `open/other`.
- **Portabler Modus:** eine leere `settings.ini` neben `mdvu.exe` hält Einstellungen, Favoriten, `user.css` und die Lizenz-Bestätigung im Programmordner — nichts landet im Benutzerprofil oder in der Registry. Die Lizenz-Bestätigung ist an Rechner und Windows-Benutzer gebunden; eine kopierte `settings.ini` nimmt sie nicht mit. Als Markdown-Standard registrieren geht in diesem Modus nicht. Releases enthalten eine fertige `mdvu-<version>-portable.zip`. Siehe [Portabel nutzen](docs/manual.de.md#portabel-nutzen).
- **Reguläre Ausdrücke in der Suche:** Der Schalter `.*` der Suchstreifen wirkt jetzt (vorher blieb er ohne Wirkung), und *Find in files* hat ihn ebenfalls.

### Geändert

- **HTML und XML in Codeblöcken** (`html`, `xml`, `svg` …) färbt mdVüs eigener HTML-/XML-Leser; `<script>` und `<style>` innerhalb von HTML werden als JavaScript und CSS gefärbt, SVG innerhalb von HTML als XML.
- **Druckleiste im schmalen Fenster:** zuerst wird die Druckerliste schmaler, dann wandern *Printer setup…*, *PDF…* und *Print…* in ein Menü hinter **»**.
- **Die Fenstergröße steht nicht mehr in der Statuszeile.** Sie war als Hilfe für Screenshots gedacht; die Einstellung `ui/footerWindowSize` blendet sie wieder ein.
- **Temporäre Dateien an einem Ort:** Kopierte Bilder und *Read in browser* benutzen jetzt einen einzigen Ordner `%TEMP%\{mdvu.exe}`; *Hilfe → Diagnostics* zeigt ihn an.

### Behoben

- **Dateien mit Byte-Order-Mark (UTF-8 mit BOM)** zeigten ihr Frontmatter als normalen Text; auch *Find in files* übersah solches Frontmatter. Fehlerhaft seit 0.12.
- Die Links der Startseite auf das Handbuch und auf die Sprachliste wurden mit „Link denied“ abgewiesen.
- Eine von einem anderen Programm gesperrte `settings.ini` (Sync-Werkzeug, Virenscanner) hält mdVü nicht mehr mit einem Fehler an; mdVü versucht es mit der nächsten Änderung und beim Beenden erneut.

## [0.18.0] — 2026-10-12

### Neu

- **HTML nach Markdown (Vorschau):** *Tools → Convert HTML file to Markdown* wandelt eine lokale HTML-Datei in eine Markdown-Datei daneben und öffnet sie; `mdvu.exe /convert <html> [<md>]` tut dasselbe ohne Fenster. Eine Datei `mdvu-converter.yaml` neben der HTML-Datei steuert die Einzelheiten: Callouts und Code-Sprachen nach CSS-Klasse, auszulassende Teile, Links auf andere gewandelte Seiten, einen Frontmatter-Block, ein Banner und die Basisadresse für relative Links. Es wird nichts nachgeladen. Der Wandler ist eine Vorschau — seine Einstellungen können sich noch ändern.
- **Frontmatter ein- und ausblenden:** *Ansicht → Show Frontmatter* klappt den YAML-Kopf am Dateianfang auf eine einzelne Zeile ein, damit erkennbar bleibt, dass es einen gibt; ein Klick auf die Zeile blendet ihn wieder ein. Solange Sie durch Suchtreffer gehen, steht das Frontmatter immer vollständig da. Druck und PDF lassen ein ausgeblendetes Frontmatter weg. Einstellung: `doc/showFrontmatter`.
- **Meldungen mit Verlauf:** Meldungen in der Statuszeile gibt es jetzt in drei Arten — rot für Wichtiges (in der Ausgabe fehlt etwas, oder etwas ist gescheitert), orange für Hinweise, blau für eine bloße Bestätigung. Eine kleine Fahne am rechten Ende der Statuszeile listet die früheren auf.
- **Linkziel in der Statuszeile:** Solange die Maus auf einem Link steht oder ein Link mit der Tastatur gewählt ist, zeigt die Statuszeile, wohin er führt. Links, die mdVü verlassen (Web, E-Mail), haben eine eigene Farbe.
- **Marke an der Leseposition:** Ein schmaler Strich am linken Rand zeigt die Zeile des Carets, des aktuellen Suchtreffers oder des gewählten Links.
- **Diagnose-Seite:** *Hilfe → Diagnostics* listet den Verlauf (Zurück/Vor) mit den gemerkten Lesepositionen und die Ordner, die mdVü benutzt.
- **Die Fenstergröße wird gemerkt** — getrennt je Bildschirmgröße, das Notebook-Display und der große Monitor behalten also jeweils ihre eigene. Die Position bleibt Windows überlassen. Einstellung: `ui/windowSize`.

### Geändert

- **Eine laufende Suche wandert mit:** Wer bei offenem Suchstreifen ein anderes Dokument öffnet, bekommt den Begriff dort sofort gesucht und die Treffer hervorgehoben. `Eingabe` und `F3` suchen neu, statt nichts zu tun, wenn es noch keine Treffer gibt.
- **Links innerhalb eines Dokuments stehen im Verlauf:** Ein Sprung zu `[Abschnitt](#abschnitt)` lässt sich mit *Zurück* rückgängig machen.
- **Die Link-Navigation lässt die Seite stehen:** Eine in der Link-Einheit geöffnete Seite springt nicht mehr zu ihrem ersten Link, wenn der außerhalb des Bildes liegt (`LINK 0/41`); `↑` auf dem obersten Link führt an den Seitenanfang zurück.
- **Wichtige Meldungen sind rot und stehen länger:** „Preview limited to 200 pages“ und „Table wider than page“ waren leicht zu übersehen. Anfang oder Ende des Verlaufs ist jetzt nur noch ein kurzer blauer Hinweis.

### Behoben

- Im Druck konnte der Titel eines Callouts allein am Seitenende stehen bleiben.
- Der Caret nimmt jetzt die Textfarbe des Dokuments statt einer festen Farbe.
- Wo ein Wort an einem Bindestrich über zwei Zeilen umbrach (ein Link wie „Little Snow-white“), blieb ein Teil davon bei Auswahl, Suchmarkierung oder Link-Marke ausgespart.

## [0.17.0] — 2026-10-10

### Neu

- **Bilder in Tabellen:** eine Tabellenzelle, die nur Bilder enthält, zeigt sie jetzt statt des Alternativtexts. Ein Bild ohne eigene Breite wird auf 400 px begrenzt; die Einstellung `doc/tableImageMaxWidth` ändert das (0 = Naturgröße). Eine Zelle mit Bildern und Text zeigt weiterhin den Alternativtext.
- **Performance-Seite:** *Hilfe → Performance* zeigt, was mdVü in der laufenden Sitzung gemessen hat — wie lange die letzten Seiten zum Laden und bis zur Anzeige brauchten, was die Caches halten und wie viel Speicher belegt ist. *Detail level* am Seitenanfang (normal, medium, verbose) schlüsselt jede Seite in ihre Schritte auf; Schritte, die ein Viertel der Zeit oder mehr ausmachen, sind hervorgehoben.
- **Cache-Einstellungen:** der Textcache (`perf/textCacheMinMB`, `perf/textCacheMaxMB`, `perf/textCacheIdleMinutes`) und der Bild-Cache (`perf/imageCacheMB`, `perf/imageWicDecoder`) lassen sich anpassen; die Vorgaben sind 8/16 MB für Text und 64 MB für Bilder.
- **Links auf Bilder und PDFs:** ein Link wie `[[foto.jpg]]` oder `[Scan](vertrag.pdf)` öffnet die Datei jetzt nach einer Rückfrage in ihrer Standardanwendung. In den Verlauf (Zurück/Vor) kommen solche Dateien nicht.

### Geändert

- **Schnelleres Blättern durch Dokumente:** einmal gesetzte Wörter und Emojis bleiben erhalten, statt auf jeder Seite neu berechnet zu werden; Farb-Emojis bleiben für die ganze Sitzung. Der Weg zurück auf eine schon gesehene Seite ist spürbar schneller.
- **Schnellere Bilder, weniger Speicher:** PNG- und JPEG-Dateien dekodiert Windows in der Größe, in der sie gezeigt werden, und zwar beim ersten Zeichnen; sie liegen in dieser Größe in einem Cache.
- **Schnellere Ordnerseite:** die Seite eines Ordners mit einigen hundert Dateien erscheint in deutlich unter einer Zehntelsekunde (gemessen: 280 Dateien in etwa 70 ms statt 170 ms).
- **Schnellere Gliederung:** der Austausch der Gliederung beim Seitenwechsel braucht nur noch einen Bruchteil der Zeit.

### Behoben

- Ein Klick auf einen Link zu einem Bild zeigte die Datei als unlesbaren Text in der Dokumentansicht.

## [0.16.0] — 2026-10-09

### Neu

- **Kontextmenü im Explorer:** *Datei → Als Markdown-Standard registrieren* ergänzt jetzt bei jeder `.md`-Datei *Print with mdVü* (öffnet die Druckvorschau), *Export as PDF with mdVü* und *Open with mdVü* — auch wenn ein anderes Programm wie Obsidian Standard ist — und bei Ordnern *Open in mdVü*; in einem Vault oder Repository öffnet sich das Ganze. Unter Windows 11 stehen die Einträge unter *Weitere Optionen anzeigen*. Schon registriert? Einmal neu registrieren. Siehe [Dateien öffnen](docs/manual.de.md#dateien-öffnen).
- **Screenreader, erste Schritte:** Ordnerbaum und Gliederung funktionieren jetzt mit Screenreadern (geprüft mit der Windows-Sprachausgabe) — sie sagen die gewählte Datei bzw. Überschrift an und ob ein Ordner aufgeklappt ist. Die Dokumentansicht selbst können Screenreader noch nicht lesen; bis dahin öffnet **Read in browser** (`Strg+Umschalt+B`, Menü *Ansicht*) das aktuelle Dokument als Webseite im Standardbrowser, wo jeder Screenreader Überschriften, Listen, Tabellen und Links beherrscht. mdVü vollständig zugänglich zu machen, ist ein erklärtes Ziel — Rückmeldungen von Screenreader-Nutzern sind sehr willkommen. Siehe [Screenreader](docs/manual.de.md#screenreader).

### Geändert

- **Startseite mit Favoriten:** Die Startseite (*Datei → Start page*) zeigt jetzt neben den zuletzt geöffneten Dateien auch Ihre Favoriten. Sobald Sie einmal eine Datei geöffnet haben, startet mdVü mit der Startseite statt mit der Willkommensseite; diese bleibt über *Hilfe → Welcome page* erreichbar. Die Startseite bekommt den Tastaturfokus mit eingeschalteter Link-Navigation, Pfeiltasten und `Eingabe` wirken also sofort. Mit welcher Seite mdVü startet, lässt sich in der `settings.ini` einstellen (`ui/startPage`) — siehe [Einstellungen](docs/manual.de.md#einstellungen).
- **Der ganze Vault bzw. das ganze Repository in der Ordneransicht:** Wer eine Datei oder einen Ordner öffnet, die zu einem Obsidian-Vault oder Git-Repository gehören — per Kommandozeile, Dateidialog, Drag & Drop, Link oder aus den zuletzt benutzten Dateien —, sieht in der Ordneransicht jetzt den ganzen Vault bzw. das ganze Repository mit markierter Datei bzw. markiertem Ordner statt nur deren eigenen Ordner. Wer sich darin bewegt, behält die Ordneransicht. Ein Klick auf einen Ordner in der Pfadleiste oder ein auf das Fenster gezogener Ordner zeigt zusätzlich dessen Ordnerseite. Siehe [Dateien öffnen](docs/manual.de.md#dateien-öffnen).
- **Schnellere Ordneransicht in großen Vaults:** Der Wechsel in einen großen Vault oder ein großes Repository geht spürbar schneller — jeder Ordner wird nur noch einmal gelesen, und Ordner, deren Name mit einem Punkt beginnt (`.git`, `.obsidian`, `.trash` …), werden weder angezeigt noch durchsucht. Die Einstellung `ui/folderTreeHideDot = false` zeigt sie wieder.
- **In der Link-Einheit bleiben:** Wer einem Link folgt, während die Einheit *Links* aktiv ist, bleibt darin — das nächste Dokument beginnt beim ersten Link im Bild, und es geht ohne Maus von Link zu Link weiter. Links, die eine Suche mitbringen (die Treffer von *Suchen in Dateien*), öffnen weiterhin mit ihrer Suche.

### Behoben

- Die Bildlaufleisten von Ordneransicht und Gliederung konnten alle halbe Sekunde flackern, und mdVü erzeugte auch im Leerlauf eine kleine, aber dauernde Last im Task-Manager. Beides ist behoben — und Screenreader sagen nicht mehr ständig den Namen der Ordneransicht an.
- Die Ordnerseite zeigte das Badge **Obs**/**Git** ihres Vaults bzw. Repositorys nicht, und *Suchen in Dateien* bot von dort den Vault nicht als Bereich an. Auch die Trefferseite einer Suche zeigt jetzt das Badge ihres Ordners.
- Wikilinks in Tabellenzellen erschienen als reiner Text und waren nicht anklickbar. Sie funktionieren jetzt wie überall sonst, auch in der Alias-Form `[[Notiz\|Text]]`, die Obsidian in Tabellen verwendet. `%%Kommentare%%` in Tabellenzellen werden ebenfalls ausgeblendet.

## [0.15.0] — 2026-10-08

### Neu

- **Ordnerseite:** Ein in der Ordneransicht gewählter Ordner erscheint als Seite — seine Unterordner und Markdown-Dateien mit Größe, Datum und den ersten Zeilen jeder Datei. `Enter` wechselt mit Link-Navigation hinein: Die Pfeiltasten gehen von Datei zu Datei, `Enter` öffnet sie. Die Seite folgt Änderungen im Ordner. Siehe [Ordneransicht und Suche](docs/manual.de.md#ordneransicht-und-suche).
- **Zuletzt geändert auf einen Blick:** Ein farbiger Punkt hinter jeder Datei in der Ordneransicht zeigt, wie lange die letzte Änderung her ist — rot bis 10 Minuten, orange bis eine Stunde, gelb bis ein Tag, grau bis eine Woche. Ordner zeigen den Punkt ihrer zuletzt geänderten Datei, auch zugeklappt. Die Punkte folgen Änderungen durch andere Programme, solange mdVü offen ist, und eine eben geänderte oder neue Datei leuchtet kurz auf. Siehe [Ordneransicht und Suche](docs/manual.de.md#ordneransicht-und-suche).
- **Nach letzter Änderung filtern:** Die Uhr ⏱ im Kopf der Ordneransicht zeigt nur Dateien, die in den letzten 10 oder 30 Minuten, der letzten Stunde, dem letzten Tag oder der letzten Woche geändert wurden. Der Filter wirkt zusammen mit der Suche in der Ordneransicht und bleibt beim Wechsel in einen anderen Ordner eingeschaltet.
- **Zurück/Vor mit der Maus:** Die Seitentasten der Maus (und die Browser-Tasten mancher Tastaturen) blättern zurück und vor, wie im Browser. Auf Tastaturen mit `AltGr` wirkt `AltGr+←`/`→` wie `Alt+←`/`→` — einhändig neben den Pfeiltasten.

### Geändert

- **Hineinschauen beim Durchblättern:** Wer in Ordneransicht oder Gliederung klickt oder mit den Pfeiltasten läuft, sieht jedes Dokument weiterhin sofort — aber nur zum Hineinschauen (Peek): Es füllt nicht mehr den Verlauf (*Zurück*) und die Liste der zuletzt benutzten Dateien, und die Pfadleiste zeigt seinen Namen kursiv. `Enter` oder ein Doppelklick öffnet es richtig und setzt den Fokus ins Dokument; ebenso ein Klick ins Dokument oder `F6`. Mit `Enter` oder Doppelklick angesprungene Kapitel der Gliederung stehen jetzt im Verlauf. `Strg+Umsch+E` führt in die Ordneransicht. Siehe [Ordneransicht und Suche](docs/manual.de.md#ordneransicht-und-suche).
- **Kurze Hinweise statt Dialoge:** Wer über das Ende des Verlaufs hinaus zurück- oder vorblättert, bekommt kein Meldungsfenster mehr — die Statuszeile zeigt kurz rot *Start of history reached* bzw. *End of history reached*. Auch andere kurze Meldungen (Pfad kopiert, Vorschau gekappt, …) erscheinen dort.
- **Tiefe der Ordneransicht:** In einem Obsidian-Vault oder Git-Repository zeigt die Ordneransicht jetzt alle Unterordner statt zwei Ebenen. Anderswo bleibt es bei zwei Ebenen, damit das Öffnen eines Laufwerks nicht das ganze Laufwerk durchsucht. Wirken große Vaults oder Repositories dadurch langsamer, [geben Sie bitte Bescheid](https://github.com/m3repo/mdvu/issues) — dann könnte die Tiefe einstellbar werden.

### Behoben

- Beim Verbreitern des Fensters blitzen zwischen Ordneransicht und Dokument keine schmalen Streifen mit Dokumentinhalt mehr auf.

## [0.14.0] — 2026-10-07

### Neu

- **Kopieren mit Formatierung:** `Strg+C` im Dokument legt die Auswahl jetzt als Text *und* als HTML in die Zwischenablage, wie ein Browser. In Word, Outlook oder OneNote eingefügt, kommen Überschriften, Fett und Kursiv, Listen, Tabellen und Links als solche an — mit den Schriften und Farben des Drucklayouts. Eine nur teilweise markierte Überschrift oder Liste behält ihr Format. Bilder gehen als Verweis auf die Originaldatei im Originalformat mit (Word bettet sie beim Einfügen ein); relative Links und Obsidian-Embeds werden zu absoluten Pfaden. Die Flächen von Callouts kommen in Word noch nicht an.
- **Als Markdown kopieren:** `Strg+Umschalt+C` kopiert den Markdown-Quelltext der Auswahl — beginnt sie an einer Überschrift oder einem Listenpunkt, samt `##` bzw. `-`.
- **Kontextmenü im Dokument:** Ein Rechtsklick (oder die Menütaste) bietet Kopieren, Als Markdown kopieren, Zurück und Vor.
- **Zeilenumbruch mit `<br>`:** `<br>`, `<br/>` und `<br />` beginnen eine neue Zeile — auch in Tabellenzellen, wo Markdown sonst keinen Weg kennt. Siehe [Inline-HTML](docs/markdown-support.de.md#inline-html).
- **Zoom-Menü und Zoom bleibt erhalten:** Ein Klick auf den Zoomwert im Footer bietet alle Stufen von 50 bis 200 % an. Der Zoom bleibt für den nächsten Start erhalten (`doc/zoom` in der `settings.ini`).
- **Menü der Einheiten:** Ein Klick auf `SCROLL`/`CARET`/`LINK`/`HIT` im Footer öffnet ein Menü mit allen Lese-Einheiten.

### Geändert

- In *Suchen in Dateien* ist die Bereichsauswahl schmaler; aufgeklappt ist sie so breit wie der längste Eintrag.

### Behoben

- Im Caret-Modus springt die Hover-Hervorhebung im Footer nicht mehr zwischen dem Element unter der Maus und einem anderen hin und her.
- In schmalen Fenstern wandern die Knöpfe der Suchleisten nicht mehr nach links in die Ordneransicht.

## [0.13.0] — 2026-10-06

### Neu

- **Diagramme aus Mermaid-Codeblöcken:** Kreisdiagramme (`pie`), Balken-/Liniendiagramme (`xychart-beta`, auch waagerecht) und Sequenzdiagramme (`sequenceDiagram` mit Aktivierungen, Notizen, Rahmen, Nummerierung und Teilnehmer-Symbolen) zeichnet mdVü selbst — eine bewusst abgespeckte Teilmenge von Mermaid, ohne JavaScript. Die Diagramme folgen dem Dunkelmodus und der `user.css` und bleiben in Druck und PDF Vektorgrafik. Andere Diagrammarten bleiben Codeblöcke; ein fehlerhaftes Diagramm zeigt seinen Codeblock mit einem Hinweis auf die Zeile. Siehe [Diagramme](docs/markdown-support.de.md#diagramme-mermaid-teilmenge).
- **Flussdiagramme aus Mermaid-Codeblöcken:** `flowchart`/`graph` in allen vier Richtungen, mit den gängigen Knotenformen, gepunkteten und dicken Kanten, Kreis- und Kreuzenden, Kantenbeschriftungen und Schleifen. mdVü ordnet die Knoten in Ebenen an wie Mermaids Standard-Renderer, sodass Knoten und Beschriftungen nie überlappen und Kanten sich so selten wie möglich kreuzen. `subgraph`-Rahmen und Stilangaben werden vorerst übergangen. Siehe [Flussdiagramme](docs/markdown-support.de.md#flussdiagramme).
- **Lesen mit der Tastatur:** Die Pfeiltasten bewegen sich in einer Einheit, die Sie wählen und die der Footer anzeigt — `0` Scrollen (wie im Browser), `1` Caret (`F7` schaltet zwischen beiden um), `L` Links, `H` Suchtreffer. In der Einheit Links gehen `←`/`→` in Lesereihenfolge durch die Links, `↑`/`↓` zum nächstgelegenen Link in der Zeile darüber bzw. darunter, `Eingabe` folgt ihm; `Tab`/`Umschalt+Tab` gehen immer zum nächsten/vorigen Link. Begonnen wird beim ersten Link im Bild; das klappt auch in sehr großen Dokumenten, auch in noch nicht angezeigten Teilen. Die Einheit gehört zum Ort: Zurück bringt sie wieder, samt aktivem Link. Siehe [Lesen mit der Tastatur](docs/manual.de.md#lesen-mit-der-tastatur).
- **Favoriten:** `Strg+D` merkt den aktuellen Ordner als Favorit (der Stern in der Leiste zeigt es), `Strg+Umschalt+D` öffnet die Liste — Pfeiltasten und `Eingabe` öffnen einen, `Entf` entfernt ihn. Die Favoriten stehen auch im Menü *File* und im Menü einer Datei bzw. eines Ordners, und *Suchen in Dateien* kann alle Favoriten auf einmal durchsuchen, nach Favorit gruppiert. Siehe [Favoriten](docs/manual.de.md#favoriten).
- **Menü zur Datei:** Ein Klick auf den Dateipfad in der Statuszeile öffnet ein Menü für diese Datei — Pfad kopieren, im Explorer zeigen, in Obsidian öffnen (im Vault) oder mit einem anderen Programm. Ein Rechtsklick auf Datei oder Ordner in der Ordneransicht oder auf die Obs-/Git-Badges öffnet dasselbe Menü.
- **Menüleiste per Tastatur:** `F10` oder ein einzelnes `Alt` schaltet die Menüleiste in den Tastaturmodus — `←`/`→` wählen das Menü, `Eingabe` öffnet es, `↑`/`↓` und `Eingabe` führen einen Eintrag aus, ein Buchstabe springt dorthin, `Esc` geht zurück. `Alt`+Anfangsbuchstabe öffnet ein Menü direkt.

### Geändert

- **Aus der Suche ins Dokument:** In der Dokumentsuche sucht das erste `Eingabe`, jedes weitere — und `↓` jederzeit — wechselt ins Dokument mit der Einheit *Treffer*, `←`/`→` gehen dann durch sie weiter. Bei *Suchen in Dateien* wechseln `Eingabe` auf der schon angezeigten Trefferliste und `↓` jederzeit in die Liste mit der Einheit *Links*; sind Begriff oder Schalter geändert, sucht `↓` vorher. `Esc` geht Schritt für Schritt zurück: von Links oder Treffern ins Suchfeld, von dort aus dem Streifen zurück ins Dokument beim Scrollen.

### Behoben

- `Eingabe` und `Esc` in den Suchfeldern lösen keinen Windows-Ton mehr aus.

## [0.12.1] — 2026-10-03

### Neu

- **Links auf fehlende Notizen oder Dateien erscheinen blasser**, wie die nicht aufgelösten Links in Obsidian — Wikilinks wie relative Markdown-Links. Klickbar bleiben sie. Im Vault zieht die Markierung mit, wenn Sie eine Notiz anlegen oder löschen. Die Farbe lässt sich über `a.unresolved` in der `user.css` ändern.

## [0.12.0] — 2026-10-03

### Neu

- **Suchen in Dateien:** `Strg+Umschalt+F` durchsucht alle Markdown-Dateien des aktuellen Obsidian-Vaults, Git-Repositorys oder Ordners. Das Ergebnis ist ein eigenes Dokument: zuerst Dateien, deren Name passt, dann die Treffer nach Ordnern mit bis zu drei Zeilen Kontext. Ein Klick auf eine Zeilennummer öffnet die Datei genau an diesem Treffer, die Dokumentsuche ist belegt, `F3` geht weiter. Zurück führt an die alte Stelle der Liste, `F5` sucht neu. Große Ordner werden im Hintergrund durchsucht. Optionen: Groß-/Kleinschreibung, Wortanfang (`der` findet *derzeit* und *Nord-der*, nicht *oder*) und ganze Wörter. Siehe [Suchen in Dateien](docs/manual.de.md#suchen-in-dateien).
- **Markierungen und Inline-HTML:** `==Text==` markiert wie ein Textmarker, wie in Obsidian — auch im Druck und im PDF. Eine kurze Liste von HTML-Formatierungs-Tags wird verstanden: `<u>`, `<mark>`, `<s>`, `<b>`, `<i>`, `<kbd>` (Tastenkappen) und `<span class="…">` für eigene Stile; jedes andere Tag bleibt wörtlicher Text. Siehe [Markierungen](docs/markdown-support.de.md#markierungen) und [Inline-HTML](docs/markdown-support.de.md#inline-html).
- **Links springen zum Abschnitt in einem anderen Dokument:** `[[Notiz#Überschrift]]` und `[Details](notiz.md#installation)` öffnen das Dokument und scrollen zur Überschrift. Als Ziel taugt der Ankername oder der Text der Überschrift; `[[Notiz#Kapitel 2#Details]]` wählt „Details“ unter „Kapitel 2“, wenn der Titel doppelt vorkommt. Ein Link auf das schon offene Dokument springt nur. Die Gliederung geht denselben Weg: Nach Zurück führt Vor wieder an die dort zuletzt gewählte Überschrift. In großen Dateien springt mdVü, sobald die Überschrift geladen ist; fehlt sie, öffnet sich das Dokument oben mit einem Hinweis in der Statuszeile.
- **Fundstellen verlinken:** Ein Link `mdvu:open?uri=…&find=Begriff` öffnet das Dokument, markiert alle Fundstellen wie die Suche und blendet den Suchstreifen ein (`&case`, `&word`, `&hit=3` wie in der Suche). `&mark=12-14` oder `&mark=12:5-20` heben Zeilen bzw. Bereiche des Quelltexts hervor, beliebig oft, auf Wunsch farbig (`~warn`, `~ffcc00`); die Farbklassen lassen sich per `user.css` anpassen. `Esc` räumt ab. Siehe [Fundstellen verlinken](docs/markdown-support.de.md#fundstellen-verlinken).
- **Zurück führt dorthin, wo man war:** Vor/Zurück stellt die Leseposition wieder her statt am Dokumentanfang zu landen — verankert an der Textzeile, nicht an Pixeln, passt also auch nach geänderter Fensterbreite, Zoom oder stückweisem Nachladen. Eine laufende Suche kommt mit zurück: Begriff, Optionen, aktiver Treffer und Suchstreifen.
- **Suche in der Gliederung:** `Strg+F3` mit dem Fokus in der Gliederung filtert sie auf passende Überschriften (samt übergeordneten) und hebt den Suchtext hervor — wie in der Ordneransicht. Nach dem Schließen ist sie wieder so aufgeklappt wie vorher.

### Geändert

- **Die Suche im Dokument durchsucht den ganzen Text**, auch Teile großer Dateien, die noch nicht angezeigt wurden. Bisher fand sie dort nur, was schon aufgebaut war — Treffer weiter unten tauchten erst nach dem Hinscrollen auf.
- **Suchen beim Tippen:** Gesucht wird erst nach einer kurzen Pause (0,3 Sekunden) und ab 3 Zeichen, damit die Eingabe auch in großen Dokumenten flüssig bleibt. `Eingabe` und `F3` suchen sofort, auch kürzere Begriffe; in Anführungszeichen (`"ab"`) wird genau dieser Text gesucht.
- **`F3` / `Umschalt+F3` gelten immer dem Haupt-Pane**, auch wenn der Fokus in Ordneransicht oder Gliederung steht. Bereichsabhängig ist nur noch `Strg+F3`.

### Behoben

- Markdown-Links mit Sprungmarke in ein anderes Dokument (`andere.md#abschnitt`) führten ins Leere.
- Prozent-kodierte Links, wie Obsidian sie schreibt (`Meine%20Notiz.md`), wurden nicht gefunden.
- In sehr großen Dokumenten erreichten Sprungmarken und Gliederung noch nicht geladene Überschriften nicht, und weit auseinanderliegende gleichnamige Überschriften konnten denselben Anker tragen.
- Absturz in sehr großen Dokumenten, wenn nach weitem Scrollen mit `F3` gesucht oder Text ausgewählt wurde.
- Absturz, wenn nach einem Klick auf einen weit springenden Link mit gedrückter Maustaste weitergezogen wurde.
- Nach dem Schließen der Suche in der Ordneransicht war der Baum bis auf die gewählte Datei zugeklappt; er steht jetzt wieder wie vor der Suche.

## [0.11.0] — 2026-10-02

### Neu

- **Callouts sehen aus wie in Obsidian:** ein farbiger Kasten mit Titelzeile in der Farbe des Typs, hell wie dunkel. Ohne Titel steht der Typname da (`> [!warning]` → „Warning“). Die Farben sind Obsidians Standardfarben; Aliase wie `caution` oder `tldr` teilen die Farbe ihrer Gruppe, unbekannte Typen erscheinen wie `note`. Per `user.css` lässt sich jeder Typ samt Titelzeile (`callout-title`) umgestalten — siehe [Callouts einfärben](docs/css-customizing.de.md#callouts-einfärben).

### Behoben

- Der Titel eines Callouts (`> [!note] Mein Titel`) ging verloren.
- Durchgestrichenes und die Unterstreichung von Links fehlten im PDF-Export.

## [0.10.1] — 2026-09-30

### Behoben

- **Obsidian-Kommentare** (`%%…%%`, inline und als Block) wurden angezeigt — und mitgedruckt. Sie sind jetzt überall ausgeblendet, auch in Druck und PDF.

## [0.10.0] — 2026-09-30

### Neu

- **Wikilinks und Einbettungen wie in Obsidian:** In einem Vault werden `[[Notiz]]` und `![[bild.png]]` über den Namen im ganzen Vault aufgelöst — ohne Pfad, ohne `.md`; bei gleichen Namen gewinnt der Ordner der aktuellen Notiz, danach die nächste zur Vault-Wurzel. mdVü liest die Dateinamen des Vaults im Hintergrund ein und hält sie aktuell, eine in Obsidian angelegte Notiz oder ein eingefügtes Bild wird sofort gefunden. `[[#Überschrift]]` springt im Dokument. Außerhalb eines Vaults findet `[[Notiz]]` die `Notiz.md` neben der aktuellen Datei.
- **Obsidian-Vaults und Git-Repositories werden erkannt:** Die Statuszeile zeigt **Obs**, **Git** oder **Obs/Git** mit dem Ordnernamen; ein Klick öffnet den Vault bzw. das Repository in der Ordneransicht.
- In einem Obsidian-Vault folgen die Zeilenumbrüche dessen Einstellung *Strict line breaks* — Notizen sehen aus wie in Obsidian. Außerhalb eines Vaults bricht die neue Einstellung `doc/lineBreaks = newline` an jeder Zeile um.

### Behoben

- `[[Notiz]]` ohne `.md` führte ins Leere.
- Zeilenumbrüche mit zwei Leerzeichen oder einem Backslash (`\`) am Zeilenende wurden als Leerzeichen dargestellt; sie brechen jetzt um, wie es der Markdown-Standard verlangt.

## [0.9.0] — 2026-09-24

### Neu

- **Seiteneinrichtung** in der Druckvorschau: Eine Leiste oben wählt Drucker, Papierformat (A3, A4, A5, A6, Letter, Legal) und Hoch-/Querformat. Die Vorschau wird sofort neu umbrochen, Druck und PDF verwenden genau das angezeigte Format. *Printer setup…* öffnet die Windows-Druckereinstellungen, ohne zu drucken. `Strg+Umschalt+P` blendet die Leiste ein und aus; die Auswahl bleibt gespeichert (`print/paper`, `print/orientation`, `print/printer`).

### Geändert

- Gedruckt wird über die Seiteneinrichtung: Der Druckdialog startet mit dem gewählten Drucker und Papier, Änderungen darin fließen in die Vorschau zurück — Druckertreiber und Vorschau sind sich beim Format also immer einig.
- Der Suchstreifen benutzt jetzt native Windows-Bedienelemente: Er folgt dem Dunkelmodus und skaliert sauber mit der Bildschirm-DPI.

### Behoben

- Ausdrucke sitzen papiergenau: Der nicht bedruckbare Rand des Druckers wird jetzt herausgerechnet, statt die Seite um genau dieses Maß zu verschieben.

## [0.8.0] — 2026-09-16

Die erste öffentliche Beta und das erste Release unter dem Namen **mdVü**. Bis Version 0.6 hieß das Programm *mdView* und lag im Repository der m3-Bibliothek; es hat jetzt ein eigenes Repository, ein eigenes Versionsschema und einen eigenen Release-Ablauf.

### Neu

- **Gliederungsbereich** — alle Überschriften des offenen Dokuments als Baum unter der Ordneransicht; ein Klick springt zur Stelle und lässt das Ziel kurz aufleuchten.
- **Pfadleiste** über dem Dokument, mit klickbaren Pfadsegmenten.
- **Verlauf** wie im Browser: vor und zurück über die Symbole der Leiste oder `Alt+←` / `Alt+→`, Rechtsklick auf die Pfeile öffnet die Verlaufsliste.
- **Suche in allen Bereichen:** `Strg+F` öffnet den Suchstreifen für die gerade gelesene Ansicht, `F3` und `Umschalt+F3` springen durch die Treffer, `Strg+F3` sucht dort, wo der Tastaturfokus liegt — und ist der einzige Weg zur Ordneransicht, deren Baum während der Eingabe gefiltert wird. `Esc` schließt den Streifen; der Suchbegriff bleibt erhalten, `F3` nimmt die Suche damit wieder auf.
- **Startseite** mit den letzten fünf Dokumenten.
- **PDF-Export** mit einem Lesezeichen-Baum aus den Überschriften des Dokuments.
- **Absturzbericht**: Bei einer Zugriffsverletzung schreibt mdVü `mdvu.crash.log` neben die ausführbare Datei. Verschickt wird nichts — die Datei einzusenden oder zu ignorieren, bleibt dem Anwender überlassen.
- **Import-Prüfung im Release-Ablauf**: Die DLL-Importe der EXE werden vor dem Signieren gegen eine versionierte Baseline verglichen, eine eingeschlichene Netzwerkbibliothek fiele damit auf. mdVü bindet überhaupt keine Socket-DLL ein.
- **Signierte Releases**: Veröffentlichte Builds sind code-signiert und zeitgestempelt.

### Geändert

- **Umbenennung in mdVü.** Mitgewandert sind: der Einstellungsordner (`%APPDATA%\m3Works\mdVu`), die Dateityp-Kennung für die `.md`-Verknüpfung und das interne URL-Schema.
- Der Dokument-Lebenszyklus ist in die Render-Bibliothek gewandert, wodurch große Dateien spürbar geschmeidiger laden (der Dokumentanfang erscheint sofort, der Rest fließt nach).
- Der Dunkelmodus ist jetzt vollständig CSS-getrieben, eigene `user.css`-Regeln überleben also einen Moduswechsel.
- Überbreite Tabellen werden in Druck und PDF nun *eingepasst* statt gequetscht: Die Schrift schrumpft um bis zu 30 %, Langtext-Spalten werden gedeckelt, der Rest am rechten Rand abgeschnitten. Das alte Verhalten steht über `print/tableFit = squeeze` bereit.

### Hinweise für Tester, die von mdView 0.6 kommen

Die Umbenennung ist ein bewusster Schnitt:

- Einstellungen aus `%APPDATA%\m3Works\MarkdownView` werden **nicht** übernommen — Ordner, Verlaufsliste und die eigene `user.css` sind neu einzurichten.
- Eine bestehende `.md`-Verknüpfung zeigt weiterhin auf das alte Programm. Neu setzen über *Datei → Als Markdown-Standard registrieren*.
- Die Lizenz ist erneut zu bestätigen.

## Vorgeschichte

Die Versionen bis 0.6 erschienen als *mdView* und sind hier nicht dokumentiert. Sie brachten den Kern dessen, was mdVü heute ausmacht: den Markdown-Renderer mit eigener Layout-Engine, Druck und Druckvorschau, die Ordneransicht, den CSS-Editor, den Dunkelmodus, Drag & Drop, die `.md`-Dateiverknüpfung und die Lizenzmechanik.
