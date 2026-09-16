# mdVü — Handbuch

Markdown-Viewer für Windows · © 2026 Martin Niedergesäß — m3Works · *[English version](manual.md)*

---

Dies ist das ausführliche Handbuch für alle, die das ganze Bild wollen — samt Installation, Einstellungen und Fehlersuche. Eine kürzere Fassung steckt im Programm selbst: Taste `F1`.

**Inhalt**

- [Warum ein Markdown-Viewer?](#warum-ein-markdown-viewer)
- [Installation und erster Start](#installation-und-erster-start)
- [Das Fenster im Überblick](#das-fenster-im-überblick)
- [Dateien öffnen](#dateien-öffnen)
- [Ordneransicht und Suche](#ordneransicht-und-suche)
- [Gliederung](#gliederung)
- [Pfadleiste, vor und zurück](#pfadleiste-vor-und-zurück)
- [Die vier Ansichten](#die-vier-ansichten)
- [Drucken und PDF](#drucken-und-pdf)
- [Dunkelmodus](#dunkelmodus)
- [Darstellung anpassen](#darstellung-anpassen)
- [Einstellungen](#einstellungen)
- [Grenzen](#grenzen)
- [Tastaturkürzel](#tastaturkürzel)
- [Kommandozeile](#kommandozeile)
- [Fehlersuche](#fehlersuche)
- [Deinstallieren](#deinstallieren)

## Warum ein Markdown-Viewer?

Es gibt hervorragende Markdown-*Editoren* — Obsidian, Typora, VS Code und viele mehr. Warum also noch ein Viewer?

Weil Lesen etwas anderes ist als Schreiben. Wer schnell eine Notiz nachschlagen, eine Doku überfliegen oder eine per Mail erhaltene `.md`-Datei einfach nur *ansehen* will, braucht keinen Editor mit Plugins, Vault und Sync — sondern ein Programm, das sofort startet, die Datei anzeigt und wieder aus dem Weg ist.

mdVü ist genau dafür gebaut:

- **Schlank:** eine einzelne EXE unter 15 MB, keine Installation von Frameworks oder Laufzeitumgebungen.
- **Schnell:** native Windows-Anwendung mit eigener Render-Engine. Auch große Dokumente öffnen ohne spürbare Wartezeit.
- **Sparsam:** benötigt nur einen Bruchteil des Arbeitsspeichers Chromium-basierter Editoren, die für jedes Fenster einen kompletten Browser mitbringen.
- **Ergänzung, kein Ersatz:** mdVü will Obsidian & Co. nicht verdrängen. Es ist das Werkzeug für den schnellen Blick — Datei im Explorer doppelklicken, lesen, fertig. Der Editor bleibt fürs Schreiben zuständig.

## Installation und erster Start

Es gibt keinen Installer. mdVü ist eine einzelne ausführbare Datei:

1. `mdvu.exe` dorthin legen, wo es passt — Programmordner, USB-Stick, synchronisierter Ordner. Es läuft von überall.
2. Starten. Beim allerersten Start wird die Lizenz angezeigt und ist einmalig zu bestätigen.
3. Optional: *Datei → Als Markdown-Standard registrieren* sorgt dafür, dass `.md`-Dateien per Doppelklick in mdVü aufgehen.

Es wird nichts systemweit installiert, es sind keine Admin-Rechte nötig, und es werden weder Dienste noch geplante Aufgaben angelegt. Außerhalb des eigenen Ordners schreibt das Programm an genau zwei Stellen — siehe [Deinstallieren](#deinstallieren).

**Falls SmartScreen warnt:** veröffentlichte Builds sind code-signiert und zeitgestempelt, aber Windows bewertet zusätzlich die *Reputation*, die ein neuer Build erst noch sammeln muss. „Weitere Informationen → Trotzdem ausführen“ startet das Programm; die Signatur lässt sich vorher über *Eigenschaften → Digitale Signaturen* prüfen.

## Das Fenster im Überblick

![mdVü-Hauptfenster (stilisiert)|620](img/mdvu-window.svg)

Das Fenster hat keine klassische Menüleiste — das **Hauptmenü sitzt in der Titelleiste** (*Datei*, *Ansicht*, *Hilfe*), neben den Symbolen der Werkzeugleiste.

Darunter ist das Fenster geteilt:

- **links oben:** die **Ordneransicht** — der aktuelle Ordner als Baum, nur `.md`-Dateien
- **links unten:** die **Gliederung** des geöffneten Dokuments — alle Überschriften als Baum
- **rechts oben:** die **Pfadleiste** mit dem Ort der aktuellen Datei
- **rechts in der Mitte:** das **Dokument**
- **unten:** die Statuszeile mit Angaben zum Dokument und Hinweisen

`F6` schaltet den Tastaturfokus reihum zwischen den Bereichen weiter.

## Dateien öffnen

Es gibt mehrere Wege, eine Datei zu öffnen:

- **Drag & Drop:** eine `.md`-Datei oder einen ganzen **Ordner** auf das Fenster ziehen. Ein Ordner wird in der Ordneransicht geöffnet. Wird mehreres zugleich fallengelassen, hat eine Datei Vorrang vor einem Ordner.
- **Öffnen-Dialog** mit `Strg+O`.
- **Ordneransicht:** Ein Klick auf eine Datei im Ordnerbaum links zeigt sie sofort an — auch beim Durchblättern mit den Pfeiltasten folgt die Anzeige.
- **Zuletzt verwendet:** Das *Datei*-Menü führt die zuletzt geöffneten Dateien und Ordner. Auch die **Startseite** (*Datei → Startseite*) zeigt die letzten fünf Dateien.
- **Doppelklick im Explorer:** Über *Datei → Als Markdown-Standard registrieren* verknüpft sich mdVü mit `.md`-Dateien (pro Benutzer, keine Admin-Rechte nötig). Windows fragt ggf. einmalig per „Öffnen mit“ nach — siehe [Fehlersuche](#fehlersuche).
- **Kommandozeile:** `mdvu.exe "C:\Notizen\Liesmich.md"` — siehe [Kommandozeile](#kommandozeile).

Wird die angezeigte Datei von einem anderen Programm geändert, lädt mdVü sie automatisch neu — die Scrollposition bleibt erhalten. Mit `F5` geht das auch von Hand. Dateien, die im aktuellen Ordner hinzukommen oder verschwinden, erscheinen im Baum ohne manuelles Auffrischen; das gilt rekursiv, also auch für Unterordner.

Sehr große Dateien werden bis zu einer Grenze von **50 MB** geladen — ein Banner am Dokumentanfang weist darauf hin, dass nur der Anfang angezeigt wird. Siehe [Grenzen](#grenzen).

## Ordneransicht und Suche

Die Ordneransicht zeigt den Ordner des aktuellen Dokuments, gefiltert auf `*.md`. Sie ist kein Vault und kein Workspace: es ist schlicht der Ordner, in dem man gerade ist, und sie folgt der Navigation.

`Strg+F` öffnet den Suchstreifen für das Haupt-Pane — also für die gerade sichtbare Ansicht: Dokument, Quelltext, CSS oder Druckvorschau. `F3` und `Umschalt+F3` springen zum nächsten bzw. vorherigen Treffer; das geht aus dem Suchfeld heraus genauso wie aus dem Dokument, man kann also weiterlesen und mit `F3` weiterspringen.

`Strg+F3` sucht dort, wo Sie gerade sind — der Bereich mit dem Tastaturfokus bekommt den Streifen. Nur so erreicht man die Ordneransicht, und anders als `Strg+F` schaltet diese Taste den Streifen auch wieder aus.

In der **Ordneransicht** erscheint der Streifen über dem Baum. Während der Eingabe wird der Baum auf passende Dateien gefiltert, Treffer werden im Namen hervorgehoben. Die Pfeil-runter-Taste setzt den Fokus vom Suchfeld in den Baum — tippen, dann blättern, ganz ohne Maus.

Im **Dokument, im Quelltext, im CSS-Editor und in der Druckvorschau** erscheint der Streifen unter der Pfadleiste und arbeitet wie die Suchleiste eines Browsers: `Eingabe` und `Umschalt+Eingabe` gehen durch die Treffer, ein Zähler zeigt *Treffer / gesamt*, und alle Treffer sind gleichzeitig hervorgehoben. Drei Umschalter verfeinern die Suche:

| Umschalter | Bedeutung |
|---|---|
| `Aa` | Groß-/Kleinschreibung beachten (standardmäßig aus) |
| `.*` | Suchtext als regulären Ausdruck lesen |
| `Sel` | Suche auf die aktuelle Auswahl beschränken (nur im Dokument; braucht eine nicht-leere Auswahl) |

Nochmal `Strg+F3`, `Esc` oder der `X`-Knopf schließt den Streifen — Hervorhebungen verschwinden, der Ordnerfilter wird aufgehoben. Der Suchbegriff selbst bleibt erhalten: `Strg+F` holt ihn wieder ins Feld, `F3` nimmt die Suche beim ersten Treffer wieder auf. Damit kann `F3` auch ohne sichtbaren Streifen Hervorhebungen im Dokument stehen lassen; `Esc` im Dokument räumt sie weg.

Es ist immer höchstens ein Streifen offen; ein Ansichtswechsel schließt ihn.

Hinweis zur Druckvorschau: Sie durchsucht, was tatsächlich paginiert wurde. Dokumente, die an der 200-Seiten-Grenze abgeschnitten sind, enden auch für die Suche dort.

## Gliederung

Unterhalb der Ordneransicht zeigt mdVü die **Gliederung** des aktuellen Dokuments — alle Überschriften als Baum, nach Ebenen verschachtelt. Ein Klick springt zur entsprechenden Stelle im Dokument; das Sprungziel leuchtet kurz auf, damit das Auge es sofort findet.

Bei einem langen Dokument ist die Gliederung der schnellste Weg: kein Scrollen, kein Suchen, ein Klick.

## Pfadleiste, vor und zurück

Über dem Dokument zeigt die **Pfadleiste** den Ort der aktuellen Datei. Jedes Segment ist klickbar: Ein Klick auf einen Ordner öffnet ihn in der Ordneransicht.

Wie im Browser navigiert mdVü durch die Historie: Pfeil-Symbole in der Leiste oder `Alt+←` / `Alt+→`. Ein **Rechtsklick auf die Pfeile** öffnet die Verlaufsliste — damit lässt sich ein früheres Dokument direkt anspringen, statt sich Schritt für Schritt zurückzuklicken.

Links innerhalb von Dokumenten funktionieren wie erwartet: ein relativer Link auf eine andere `.md`-Datei öffnet diese Datei, ein Link auf eine Überschrift (`#abschnitt`) springt im Dokument, ein `http(s)`-Link geht nach Rückfrage in den Browser. Links, die ins Leere oder ins Zwielichtige führen, werden abgelehnt statt befolgt.

## Die vier Ansichten

Der Dokumentbereich beherbergt vier austauschbare Ansichten:

| Ansicht | Kürzel | Wofür |
|---|---|---|
| **Markdown** | `Strg+1` | das gerenderte Dokument — die normale Ansicht |
| **Quelltext** | `Strg+2` | der rohe Markdown-Text, syntaxgefärbt, nur lesend |
| **CSS** | `Strg+4` | das eigene Stylesheet, siehe [Darstellung anpassen](#darstellung-anpassen) |
| **Druckvorschau** | `Strg+F2` oder `Strg+3` | das umbrochene Dokument, so wie es druckt |

Beim Zurückschalten von der CSS-Ansicht auf die Markdown-Ansicht wird das geänderte Stylesheet sofort angewandt.

## Drucken und PDF

mdVü bringt eine eigene Druck- und PDF-Ausgabe mit — kein Umweg über den Browser oder einen PDF-Druckertreiber:

- **Druckvorschau** (`Strg+F2`): auch bei umfangreichen Dokumenten stehen 100 Seiten in wenigen Sekunden bereit.
- **Natives PDF:** *Ansicht → Als PDF exportieren* erzeugt ein echtes Vektor-PDF mit kopierbarem Text und einem Lesezeichen-Baum aus den Überschriften des Dokuments. Die Dateien sind in der Regel kleiner als bei „Drucken als PDF“ über einen Druckertreiber.
- **Saubere Seitenumbrüche:** Beim Umbruch werden verwaiste Zeilen berücksichtigt — eine einzelne Absatzzeile bleibt nicht allein am Seitenende oder Seitenanfang stehen.
- **Überbreite Tabellen** werden automatisch eingepasst: Die Schrift wird maßvoll verkleinert (bis 70 %), was dann noch übersteht, wird am rechten Seitenrand abgeschnitten — die wichtigen Spalten also nach links stellen. Langtext-Spalten werden bei knappem Platz auf 30 % der Seitenbreite gedeckelt. Das bisherige Verhalten (alle Spalten auf die Seite quetschen) bleibt über die Einstellung `print/tableFit = squeeze` verfügbar.
- **Drucken** direkt aus der Ansicht mit `Strg+P`.

Die Druck- und PDF-Ausgabe ist immer hell, unabhängig vom Dunkelmodus der Anzeige — ein dunkler Seitengrund würde Toner verschwenden und sich auf Papier schlecht lesen. Vorschau, Druck und PDF sind auf die ersten **200 Seiten** begrenzt; wird ein Dokument gekürzt, erscheint ein Hinweis in der Statuszeile.

## Dunkelmodus

*Ansicht → Dark Mode* schaltet die komplette Oberfläche samt Dokument um. Die Einstellung wird gemerkt.

Der Dunkelmodus im Dokument ist vollständig CSS-getrieben: Das eingebaute dunkle Stylesheet wird über das helle gelegt. Das ist wichtig, sobald man eigenes CSS schreibt — [Anpassen per CSS](css-customizing.de.md) erklärt, warum eine nur für den Dunkelmodus gesetzte Farbe beim Zurückschalten „hängenbleiben“ kann.

## Darstellung anpassen

Über *Ansicht → CSS* (`Strg+4`) lässt sich ein eigenes Stylesheet bearbeiten, das über die eingebauten Vorgaben gelegt wird. Damit können z.B. Schriftart, Schriftgröße, Farben und Abstände angepasst werden. Die Datei (`user.css`) liegt im Einstellungsordner und bleibt über Updates hinweg erhalten.

Beim ersten Start ist sie mit einem Kommentar und einer Zeile vorbelegt:

```css
@import "builtin:default.css";
```

Diese Zeile ist der Schalter für das eingebaute Design. Bleibt sie stehen, legen sich die eigenen Regeln darüber. Wird sie aus einer nicht-leeren `user.css` entfernt, lädt mdVü weder das Standard-Stylesheet noch dessen dunkles Gegenstück — dann gestaltet man von Null an.

Wichtig zu wissen: mdVü unterstützt bewusst nur eine **Teilmenge** von CSS — nicht alles, was ein Browser mit HTML5 kann. Der Umfang ist absichtlich klein gehalten, denn genau daraus bezieht mdVü seine Geschwindigkeit und seinen geringen Speicherbedarf. Tipp: Schriftgrößen in `pt` angeben, dann skaliert die Anzeige sauber mit der Bildschirm-DPI.

Die vollständige Referenz mit durchgerechneten Beispielen steht in [Anpassen per CSS](css-customizing.de.md).

## Einstellungen

Einen Einstellungsdialog gibt es noch nicht. *Hilfe → Setting* öffnet einen kleinen Hinweis mit einem klickbaren Link auf den Einstellungsordner:

```
%APPDATA%\m3Works\mdVu
```

Darin liegen `settings.ini` (Werte) und `user.css` (das eigene Stylesheet). Werte werden sofort geschrieben — mdVü verliert bei einem Absturz keine Einstellung, das heißt aber auch: **vor dem Bearbeiten der `settings.ini` von Hand das Programm schließen**, sonst werden die Änderungen wieder überschrieben.

Die Schlüssel sind hierarchisch: alles vor dem Schrägstrich ist der INI-Abschnitt, alles dahinter der Name. `doc/maxLoadMB = 80` sieht in der Datei also so aus:

```ini
[doc]
maxLoadMB=80
```

Die Werte, die man kennen sollte:

| Schlüssel | Bedeutung |
|---|---|
| `doc/maxLoadMB` | Ladegrenze für ein einzelnes Dokument in MB (Standard 50) |
| `print/tableFit` | wie überbreite Tabellen eingepasst werden: `shrink` (Standard) oder `squeeze` |
| `print/tableMaxColPct` | maximale Breite einer Langtext-Spalte in Prozent der Seite (Standard 30) |
| `print/tableMinFontPct` | wie weit die Schrift beim Einpassen schrumpfen darf, in Prozent (Standard 70) |
| `ui/theme`, `ui/mode` | benanntes Stylesheet und hell/dunkel/System — wird vom Dark-Mode-Befehl geschrieben |
| `ui/currentFolder` | Ordner, der beim nächsten Start wiederhergestellt wird |
| `ui/fileMru`, `ui/folderMru` | zuletzt benutzte Dateien und Ordner |
| `ui/resizeBudgetMs`, `ui/resizeSettleMs`, `ui/resizeRefreshMs` | Zeitverhalten des Neuumbruchs während der Größenänderung des Fensters |

## Grenzen

mdVü hat einige bewusst gesetzte harte Grenzen. Sie sorgen dafür, dass eine ungewöhnliche Datei das Programm nicht einfrieren kann:

| Grenze | Wert | Was passiert |
|---|---|---|
| Dateigröße | 50 MB | nur der Anfang wird angezeigt, mit gelbem Banner am Dokumentkopf; über `doc/maxLoadMB` änderbar |
| Seiten in Vorschau / Druck / PDF | 200 | die Ausgabe wird gekappt, mit Hinweis in der Statuszeile |
| Einzelner Absatz | 100 KB | ein überlanger Absatz wird geteilt (betrifft generierte Dateien, nicht von Hand geschriebenen Text) |

## Tastaturkürzel

| Taste | Funktion |
|---|---|
| `Strg+O` | Datei öffnen |
| `F1` | Handbuch |
| `Strg+F` | Suche im Haupt-Pane |
| `F3` / `Umschalt+F3` | Nächster / vorheriger Treffer |
| `Strg+F3` | Suche im fokussierten Bereich ein/aus (inkl. Ordneransicht) |
| `Esc` | Suchstreifen schließen / Hervorhebungen wegräumen |
| `F5` | Dokument neu laden |
| `F6` | Zwischen Bereichen wechseln (Baum / Dokument / Editor) |
| `Alt+←` / `Alt+→` | Zurück / Vorwärts |
| `Strg+1` | Markdown-Ansicht |
| `Strg+2` | Quelltext-Ansicht |
| `Strg+3` / `Strg+F2` | Druckvorschau |
| `Strg+4` | CSS bearbeiten |
| `Strg+P` | Drucken |

## Kommandozeile

```
mdvu.exe "C:\Notizen\Liesmich.md"   Datei öffnen
mdvu.exe "C:\Notizen"               Ordner öffnen
mdvu.exe -accepteula                Lizenz ohne Rückfrage bestätigen
```

Der erste Parameter darf eine Datei oder ein Ordner sein; eine Datei wird geöffnet, ein Ordner in der Ordneransicht gezeigt. Auf diesem Weg funktioniert auch die Explorer-Verknüpfung.

`-accepteula` ist für unbeaufsichtigte Installationen gedacht, wo der Erststart-Dialog im Weg wäre — es hinterlegt die Bestätigung genauso, wie es ein Klick auf *Akzeptieren* täte.

## Fehlersuche

**Ein Doppelklick auf eine `.md`-Datei öffnet weiterhin das alte Programm.**
Windows merkt sich für Dateitypen eine eigene Benutzerentscheidung, die Vorrang vor der Registrierung einer Anwendung hat. Rechtsklick auf die Datei → *Öffnen mit* → *Andere App auswählen* → mdVü → *Immer*. Danach sitzt die Verknüpfung.

**Ein Bild im Dokument wird nicht angezeigt.**
mdVü löst relative Bildpfade gegen den Ort des Dokuments auf — das Bild muss von dort aus erreichbar sein. Bilder aus dem Internet werden nicht geladen, das Programm hat überhaupt keinen Netzwerkzugriff. Unterstützt sind die üblichen Windows-Formate (PNG, JPEG, GIF, BMP, TIFF, SVG); eine unlesbare Datei wird übersprungen, nicht gemeldet.

**Meine CSS-Regel greift nicht.**
Die häufigsten Ursachen: eine Einheit, die die Engine nicht auflösen kann (`pt`, `px`, `mm`, `cm` oder `in` verwenden — *nicht* `em` oder `%` für Größen), ein Selektor für etwas, das das Dokument gar nicht erzeugt, oder eine aus der `user.css` entfernte `@import`-Zeile. Die [CSS-Dokumentation](css-customizing.de.md) enthält genau dafür eine Checkliste.

**Am Bildschirm sieht es richtig aus, auf Papier nicht.**
Druck, Vorschau und PDF benutzen ein eigenes Stylesheet und sind immer hell. Regeln, die nur im Dunkelmodus-Block stehen, wirken dort nicht.

**Das Fenster ist dunkel, das Dokument blieb weiß** (oder umgekehrt).
Dunkelmodus einmal aus- und wieder einschalten. Bleibt es dabei, ist das eine Meldung wert — bitte dazuschreiben, ob es direkt nach dem allerersten Start auftrat.

**Das Programm ist abgestürzt.**
mdVü schreibt `mdvu.exe.crash.log` neben die ausführbare Datei. Die Datei enthält Fehlerort und Stapelabzug, keine Dokumentinhalte. Verschickt wird nichts — ob du sie einsendest, entscheidest du allein; sie erhöht die Chance auf eine Korrektur erheblich.

## Deinstallieren

`mdvu.exe` löschen. Optional außerdem:

- den Einstellungsordner `%APPDATA%\m3Works\mdVu` (Einstellungen und die eigene `user.css`)
- den Registry-Schlüssel `HKCU\Software\m3Works\mdVu` (die Lizenz-Bestätigung)
- die Dateiverknüpfung, über *Datei → Markdown-Registrierung entfernen* **bevor** die EXE gelöscht wird

Mehr fasst mdVü nie an.

---

*mdVü befindet sich in der Beta-Phase. Das Programm wird kostenlos und „wie besehen“ („AS IS“) bereitgestellt; eine Gewährleistung für Fehlerfreiheit oder Eignung für einen bestimmten Zweck wird nicht übernommen. Siehe [LICENSE](../LICENSE.md).*
