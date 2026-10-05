---
titel: Alles, was mdVü darstellt
autor: m3Works
tags: [demo, markdown, referenz]
---

# Schaufenster

*[English version](showcase.md)*

Diese Datei verwendet jedes Markdown-Element, das mdVü versteht — in mdVü geöffnet, zeigt sie den vollen Umfang des Renderers in einem Durchlauf. Der Block oben ist **Frontmatter**: Metadaten am Dateianfang, die als gedämpfter Monospace-Block erscheinen statt versteckt zu werden. Die vollständige Referenz steht in [Markdown-Unterstützung](../docs/markdown-support.de.md).

## Überschriften

Die Überschrift oben ist Ebene 1. Darunter folgen die übrigen — sie bilden zugleich den Gliederungsbaum links, dieser Abschnitt eignet sich also gut zum Herumklicken darin.

### Ebene 3

#### Ebene 4

##### Ebene 5

###### Ebene 6

Setext-Überschriften gehen auch
===============================

Und die zweite Sorte
--------------------

## Text

Gewöhnliche Absätze sind einfach Text. Eine Leerzeile beginnt einen neuen.

Dieser Absatz zeigt die Inline-Auszeichnungen: *kursiv*, **fett**, ***beides zugleich***, `Inline-Code`, ~~durchgestrichen~~ und ein [Link auf das Handbuch](../docs/manual.de.md). Unbalancierte Auszeichnung wie **diese hier ist unproblematisch — sie bleibt wörtlicher Text, statt den Rest des Absatzes zu verschlucken.

Markierungen wirken wie in Obsidian: ==eine markierte Stelle==, ==mit **Fettem** und einem [Link](../README.de.md) darin== und eine längere Markierung, die ruhig über das Zeilenende laufen darf, damit man sieht, dass sie in der nächsten Zeile ohne Naht weitergeht. Ein Vergleich wie a == b bleibt, wie er ist. Wo Markdown keine Syntax hat, helfen einige HTML-Tags: <u>unterstrichen</u>, <mark>markiert</mark>, <kbd>Strg</kbd>+<kbd>F</kbd>.

Ein harter Zeilenumbruch sind zwei Leerzeichen am Zeilenende —  
es geht hier weiter, im selben Absatz. Ein Backslash am Ende tut dasselbe.\
So wie hier.

Emoji erscheinen farbig: 🎉 🚀 📄 ✅ — auch die, die Windows aus einer Farbschrift zeichnet.

## Listen

- Eine Aufzählung
- mit einem zweiten Punkt
  - und einem verschachtelten
    - und einer Ebene tiefer
- zurück auf der obersten Ebene

1. Eine nummerierte Liste
2. Zweitens
3. Drittens
   1. Verschachtelt, eigene Zählung
   2. Zweiter verschachtelter Punkt

Listen dürfen bei jeder Zahl beginnen:

7. Sieben
8. Acht
9. Neun

Aufgabenlisten:

- [x] Beispieldatei schreiben
- [x] Jedes Element unterbringen
- [ ] Jemanden zum Lesen überreden
- [ ] Die Weltherrschaft an mich reißen

## Zitate und Callouts

> Ein einfaches Blockzitat.
> Es darf über mehrere Zeilen gehen und trägt **Inline-Auszeichnungen** wie ein Absatz.

> Zitate verschachteln sich:
> > und das innere wird weiter eingerückt.

