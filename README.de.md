![mdVü|860](docs/img/welcome-banner.svg)

# mdVü — ein Markdown-Viewer für Windows

*[English version](README.md)*

**Lesen ist etwas anderes als Schreiben.** Wer schnell eine Notiz nachschlagen, eine Doku überfliegen oder eine per Mail erhaltene `.md`-Datei einfach nur *ansehen* will, braucht keinen Editor mit Plugins, Vault und Sync — sondern ein Programm, das sofort startet, die Datei anzeigt und wieder aus dem Weg ist.

Genau dafür ist mdVü gebaut.

![mdVü-Hauptfenster (stilisiert)|620](docs/img/mdvu-window.svg)

*Die Abbildung ist eine stilisierte Darstellung des Fensteraufbaus — echte Screenshots folgen mit dem ersten öffentlichen Release.*

## Was es anders macht

- **Schlank** — eine einzelne EXE unter 15 MB. Kein Installer, kein Framework, keine Laufzeitumgebung, keine Browser-Engine. Irgendwohin kopieren und starten.
- **Schnell** — native Windows-Anwendung mit eigener Layout-Engine. Große Dokumente öffnen ohne spürbare Wartezeit; eine Druckvorschau über 100 Seiten steht in Sekunden.
- **Sparsam** — ein Bruchteil des Arbeitsspeichers Chromium-basierter Editoren, weil hier kein Chromium mitläuft.
- **Offline und ruhig** — mdVü bindet keine einzige Netzwerk-DLL ein. Keine Telemetrie, keine Update-Anfragen, keine Konten. Jedes Release wird [gegen eine Baseline seiner eigenen Importe geprüft](#datenschutz-und-sicherheit), bevor es signiert wird.
- **Echte Druck- und PDF-Ausgabe** — ein echtes Vektor-PDF mit kopierbarem Text, direkt erzeugt, ohne Umweg über Browser oder PDF-Druckertreiber.
- **Ergänzung, kein Ersatz** — Obsidian, Typora und VS Code bleiben fürs Schreiben zuständig. mdVü ist das Werkzeug für den schnellen Blick: im Explorer doppelklicken, lesen, fertig.

## Funktionen im Überblick

| | |
|---|---|
| **Formate** | GitHub-Flavoured Markdown, dazu Obsidian-Callouts, Wikilinks und Bild-Embeds — siehe [Markdown-Unterstützung](docs/markdown-support.de.md) |
| **Ordneransicht** | Baum des aktuellen Ordners mit Live-Aktualisierung, Suche während der Eingabe (`Strg+F3`) und Blättern per Pfeiltasten |
| **Gliederung** | Alle Überschriften des Dokuments als Baum; ein Klick springt zur Stelle und lässt das Ziel kurz aufleuchten |
| **Navigation** | Vor/Zurück wie im Browser samt Verlaufsliste, klickbare Pfadleiste, funktionierende Links zwischen Dokumenten |
| **Druck & PDF** | Druckvorschau, natives PDF, automatisches Einpassen überbreiter Tabellen, Umbruch ohne verwaiste Zeilen |
| **Dunkelmodus** | Oberfläche und Dokument; Druck, Vorschau und PDF bleiben bewusst hell |
| **Eigenes Aussehen** | Eine `user.css` über den eingebauten Vorgaben — siehe [Anpassen per CSS](docs/css-customizing.de.md) |
| **Windows-Integration** | Drag & Drop, Kommandozeile, `.md`-Verknüpfung pro Benutzer (ohne Admin-Rechte) |
| **Automatisches Neuladen** | Die geöffnete Datei lädt sich selbst neu, wenn ein anderes Programm sie ändert — die Scrollposition bleibt |

## Dokumentation

| Dokument | Inhalt |
|---|---|
| [Handbuch](docs/manual.de.md) | Das ausführliche Handbuch: Dateien öffnen, Ordneransicht, Gliederung, Drucken, PDF, Dunkelmodus, Tastaturkürzel, Einstellungen |
| [Markdown-Unterstützung](docs/markdown-support.de.md) | Welche Syntax genau dargestellt wird — und was bewusst nicht |
| [Anpassen per CSS](docs/css-customizing.de.md) | Die unterstützte CSS-Teilmenge, die Stolpersteine und durchgerechnete Beispiele für die `user.css` |
| [Beispieldateien](samples/) | Markdown-Dateien zum Ausprobieren, darunter eine Schau des Syntax-Highlightings |
| [Änderungsverlauf](CHANGELOG.de.md) | Was sich von Version zu Version geändert hat |

Das Handbuch steckt außerdem im Programm: Taste `F1`.

## Voraussetzungen

- Windows 10 oder 11 (64-Bit-Windows, 32-Bit-Anwendung)
- Kein .NET, kein Visual-C++-Redistributable, kein WebView2 — die EXE bringt alles mit
- Rund 15 MB Plattenplatz

Die Einstellungen liegen unter `%APPDATA%\m3Works\mdVu`, die einmalige Lizenz-Bestätigung unter `HKCU\Software\m3Works\mdVu`. Sonst wird außerhalb des Programmordners nichts geschrieben; wer beides entfernt, entfernt jede Spur.

## Download

Releases werden auf der [Releases-Seite](https://github.com/m3repo/mdvu/releases/latest) veröffentlicht: eine einzelne, signierte `mdvu.exe`, kein Installer, keine Einrichtung. Herunterladen, hinlegen wo es passt, starten. Zu jedem Release stehen der SHA-256-Hash der Datei und ein Link auf den zugehörigen VirusTotal-Report — damit lässt sich prüfen, ob das Heruntergeladene das hier Veröffentlichte ist.

## Hinweis zur Beta

mdVü ist eine **Vorschau-Version**. Sie hat viel internes Testen hinter sich, trotzdem können sich Funktionen ändern und Fehlfunktionen sind nicht auszuschließen. Das Programm wird kostenlos und „wie besehen“ („AS IS“) bereitgestellt — siehe [LICENSE](LICENSE.md).

Rückmeldungen sind willkommen, gerade jetzt: was sich falsch anfühlt, was fehlt, was kaputtgeht. Für alles Reproduzierbare bitte ein [Issue anlegen](https://github.com/m3repo/mdvu/issues) — dann sehen es andere Tester mit. Für Absturzprotokolle (`mdvu.exe.crash.log`, wird neben der EXE abgelegt) oder Dinge, die nicht öffentlich stehen sollen, geht eine Mail an `mdView@outlook.de` (die Adresse stammt noch aus der Zeit vor der Umbenennung und funktioniert weiterhin).

## Datenschutz und Sicherheit

- **Kein Netzwerkzugriff.** mdVü enthält keinen HTTP-, Socket- oder Update-Code. Die Import-Tabelle der EXE wird vor jedem Release gegen eine versionierte Baseline geprüft — statische *und* Delay-Load-Tabelle —, zusätzlich wird das Binary als Text nach Netzwerk-DLL-Namen und COM-Kennungen durchsucht, damit auch eine per `LoadLibrary` nachgeladene Bibliothek auffiele.
- **Keine Telemetrie, keine Konten, keine Cloud.** Geöffnete Dokumente verlassen den Rechner nicht.
- **Signierte Releases.** Jede veröffentlichte EXE ist code-signiert und zeitgestempelt. Windows SmartScreen kann bei einem frisch veröffentlichten Build dennoch warnen, bis die Signatur Reputation aufgebaut hat — das ist eine Frage der Download-Zahl, nicht der Gültigkeit der Signatur.
- **Absturzberichte bleiben bei dir.** Bei einer Zugriffsverletzung schreibt mdVü eine Textdatei neben die EXE. Verschickt wird nichts; ob du sie mailst, entscheidest du.

## KI-Unterstützung

mdVü ist ein Ein-Personen-Projekt, und KI-Werkzeuge gehören zum täglichen Handwerkszeug — sie helfen bei Teilen des Quelltextes, bei Texten und bei einem Teil der Grafiken. Ausgeliefert wird nichts Ungelesenes: Die Entwurfsentscheidungen sind meine, und alles im Programm und in dieser Dokumentation ist von Hand geprüft und gepflegt.

## Lizenzen

Hier wohnen drei verschiedene Dinge unter einem Dach:

| Was | Lizenz |
|---|---|
| Das Programm (`mdvu.exe`) | Kostenlos, proprietär — [LICENSE](LICENSE.md) (enthält die Hinweise zu Komponenten Dritter) |
| Dokumentation in diesem Repository (`README*`, `docs/`) | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.de) |
| Beispieldateien (`samples/`) | [MIT](https://opensource.org/licenses/MIT) — dürfen frei in eigene Projekte übernommen werden |

Der Quellcode von mdVü wird nicht veröffentlicht.

---

© 2026 Martin Niedergesäß — m3Works
