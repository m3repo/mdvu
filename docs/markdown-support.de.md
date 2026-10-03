# Markdown-Unterstützung

*[English version](markdown-support.md)*

mdVü liest **GitHub-Flavoured Markdown (GFM)** und dazu die beiden Obsidian-Erweiterungen, auf die es beim Lesen von Notizen ankommt: Callouts und Wikilinks. Diese Seite listet auf, was tatsächlich dargestellt wird, was *anders* aussieht als im Browser und was bewusst fehlt.

Der Gedanke hinter den Auslassungen: mdVü rendert Markdown direkt in einen Layout-Baum — dazwischen liegt kein HTML, kein Browser, kein DOM. Daher kommen die Geschwindigkeit und der kleine Speicherbedarf, und daher fehlt auch eine Handvoll browsertypischer Funktionen.

Alles auf einmal sehen? [`samples/showcase.de.md`](../samples/showcase.de.md) in mdVü öffnen.

## Blockelemente

| Syntax | Anmerkung |
|---|---|
| `# Überschrift` … `###### Überschrift` | sechs Ebenen |
| `Überschrift` + `=====` / `-----` | Setext-Überschriften funktionieren ebenfalls |
| Absätze | eine Leerzeile trennt sie |
| Zwei Leerzeichen oder `\` am Zeilenende | harter Zeilenumbruch innerhalb eines Absatzes |
| `- Punkt`, `* Punkt`, `+ Punkt` | Aufzählungen, verschachtelbar |
| `1. Punkt`, `1) Punkt` | nummerierte Listen; die erste Zahl wird übernommen, eine Liste darf also bei 5 beginnen |
| `- [ ] offen`, `- [x] erledigt` | Aufgabenlisten mit Kästchen |
| `> Zitat` | Blockzitate, verschachtelbar |
| `> [!note] Titel` | Callouts — siehe unten |
| ` ```sprache … ``` ` | Codeblöcke mit Syntaxhervorhebung; `~~~` geht auch als Zaun |
| vier führende Leerzeichen | eingerückter Codeblock |
| `\| a \| b \|` + `\|---\|---\|` | GFM-Tabellen — siehe unten |
| `---`, `***`, `___` | Trennlinie |
| `---` … `---` am Dateianfang | YAML-Frontmatter — siehe unten |

## Inline-Elemente

| Syntax | Ergebnis |
|---|---|
| `*kursiv*`, `_kursiv_` | *kursiv* |
| `**fett**`, `__fett__` | **fett** |
| `***beides***` | Verschachtelung in jeder Kombination |
| `~~durchgestrichen~~` | durchgestrichen, mit echter Linie |
| `==markiert==` | markiert wie mit einem Textmarker — siehe [Markierungen](#markierungen) |
| `<u>unterstrichen</u>` | unterstrichen — Markdown hat dafür keine eigene Syntax |
| `` `Code` `` | Inline-Code in eigener Farbe |
| `[Text](url)`, `[Text](url "Titel")` | Link |
| `<https://example.com>` | Autolink |
| `https://example.com`, `www.example.com` | auch nackte URLs werden verlinkt |
| `![alt](bild.png)` | Bild — siehe unten |
| `[[Ziel]]`, `[[Ziel\|Alias]]` | Wikilink |
| `![[bild.png]]` | Bild-Embed |
| 🎉 Emoji | wird farbig dargestellt, nicht als schwarze Kontur |
| `<kbd>Strg</kbd>`, `<span class="…">` | einige HTML-Formatier-Tags — siehe [Inline-HTML](#inline-html) |

Die Auszeichnungen werden tolerant gelesen: ein unbalanciertes `**fett ohne Ende` bleibt einfacher Text, statt den Rest des Absatzes zu verschlucken.

## Markierungen

```markdown
Das ist ==wichtig== und das ist ==**sehr** wichtig==.
```

`==Text==` markiert wie in Obsidian — in jedem Dokument, nicht nur im Vault. Die Zeichen müssen am Text anliegen: in `a == b` bleiben die Gleichheitszeichen, was sie sind. Auszeichnungen innerhalb der Markierung wirken, und ein Link darin behält seine Linkfarbe. Läuft eine Markierung über einen Zeilenumbruch, setzt sie sich in der nächsten Zeile ohne Naht fort.

Ab Werk ist die Markierung hellgelb, im Dunkelmodus ein gedecktes Gelb; sie wird auch gedruckt und ins PDF übernommen. Per `user.css` lässt sie sich ändern — siehe [Markierungen, Tasten und eigene Klassen](css-customizing.de.md#markierungen-tasten-und-eigene-klassen).

## Inline-HTML

mdVü hat keine HTML-Engine, versteht im Text aber eine kurze Liste von Formatier-Tags:

| Tag | Ergebnis |
|---|---|
| `<u>…</u>` | unterstrichen |
| `<mark>…</mark>` | markiert, wie `==…==` |
| `<s>…</s>`, `<del>…</del>` | durchgestrichen, wie `~~…~~` |
| `<b>…</b>`, `<strong>…</strong>` | fett |
| `<i>…</i>`, `<em>…</em>` | kursiv |
| `<kbd>…</kbd>` | eine Taste: dicktengleich, mit hellem Rahmen |
| `<span class="name">…</span>` | ohne eigenes Aussehen — das gibt ihm `span.name { … }` in der `user.css` |

Markdown in diesen Tags wirkt weiter (`<u>*beides*</u>`). Groß- und Kleinschreibung spielt keine Rolle. Als Attribut zählt nur `class`; `style="…"` und alle anderen werden ignoriert. Ein Tag, das nie geschlossen wird, gilt bis zum Ende des Absatzes; ein schließendes Tag ohne öffnendes bleibt als Text sichtbar. Alle anderen Tags erscheinen als wörtlicher Text.

## Tabellen

```markdown
| Links | Mitte | Rechts |
|:------|:-----:|-------:|
| a     |   b   |      c |
```

- Die Ausrichtungszeile (`:---`, `:---:`, `---:`) wird beachtet, am Bildschirm wie im Druck.
- Eine Tabelle **braucht eine Kopfzeile**. Zeilen ohne gültige `|---|`-Trennzeile bleiben ein Absatz — so schreibt es GFM vor, und so wird aus einem versehentlichen senkrechten Strich im Fließtext keine Tabelle.
- Ausgefranste Zeilen werden toleriert: zu wenige Zellen werden aufgefüllt, überzählige verworfen, Maßstab ist die Spaltenzahl des Kopfes.
- Zellen tragen Inline-Auszeichnungen (fett, Code, Links), keine Blockelemente.
- Sehr breite Tabellen werden beim Drucken automatisch eingepasst — siehe [Handbuch](manual.de.md#drucken-und-pdf).

## Links und Sprungmarken

- **Relative Links** (`[Handbuch](manual.de.md)`) werden gegen den Ordner des aktuellen Dokuments aufgelöst und öffnen die Datei in mdVü.
- **Sprungmarken** (`[zum Abschnitt](#tabellen)`) springen innerhalb des Dokuments. Der Ankername wird aus der Überschrift gebildet: kleingeschrieben, Leerzeichen werden zu Bindestrichen, Binde- und Unterstriche bleiben, alles andere (Satzzeichen, Symbole) fällt weg. Aus `## Links und Sprungmarken` wird also `#links-und-sprungmarken`. Gleichnamige Überschriften werden durchnummeriert: `#notizen`, `#notizen-1`, `#notizen-2`. Das entspricht der Konvention von GitHub, derselbe Link funktioniert also meist an beiden Orten.
- **Sprungmarken in andere Dokumente** (`[Details](andere.md#installation)`) öffnen das Dokument und springen zur Überschrift. Hinter dem `#` darf der Ankername stehen (wie oben) oder der Text der Überschrift. Prozent-kodierte Links, wie Obsidian sie bei abgeschalteten Wikilinks schreibt (`[x](Meine%20Notiz.md#Mein%20Abschnitt)`), funktionieren ebenso. Zeigt der Link auf das schon offene Dokument, wird nur gesprungen. Fehlt der Abschnitt, öffnet sich das Dokument oben und die Statuszeile sagt Bescheid.
- **`http(s)`-Links** öffnen nach Rückfrage den Standardbrowser.
- Links auf alles Übrige werden abgelehnt statt befolgt. mdVü startet aus einem Dokument heraus niemals ein Programm oder einen Shell-Befehl.

Auch in sehr großen Dokumenten, die in Stücken geladen werden, finden Sprungmarken und die Gliederung ihr Ziel, selbst wenn es noch nicht geladen ist. Ein `#` im Dateinamen muss im Link als `%23` stehen — sonst gilt alles dahinter als Sprungmarke.

**Links auf fehlende Dateien** erscheinen blasser als andere Links, wie die nicht aufgelösten Links in Obsidian — bei relativen Links wie bei Wikilinks. Klickbar bleiben sie. Ein Link auf einen fehlenden *Abschnitt* einer vorhandenen Datei wird wie in Obsidian nicht markiert. Die Farbe kommt aus `a.unresolved` in Ihrer `user.css` — siehe [Selektoren](css-customizing.de.md#selektoren).

## Fundstellen verlinken

Ein Link auf `mdvu:open` öffnet ein Dokument und bringt dabei Markierungen oder eine Suche mit — gedacht für Notizen, Trefferlisten und Werkzeuge, die auf bestimmte Stellen in anderen Dateien zeigen wollen:

```
[Alle Rechnungen](mdvu:open?uri=C:/Notizen/plan.md&find=Rechnung)
[Der dritte Treffer, ganzes Wort](mdvu:open?uri=C:/Notizen/plan.md&find=Rechnung&word&hit=3)
[Zeilen 40–42 als Warnung](mdvu:open?uri=C:/src/README.md&mark=12:5-20&mark=40-42~warn)
[Markierung plus Abschnitt](mdvu:open?uri=C:/Notizen/plan.md&mark=7~ffcc00#Ziele)
```

`uri=` ist der vollständige Pfad der Datei mit `/` statt `\`; Leerzeichen und andere Sonderzeichen stehen prozent-kodiert (`%20`, `&` als `%26`). Solche Links funktionieren in Dokumenten — die Kommandozeile nimmt nur Dateien und Ordner.

**`find=` — alle Fundstellen markieren, wie die Suche.** mdVü sucht im ganzen Dokument, markiert alle Treffer und blendet den Suchstreifen mit dem Begriff ein; `F3` und `Umschalt+F3` gehen weiter, `Esc` räumt ab.

| Zusatz | Bedeutung |
|---|---|
| `&case` | Groß-/Kleinschreibung beachten |
| `&word` | nur ganze Wörter |
| `&regex` | Suchtext als regulären Ausdruck lesen (ohne Regex-Unterstützung im Programm wird nach dem Text gesucht; die Statuszeile sagt Bescheid) |
| `&hit=3` | der dritte Treffer ist der aktive (Vorgabe: der erste) |
| `find=TODO~todo` | Farbe der Markierung (siehe unten) |

**`mark=` — Zeilen oder Bereiche hervorheben**, beliebig oft. Die Angaben beziehen sich auf den **Quelltext** der Datei, so wie ihn ein Editor oder `grep` zeigt; Zeilen und Spalten zählen ab 1, das Ende ist ausschließlich:

| Angabe | Bereich |
|---|---|
| `12` | ganze Zeile 12 |
| `12-14` | Zeilen 12 bis 14 |
| `12:5-20` | Zeile 12, Spalte 5 bis vor Spalte 20 |
| `12:5-14:3` | von Zeile 12, Spalte 5 bis vor Zeile 14, Spalte 3 |
| `12:5` | nur Sprungziel, keine Markierung |

Markup, das nicht sichtbar ist (`**`, Link-Adressen, Kommentare), wird ausgespart. Bereiche hinter dem Dateiende entfallen; liegen alle dahinter, sagt die Statuszeile Bescheid. Höchstens 1000 `mark` je Link.

**Farben:** `~` und dahinter entweder eine Klasse — `warn`, `error`, `ok`, `info`, `find` — oder eine Farbe als sechs Hex-Ziffern **ohne** `#` (`~ffcc00`; das `#` leitete in einem Link schon den Abschnitt ein). Ohne Angabe nimmt `mark` Gelb und `find` die Farbe der Suche. Die Klassen sind Stilregeln im Dokument-CSS und lassen sich in der `user.css` umfärben oder ergänzen, z.B. `highlight.todo { background-color: #a0e0ff; }`.

**Wohin gesprungen wird:** zum Abschnitt hinter `#`, sonst zur ersten `mark`, sonst zum aktiven `find`-Treffer — markiert wird in jedem Fall alles. Beim Zurückblättern gewinnt die Stelle, an der man zuletzt war. `Esc` im Dokument räumt die Markierungen ab.

## Bilder

```markdown
![Alternativtext](img/screenshot.png)
![Alternativtext|620](img/screenshot.png)      Breite 620
![Alternativtext|620x400](img/screenshot.png)  Breite 620, Höhe 400
![[diagramm.svg]]                              Obsidian-Embed
```

- Formate: PNG, JPEG, GIF, BMP, TIFF und SVG, dazu `data:`-URIs.
- **Ein Bild muss ein eigener Absatz sein.** Ein Bild mitten im Fließtext (`siehe ![das](a.png) hier`) wird *nicht* dargestellt — es erscheint nur der Alternativtext. Also auf eine eigene Zeile setzen, mit Leerzeilen davor und dahinter.
- Mehrere Bilder in einem Absatz stehen nebeneinander; ein harter Zeilenumbruch dazwischen setzt sie untereinander. Ein Link um ein Bild funktioniert (`[![alt](bild.png)](ziel.md)`).
- Der Größenzusatz `|Breite` / `|BreitexHöhe` ist die Obsidian-Konvention. Bei reiner Breitenangabe folgt die Höhe proportional. Andere Markdown-Werkzeuge zeigen den Zusatz als Teil des Alternativtextes — harmlos, und der Grund, warum auch diese Doku ihn verwendet.
- Pfade werden relativ zum Dokument aufgelöst.
- **Bilder aus dem Internet werden nicht geladen** — mdVü hat überhaupt keinen Netzwerkzugriff. Eine `https://…`-Bildquelle bleibt Alternativtext.
- Unlesbare oder fehlende Dateien werden stillschweigend übersprungen, der Alternativtext bleibt stehen.

## Codeblöcke und Syntaxhervorhebung

Gefencete Blöcke werden hervorgehoben, sobald der Zaun eine Sprache nennt:

````markdown
```python
def antwort() -> int:
    return 42
```
````

Erkannte Namen (Aliase in der zweiten Spalte):

| Sprache | Bezeichner am Zaun |
|---|---|
| Pascal / Delphi | `pascal`, `delphi`, `pas`, `dpr` |
| C / C++ | `c`, `cpp`, `h`, `hpp`, `cc` |
| C# | `cs`, `csharp` |
| Java | `java` |
| JavaScript / TypeScript | `js`, `javascript`, `jsx`, `ts`, `typescript`, `tsx` |
| Python | `python`, `py` |
| Go | `go` |
| Rust | `rust`, `rs` |
| Kotlin / Swift / PHP | `kotlin`, `kt`, `swift`, `php` * |
| Lua | `lua` |
| Shell | `sh`, `bash`, `zsh`, `shell` |
| SQL | `sql`, `tsql`, `mysql`, `pgsql` |
| VB / VBScript | `vb`, `vbs`, `vbscript`, `basic` |
| CSS | `css` |
| Markdown | `markdown`, `md` |
| JSON | `json` |
| YAML | `yaml`, `yml` |
| INI / TOML | `ini`, `conf`, `cfg`, `toml`, `properties` |

\* Bei diesen dreien werden Kommentare, Zeichenketten und Zahlen hervorgehoben, Schlüsselwörter noch nicht.

Eine unbekannte Sprache ist kein Problem: Der Block bleibt einfach in der normalen Code-Farbe, statt falsch eingefärbt zu werden. Unterschieden werden Kommentare, Zeichenketten, Zahlen, Schlüsselwörter und Bezeichner — die Farben kommen aus dem Stylesheet und lassen sich also [ändern](css-customizing.de.md#code-hervorhebung).

[`samples/code-samples.de.md`](../samples/code-samples.de.md) zeigt die Hervorhebung für ein Dutzend Sprachen nebeneinander.

## Callouts

```markdown
> [!note] Gut zu wissen
> Callouts sind Zitate mit einem Typ.

> [!warning]
> Der Titel ist optional — der Typ allein genügt.
```

Callouts sehen aus wie in Obsidian: ein farbiger Kasten mit einer Titelzeile in der Farbe des Typs, hell wie dunkel. Der Titel darf Inline-Auszeichnungen enthalten; fehlt er, steht der Typname an seiner Stelle (`> [!warning]` → „Warning“, `> [!my-type]` → „My type“).

Die Farben sind Obsidians Standardfarben, eine je Gruppe — Obsidians Aliase teilen die Farbe ihrer Gruppe:

| Farbe | Typen (Aliase in Klammern) |
|---|---|
| blau | `note`, `info`, `todo` |
| cyan | `abstract` (`summary`, `tldr`), `tip` (`hint`, `important`) |
| grün | `success` (`check`, `done`) |
| orange | `question` (`help`, `faq`), `warning` (`caution`, `attention`) |
| rot | `failure` (`fail`, `missing`), `danger` (`error`), `bug` |
| lila | `example` |
| grau | `quote` (`cite`) |

Jeder andere Typname funktioniert ebenfalls und erscheint wie `note` — mdVü führt keine Liste erlaubter Typen. Wie man ihm ein eigenes Aussehen gibt oder einen eingebauten Typ umfärbt, steht unter [Callouts einfärben](css-customizing.de.md#callouts-einfärben).

Der Faltmarker (`> [!note]-`) wird gelesen, aber nicht umgesetzt; der Inhalt ist immer sichtbar.

## Wikilinks

```markdown
[[Andere Notiz]]                 Link auf eine Notiz (".md" darf fehlen)
[[Andere Notiz|siehe dort]]      mit Anzeigetext
[[Ordner/Andere Notiz]]          über den Ordner eingegrenzt
[[#Überschrift]]                 Sprung zu einer Überschrift im Dokument
[[Andere Notiz#Überschrift]]     Notiz öffnen und zur Überschrift springen
[[Notiz#Kapitel 2#Details]]      "Details" unter "Kapitel 2" (bei gleichen Titeln)
![[bild.png]]                    Bild einbetten
![[bild.png|200]]                ... 200 Pixel breit
```

**In einem Obsidian-Vault** (ein Ordner mit `.obsidian`) löst mdVü Wikilinks auf wie Obsidian: über den Namen, irgendwo im Vault, ohne Pfadangabe. Groß- und Kleinschreibung spielen keine Rolle. Tragen mehrere Dateien denselben Namen, gewinnt die im Ordner der aktuellen Notiz, danach die nächste zur Vault-Wurzel. `[[/Ordner/Notiz]]` beginnt an der Vault-Wurzel, `[[../Notiz]]` geht einen Ordner hinauf. Dateien im Papierkorb des Vaults (`.trash`) sind nie Linkziel. mdVü liest die Dateinamen des Vaults beim Öffnen der ersten Notiz daraus im Hintergrund ein und hält die Liste während der Arbeit aktuell — eine in Obsidian angelegte Notiz oder ein eingefügtes Bild wird sofort gefunden.

**Außerhalb eines Vaults** wird das Ziel neben dem aktuellen Dokument gesucht (ebenfalls mit oder ohne `.md`).

Ein nicht auflösbarer Link erscheint blasser als andere Links und zeigt beim Klick einen Hinweis in der Statuszeile. In einem Vault prüft mdVü die Links erneut, sobald die Dateinamen des Vaults gelesen sind, und wieder, wenn Sie in Obsidian eine Notiz anlegen oder löschen.

Der Abschnitt hinter dem `#` wird wie in Obsidian über den Text der Überschrift gefunden, Groß- und Kleinschreibung egal; bei gleichnamigen Überschriften gewinnt die erste, außer ein Pfad wie `#Kapitel 2#Details` grenzt ein. Fehlt der Abschnitt, öffnet sich die Notiz oben.

Noch nicht unterstützt: `![[notiz.md]]` — das Einbetten einer anderen *Notiz* — und Embeds von Nicht-Bildern (`![[datei.pdf]]`); beides erscheint als Text. Block-Verweise (`[[Notiz#^abc123]]`) öffnen die Notiz oben, ohne zum Absatz zu springen.

## Kommentare

```markdown
Sichtbar %%versteckt%% sichtbar
%%
Ein versteckter Block,
auch über Leerzeilen hinweg.
%%
```

Obsidian-Kommentare werden nie angezeigt — weder am Bildschirm noch in Druckvorschau, Druck oder PDF. Ein nicht geschlossener Kommentar verbirgt wie in Obsidian alles, was danach kommt. In Code (`` `%%x%%` `` und Code-Blöcken) wird nichts verborgen.

## Frontmatter

Ein durch `---` begrenzter YAML-Block ganz am Dateianfang wird als Frontmatter erkannt und als gedämpfter Monospace-Block angezeigt, samt der Zäune. Er wird bewusst *nicht* versteckt: In einem Viewer sind Metadaten Inhalt — Tags und Datum will man in der Regel sehen.

Er trägt ein eigenes Style-Tag; ausblenden ist deshalb eine Zweizeilen-Änderung in der `user.css`:

```css
frontmatter { display: none; }
```

## Was nicht unterstützt wird

| Nicht unterstützt | Was stattdessen passiert | Warum |
|---|---|---|
| HTML-Blöcke (`<div>…</div>`) | werden übersprungen, es erscheint nichts | es gibt keine HTML-Pipeline — mdVü rendert Markdown direkt |
| Übriges Inline-HTML (`<sup>x</sup>`, `<a href>`, `style="…"`) | erscheint als wörtlicher Text — verstanden werden nur die [Formatier-Tags](#inline-html) | derselbe Grund |
| Referenz-Links (`[Text][id]` plus Definitionsblock) | bleibt einfacher Text | erfordert einen zweiten Durchlauf über das Dokument |
| Fußnoten (`[^1]`) | bleibt einfacher Text | als Option vorgesehen, nicht umgesetzt |
| Definitionslisten | bleibt einfacher Text | in Notizen selten |
| Mathematik / LaTeX (`$…$`) | bleibt einfacher Text | bräuchte einen Formelsatz |
| Mermaid und andere Diagramm-Zäune | erscheint als Codeblock | Diagramme zu rendern ist Aufgabe eines anderen Programms |
| Notiz-Transklusion (`![[notiz]]`) | bleibt einfacher Text | nur Bild-Embeds werden aufgelöst |

Wer auf eines davon angewiesen ist: Die Quelltext-Ansicht (`Strg+2`) zeigt die Datei immer genau so, wie sie auf der Platte steht.

## Grenzen

Drei harte Grenzen schützen den Viewer vor pathologischen Dateien: 50 MB je Dokument, 200 Seiten für Druck/Vorschau/PDF und 100 KB je Absatz. Was beim Erreichen einer Grenze passiert, steht im [Handbuch](manual.de.md#grenzen).

---

*[Zurück zum README](../README.de.md)*