Callouts sind Zitate mit einem Typ. Sie bekommen Obsidians Farben und eine Titelzeile — [umgestalten](../docs/css-customizing.de.md#callouts-einfärben) lassen sie sich in der eigenen `user.css`:

> [!note] Gut zu wissen
> Der Titel hinter dem Typ ist optional.

> [!warning]
> Ohne Titel wird der Typname zum Titel.

> [!tip] Jeder Name funktioniert
> mdVü führt keine Liste erlaubter Typen — `[!spoiler]`, `[!rezept]` und `[!bananen]` sind alle in Ordnung; unbekannte sehen aus wie `note`.

## Code

Inline-Code sieht so aus: `hier`. Gefencete Blöcke werden hervorgehoben, sobald der Zaun eine Sprache nennt:

```python
def fibonacci(n: int) -> int:
    """Der Klassiker, mit Kommentar und Zeichenkette."""
    a, b = 0, 1              # zwei Zahlen
    for _ in range(n):
        a, b = b, a + b
    return a
```

```sql
select kunden_id, sum(betrag) as umsatz
from bestellungen
where bestelldatum >= '2026-01-01'   -- Kommentar
group by kunden_id
having sum(betrag) > 1000;
```

```json
{
  "name": "mdVü",
  "version": "0.7.0",
  "netzwerk": false,
  "grenzen": { "ladeMB": 50, "seiten": 200 }
}
```

Eine unbekannte Sprache bleibt in der normalen Code-Farbe, statt falsch eingefärbt zu werden:

```klingonisch
Qapla'!  (das ist in Ordnung)
```

Eingerückte Codeblöcke funktionieren ebenfalls — vier Leerzeichen:

    schlichter eingerückter Code
    keine Sprache, keine Hervorhebung

[`code-samples.de.md`](code-samples.de.md) zeigt ein Dutzend Sprachen hintereinander.

## Tabellen

| Sprache | Erschienen | Noch im Einsatz |
|:--------|-----------:|:---------------:|
| Pascal  |       1970 |        ja       |
| C       |       1972 |        ja       |
| Perl    |       1987 | ==kommt drauf an== |

Die Ausrichtungszeile entscheidet über die Spalten: links, rechts, zentriert. Zellen tragen Inline-Auszeichnungen — **fett**, `Code`, [Links](../README.de.md) — aber keine Blockelemente.

| Ausgefranste Eingabe | wird toleriert |
|---|---|
| fehlende Zellen werden aufgefüllt |
| überzählige | werden | verworfen |

## Trennlinien

Drei Schreibweisen für dieselbe Linie:

---

***

___

## Bilder

![Drei Formen|320](img/sample-shapes.svg)

Der Größenzusatz `|320` setzt die Breite, die Höhe folgt proportional. Zwei Bilder in einem Absatz stehen nebeneinander:

![|100](img/sample-shapes.svg) ![|100](img/sample-shapes.svg)

Ein Bild muss ein eigener Absatz sein — eines mitten im Satz wie ![dieses](img/sample-shapes.svg) zeigt nichts als seinen Alternativtext.

Eine fehlende Datei hinterlässt ihren Alternativtext:

![dieses Bild gibt es nicht](img/nope.png)

## Links

- Relativ auf eine andere Datei: [das Handbuch](../docs/manual.de.md)
- Auf eine Überschrift in diesem Dokument: [zurück nach oben](#schaufenster)
- Auf eine Überschrift in einer anderen Datei: [CSS-Einheiten](../docs/css-customizing.de.md#einheiten)
- Ein Autolink: <https://example.com>
- Eine nackte URL: https://example.com
- Wikilink-Schreibweise: [[code-samples.de.md]] und [[code-samples.de.md|mit Anzeigetext]]

Externe Links fragen nach, bevor der Browser aufgeht. Man beachte das `.md` in den Wikilinks: mdVü nimmt das Ziel wörtlich, statt den Ordner nach einer passenden Notiz zu durchsuchen — [[code-samples]] erscheint als Link, führt aber ins Leere.

## Diagramme

Kreis-, Balken-/Linien- und Sequenzdiagramme aus Mermaid-Codeblöcken — eine abgespeckte Teilmenge, gezeichnet von mdVü selbst:

```mermaid
pie showData
    title Wohin die Zeit geht
    "Lesen" : 45
    "Schreiben" : 30
    "Suchen" : 15
    "Besprechungen" : 10
```

```mermaid
xychart-beta
    title Notizen je Monat
    x-axis [Jan, Feb, Mär, Apr, Mai, Jun]
    y-axis "Notizen"
    bar "Geschrieben" [12, 18, 15, 22, 27, 24]
    line "Gelesen" [30, 34, 29, 41, 45, 50]
```

```mermaid
xychart-beta horizontal
    title Saldo je Region
    x-axis [Nord, Süd, West, Ost]
    bar [12.5, -4, 7, 3]
```

```mermaid
sequenceDiagram
    actor L as Leser
    participant V as mdVü
    participant P as Platte
    L->>+V: öffne notiz.md
    V->>P: Datei lesen
    P-->>V: Markdown
    V-->>-L: gerenderte Seite
    loop bei jedem Speichern
        P-)V: Datei geändert
        V->>V: neu laden, Position halten
    end
```

## Was absichtlich nichts tut

Manches wird als einfacher Text gezeigt statt gerendert — das ist der ehrliche Teil dieses Beispiels:

Übriges HTML bleibt wörtlich: <sup>nicht hochgestellt</sup>, und ein `style`-Attribut wird ignoriert: <span style="color:red">nicht rot</span>.

Eine Fußnoten-Referenz[^1] ist wörtlicher Text.

[^1]: …und ihre Definition ebenso.

Ein Referenz-Link [wie dieser][ref] bleibt so stehen, wie er geschrieben ist.

[ref]: https://example.com

Mathematik bleibt Text: $E = mc^2$.

Andere Mermaid-Diagrammarten erscheinen als Codeblock:

```mermaid
flowchart LR
  A[Markdown] --> B[Layout-Baum] --> C[Bildschirm]
```

---

*Teil der mdVü-Beispieldateien · MIT-lizenziert · [zurück zum README](../README.de.md)*
