# Änderungsverlauf

*[English version](CHANGELOG.md)*

Hier stehen alle nennenswerten Änderungen an mdVü. Das Format folgt [Keep a Changelog](https://keepachangelog.com/de/1.1.0/); Versionen sind `Major.Minor.Patch`, die vierte Stelle in der Dateiversion der EXE ist der Build-Zähler.

## [Unreleased]

### Neu

- **Links springen zum Abschnitt in einem anderen Dokument:** `[[Notiz#Überschrift]]` und `[Details](notiz.md#installation)` öffnen das Dokument und scrollen zur Überschrift. Als Ziel taugt der Ankername oder der Text der Überschrift; `[[Notiz#Kapitel 2#Details]]` wählt „Details“ unter „Kapitel 2“, wenn der Titel doppelt vorkommt. Ein Link auf das schon offene Dokument springt nur. In großen Dateien springt mdVü, sobald die Überschrift geladen ist; fehlt sie, öffnet sich das Dokument oben mit einem Hinweis in der Statuszeile.

### Behoben

- Markdown-Links mit Sprungmarke in ein anderes Dokument (`andere.md#abschnitt`) führten ins Leere.
- Prozent-kodierte Links, wie Obsidian sie schreibt (`Meine%20Notiz.md`), wurden nicht gefunden.
- In sehr großen Dokumenten erreichten Sprungmarken und Gliederung noch nicht geladene Überschriften nicht, und weit auseinanderliegende gleichnamige Überschriften konnten denselben Anker tragen.

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
