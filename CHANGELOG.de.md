# Änderungsverlauf

*[English version](CHANGELOG.md)*

Hier stehen alle nennenswerten Änderungen an mdVü. Das Format folgt [Keep a Changelog](https://keepachangelog.com/de/1.1.0/); Versionen sind `Major.Minor.Patch`, die vierte Stelle in der Dateiversion der EXE ist der Build-Zähler.

## [0.7.0] — unveröffentlicht

Die erste öffentliche Beta und das erste Release unter dem Namen **mdVü**. Bis Version 0.6 hieß das Programm *mdView* und lag im Repository der m3-Bibliothek; es hat jetzt ein eigenes Repository, ein eigenes Versionsschema und einen eigenen Release-Ablauf.

### Neu

- **Gliederungsbereich** — alle Überschriften des offenen Dokuments als Baum unter der Ordneransicht; ein Klick springt zur Stelle und lässt das Ziel kurz aufleuchten.
- **Pfadleiste** über dem Dokument, mit klickbaren Pfadsegmenten.
- **Verlauf** wie im Browser: vor und zurück über die Symbole der Leiste oder `Alt+←` / `Alt+→`, Rechtsklick auf die Pfeile öffnet die Verlaufsliste.
- **Ordnersuche** (`F3`): Der Ordnerbaum wird während der Eingabe gefiltert, Treffer werden hervorgehoben.
- **Startseite** mit den letzten fünf Dokumenten.
- **PDF-Export** mit einem Lesezeichen-Baum aus den Überschriften des Dokuments.
- **Absturzbericht**: Bei einer Zugriffsverletzung schreibt mdVü `mdvu.exe.crash.log` neben die ausführbare Datei. Verschickt wird nichts — die Datei einzusenden oder zu ignorieren, bleibt dem Anwender überlassen.
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
