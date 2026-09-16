# Darstellung anpassen per CSS

*[English version](css-customizing.md)*

mdVü stellt Dokumente mit einem kleinen, eingebauten Stylesheet dar. `Strg+4` öffnet das **eigene** Stylesheet, das darüber gelegt wird — für Schriftart, Farben, Abstände und die Code-Hervorhebung. Die Datei heißt `user.css`, liegt im Einstellungsordner (`%APPDATA%\m3Works\mdVu`) und bleibt über Updates hinweg erhalten.

Diese Seite ist die Referenz: wie die Kaskade arbeitet, welche Selektoren und Eigenschaften es gibt und wo die Fallstricke liegen.

> **Die Kurzfassung:** die `@import`-Zeile oben stehen lassen, eigene Regeln darunter schreiben, Größen in `pt` angeben und zum Ansehen zurück auf die Markdown-Ansicht (`Strg+1`) schalten.

Ein vollständiger, kommentierter Ausgangspunkt liegt unter [`samples/example-user.css`](../samples/example-user.css).

## Die Kaskade

Das eigene Stylesheet ist nicht das einzige. mdVü setzt das Blatt für jedes Dokument so zusammen:

1. **Ein minimaler Rückfall** — nur Schriften, keine Farben. Immer vorhanden.
2. **`builtin:default.css`** — das eingebaute Design, *nur* wenn die untenstehende `@import`-Zeile in der `user.css` steht (oder die `user.css` leer ist).
3. **`builtin:default-dark.css`** im Dunkelmodus bzw. **`builtin:print.css`** für Druck, Vorschau und PDF.
4. **Die eigene `user.css`** — zuletzt, und damit Gewinner bei gleicher Spezifität.

Der Schalter für Schritt 2 ist diese Zeile, mit der eine frische `user.css` vorbelegt ist:

```css
@import "builtin:default.css";
```

Bleibt sie stehen, legen sich die eigenen Regeln über das eingebaute Design. Wird sie aus einer nicht-leeren `user.css` entfernt, gibt es weder das Standard-Blatt noch sein dunkles Gegenstück — eine leere Leinwand, was genau richtig ist, wenn man von Null gestaltet, und genau falsch, wenn man nur die Schrift vergrößern wollte.

Zwei Folgerungen, die man kennen sollte:

- **Es gibt kein eigenes Stylesheet für den Dunkelmodus.** Die `user.css` gilt hell *und* dunkel. Wer für Absätze hart `color: #202020` setzt, bekommt beim Umschalten dunkelgrauen Text auf dunklem Grund. Besser: nur setzen, was wirklich nötig ist, und die Farben dem eingebauten Dunkel-Blatt überlassen.
- **Die eigenen Regeln gelten auch für Druck und PDF.** Das Druck-Stylesheet steht in der Kaskade *vor* dem eigenen und verliert deshalb dagegen. Eine farbige Überschrift in der `user.css` druckt also farbig. Ein `@media print` gibt es nicht — wer auf Papier etwas anderes will, kann das derzeit nicht in einer Datei ausdrücken.

## Selektoren

Jedes Blockelement im Dokument trägt ein Style-Tag; das sind die Selektoren.

| Selektor | Gilt für |
|---|---|
| `body` | die Dokumentfläche — Hintergrundfarbe und vererbte Grundschrift |
| `frame` | den äußeren Rahmen um den Seitenbereich (folgt `body`, wenn nicht gesetzt) |
| `p` | Absätze |
| `h1` … `h6` | Überschriften |
| `a` | Links (nur Farbe) |
| `code` | Inline-Code *und* die Grundfarbe von Codeblöcken |
| `pre` | den Kasten um einen Codeblock |
| `blockquote` | Blockzitate und Callouts |
| `frontmatter` | den YAML-Block am Dateianfang |
| `table`, `tr`, `th`, `td` | Tabellen, Zeilen, Kopfzellen, Datenzellen |
| `ul`, `ol`, `li` | Listen und Listenpunkte |
| `hr` | Trennlinien |
| `img` | Bilder |

Was darüber hinaus funktioniert:

```css
.klasse { … }              /* eine Style-Klasse, z.B. .code-comment */
blockquote.warning { … }   /* Tag plus Klasse — hier landen die Callouts */
* { … }                    /* alles */
tr:nth-child(2n+3) { … }   /* nth-child, zählt ALLE Kinder */
```

Was **nicht** funktioniert — die Regel wird ignoriert, ohne Fehlermeldung:

- Kombinatoren `>`, `+`, `~` sowie Nachfahren-Ketten über mehr als eine Ebene
- Pseudo-Elemente (`::before`, `::after`), Attribut-Selektoren (`[href]`)
- `!important` — den Vorrang regeln Spezifität und bei Gleichstand die Quellreihenfolge (die eigene Datei kommt zuletzt, gewinnt also ohnehin)
- `@media`-Abfragen jeder Art

Spezifität: ein Tag zählt 1, eine Klasse 10. Bei Gleichstand gewinnt die spätere Regel.

## Eigenschaften

### Text (wird vererbt)

| Eigenschaft | Werte |
|---|---|
| `font-family` | eine Rückfall-Liste: `'Lora', Georgia` — die erste **installierte** Familie gewinnt |
| `font-size` | `12pt`, `16px` — **`pt` bevorzugen**, siehe [Einheiten](#einheiten) |
| `font-weight` | `bold`, `normal` oder eine Zahl (ab 600 gilt als fett) |
| `font-style` | `italic`, `normal` |
| `line-height` | `normal`, eine **Zahl** wie `1.4` (empfohlen) oder eine Länge |
| `color` | jede Farbe, siehe unten |
| `text-align` | `left`, `right`, `center`, `justify` (fällt derzeit auf links zurück) |

### Kasten (wird nicht vererbt)

| Eigenschaft | Anmerkung |
|---|---|
| `background-color` | `background` wird als Kurzform für die Farbe akzeptiert |
| `padding`, `margin` | 1–4 Längen. **Margins addieren sich zum `gap` des Containers** — kein Collapsing |
| `border` | Kurzform: `1px solid #888`; Stile `solid dashed dotted double none` |
| `border-width`, `-color`, `-style`, `-radius` | auch je Seite oder Ecke (`border-top`, `border-top-left-radius`) |
| `width`, `height` | absolute Länge oder `auto`; **Border-Box** — Rahmen und Innenabstand gehen vom Inhalt ab |
| `min-width`, `max-width`, `min-height`, `max-height` | absolute Längen |
| `gap`, `row-gap`, `column-gap` | Abstand zwischen den Kindern eines Containers |
| `justify-content` | `start`, `center`, `end`, `space-between`, `space-around` |
| `align-self` | `start`, `center`, `end` — ein `align-items` gibt es **nicht** |
| `overflow` | `visible`, `hidden`, `clip` (die Engine scrollt nicht innerhalb von Kästen) |
| `vertical-align` | `top`, `middle`, `bottom` |
| `line-clamp` | `N` — höchstens N Zeilen, Abschluss „…“ |
| `display` | `none` blendet ein Element vollständig aus, alles andere zeigt es |

**Farben:** Hex (`#fff`, `#ffffff`), CSS-Namen (`rebeccapurple`), `rgb()` / `rgba()` und `transparent`.

## Einheiten

Das ist die eine Sache, die man sich merken sollte:

| Funktioniert | Funktioniert nicht |
|---|---|
| `px` (96-dpi-Referenzpixel), `pt`, `mm`, `cm`, `in` | `em`, `rem`, `%`, `vw`, `vh`, `ch` |

Relative Einheiten lassen sich nicht auflösen, die ganze Deklaration fällt weg. `font-size: 1.2em` vergrößert die Schrift also nicht — es passiert schlicht nichts.

Für Schriftgrößen `pt` verwenden. Punktgrößen skalieren korrekt mit der Bildschirm-DPI, dasselbe Dokument sieht damit auf einem 4K-Notebook so aus wie auf einem 1080p-Monitor. Ausnahme ist `line-height`: dort eine reine Zahl (`1.45`) angeben — sie wirkt als Faktor und verhält sich wie erwartet.

## Beispiele

### Eine andere Leseschrift

```css
body, p, li, td {
  font-family: 'Georgia', 'Times New Roman';
  font-size: 12pt;
  line-height: 1.5;
}
```

Schriftgröße und -art werden vererbt, aber Überschriften und Code tragen eigene Regeln aus dem Standard-Blatt und bleiben deshalb, wie sie sind, solange man sie nicht ebenfalls ändert.

### Ruhigere Überschriften

```css
h1 {
  font-size: 20pt;
  border-top: none;
  border-bottom: 1pt solid #d0d0d0;
  padding: 0 0 4px 0;
}
h2 { border-left: none; font-size: 15pt; }
```

### Code-Hervorhebung

Die Token-Farben kommen aus sechs Klassen. Sie zu überschreiben ist der sauberste Weg zu einem eigenen Code-Design:

```css
.code-comment { color: #6a737d; font-style: italic; }
.code-string  { color: #032f62; }
.code-number  { color: #005cc5; }
.code-keyword { color: #d73a49; font-weight: bold; }
.code-ident   { color: #24292e; }
.code-plain   { color: #24292e; }
pre { background-color: #f6f8fa; padding: 8px; }
```

Je Token werden nur `color`, `font-weight` und `font-style` ausgewertet — ein Hintergrund gehört an `pre`, nicht an eine Token-Klasse.

### Callouts einfärben

Der Callout-Typ kommt als Klasse am Blockzitat an, jeder Typ kann also anders aussehen:

```css
blockquote.note    { background-color: #eaf2fb; border-left: 3pt solid #4a80c0; }
blockquote.warning { background-color: #fdf0e6; border-left: 3pt solid #d08030; }
blockquote.tip     { background-color: #eaf7ee; border-left: 3pt solid #3d9a5c; }
```

Der Typname ist das, was in `> [!name]` steht — mdVü führt keine Liste erlaubter Namen.

### Frontmatter ausblenden

```css
frontmatter { display: none; }
```

### Zebrastreifen in Tabellen

Zeilenindex 1 ist die Kopfzeile, die Datenzeilen sind also die ungeraden Indizes ab 3:

```css
tr:nth-child(2n+3) { background-color: #f2f6fa; }
th { background-color: #dde5ee; }
```

### Engere Abstände

```css
body { gap: 4px; }        /* Abstand zwischen Blöcken */
ul, ol { row-gap: 2px; }  /* Abstand zwischen Listenpunkten */
```

Zur Erinnerung: Margins addieren sich zum Gap, statt mit ihm zu verschmelzen. Wer CSS aus dem Browser übernimmt, zieht den Gap von seinen Margins ab oder setzt `row-gap` ausdrücklich.

## Warum greift meine Regel nicht — eine Checkliste

1. **Steht die `@import`-Zeile noch da?** Ohne sie — und bei nicht-leerer `user.css` — ist das komplette Standard-Design weg. Das sieht meist nach „alles kaputt“ aus, nicht nach „eine Regel fehlt“.
2. **Eine relative Einheit?** `em`, `%`, `rem` fallen stillschweigend weg. `pt` oder `px` verwenden.
3. **Ein Selektor, den das Dokument gar nicht erzeugt?** Es gibt kein `strong`, `em`, `span` oder `div` — Inline-Auszeichnungen werden innerhalb eines Textlaufs gerendert, nicht als eigenes Element. Fett und kursiv lassen sich deshalb nicht getrennt gestalten.
4. **Ein Kombinator?** `blockquote > p` wird ignoriert. Eine Nachfahren-Ebene (`blockquote p`) ist das Maximum.
5. **`!important`?** Nicht unterstützt — und nicht nötig, weil das eigene Blatt ohnehin zuletzt kommt.
6. **Zurück auf die Markdown-Ansicht geschaltet?** Das Stylesheet wird beim Verlassen der CSS-Ansicht angewandt (`Strg+1`).
7. **Dunkelmodus an?** Das Dunkel-Blatt wird *vor* dem eigenen geladen, die eigenen Regeln gewinnen also — aber eine nur für hell gedachte Farbe gilt eben auch im Dunkelmodus.

## Wo die Datei liegt

`%APPDATA%\m3Works\mdVu\user.css`

Die CSS-Ansicht schreibt sofort durch, ein externer Editor sieht die Änderungen also unmittelbar. Umgekehrt — die Datei von außen bearbeiten, während mdVü läuft — vorher das Programm schließen, sonst überschreibt die laufende Instanz die Änderungen.

---

*[Zurück zum README](../README.de.md)*
