# Code-Highlighting — Schaufenster

*[English version](code-samples.md)*

Jeder Codeblock unten nennt seine Sprache (` ```pascal `, ` ```sql `, …).
Kommentare, Strings, Zahlen (inklusive Hex), Keywords und Bezeichner bekommen
ihren Stil aus dem Stylesheet. Unbekannte Sprachen bleiben schlicht in der
Code-Grundfarbe — niemals falsch bunt.

## Pascal / Delphi

Benannt nach Blaise Pascal, entworfen von Niklaus Wirth, um sauberes
Programmieren zu lehren — mit Delphi hat es dann echte Anwendungen gebaut
und Hypotheken abbezahlt. Von Wirth stammt auch Wirths Gesetz: Software wird
schneller langsamer, als Hardware schneller wird.

```pascal
{ Berechnet die Antwort. Dauert 7,5 Millionen Jahre, plusminus. }
program DeepThought;
const
  TheAnswer = 42;             // dezimal
  Mask      = $2A;            // dasselbe, in Hex verkleidet
var
  Question: string;
begin
  Question := 'It''s 6 × 9, isn''t it?';
  if TheAnswer <> 54 then
    WriteLn('Keine Panik: ', TheAnswer);
end.
```

## C / C++

C entstand in den Bell Labs als Sprache zum Schreiben von Betriebssystemen —
und vertraut einem bis heute bedingungslos, auch mit der geladenen Fußkanone.
C++ ergänzte Klassen, Templates und vierzig Jahre Gremiensitzungen.

```c
/* Die ersten Gedanken eines Wals, in Kürze. */
#include <stdio.h>
#define GROUND 0x2A
int main(void) {
    double altitude = 1609.5;           // und fallend
    const char *thought = "Hallo, Boden!\n";
    for (int i = 0; i < 3; i++)
        printf("%s", thought);
    return GROUND;                      /* elegante Landung */
}
```

## Java

Write once, run anywhere — nachdem man eine Laufzeitumgebung von der Größe
eines kleinen Mondes geladen hat. Java hieß beinahe „Oak", nach dem Baum vor
James Goslings Bürofenster.

```java
// Eine völlig normale Fabrik für unwahrscheinliche Dinge.
public class ImprobabilityFactory {
    private static final int ANSWER = 42;
    private static final double TEA_TEMP = 99.5;   // Celsius, idealerweise
    public static void main(String[] args) {
        String note = "Share and enjoy!";
        System.out.println(note + " 0x" + Integer.toHexString(ANSWER));
    }
}
```

## C#

Microsofts Antwort auf Java, entworfen von Anders Hejlsberg — demselben
Kopf, der der Welt Turbo Pascal und Delphi geschenkt hat. Das Universum ist
klein.

```csharp
// Gepäckverfolgung, Ausführung in empfindungsfähigem Birnbaumholz.
class Luggage {
    const int Legs = 100;               // ungefähr
    static void Main() {
        var owner = "Rincewind";
        double speed = 88.8;            // erstaunlich flott für ein Möbelstück
        System.Console.WriteLine($"{owner}, lauf! 0x{Legs:X} Beine hinter dir");
    }
}
```

## JavaScript / TypeScript

Berühmt dafür, in zehn Tagen entworfen worden zu sein — und betreibt heute
das gesamte sichtbare Web. TypeScript ergänzt Typen: Man kann mit voller
Zuversicht falsch liegen, schon zur Compile-Zeit.

```js
// Größtenteils harmlos.
const answer = 42;
let guide = { towel: true, panic: false };
async function research(entry) {
  const note = `Eintrag ${entry}: größtenteils harmlos`;   // Template-String
  return note.length > 0x10 ? note : "stub";
}
```

## Go

Go wurde bei Google erfunden — angeblich, während man auf das Ende eines
C++-Builds wartete. Das Maskottchen ist ein Gopher, die Fehlerbehandlung
eine Lebenseinstellung.

```go
// Klein, schnell und pathologisch ordentlich.
package main

import "fmt"

func main() {
    const answer = 42
    temp := 99.5                        // gopher-geprüfte Teetemperatur
    if err := fmt.Errorf("Handtuch nicht gefunden"); err != nil {
        fmt.Println("keine Panik:", answer, temp)
    }
}
```

## Rust

Rust verspricht Speichersicherheit ohne Garbage Collection; im Gegenzug
diskutiert man mit dem Borrow-Checker, bis er zufrieden ist. Er hat immer
recht — das ist das Ärgerliche daran.

```rust
// Der Borrow-Checker gibt, der Borrow-Checker nimmt.
fn main() {
    let answer: u32 = 42;
    let hex = 0x2A;
    let advice = "Handtuch einpacken. Offensichtlich.";
    if answer == hex {
        println!("{} ({})", advice, answer as f64 / 2.0);
    }
}
```

## Python

Benannt nach Monty Python, nicht nach der Schlange — die frühen Dokus waren
voller Spam und Holzfäller. Whitespace ist Syntax; das teilt die
Programmierer in zwei unversöhnliche Lager.

```python
# Der Wasserkocher beobachtet dich.
def brew(cups: int = 2) -> str:
    """Kocht richtigen Tee. Keine replizierten Ersatzstoffe."""
    temperature = 99.5
    flags = 0b101010
    return f"{cups} Tassen bei {temperature} Grad (flags={flags})"
```

## Shell

Die Shell ist die älteste Benutzeroberfläche im Dauereinsatz: ein Gespräch
mit dem Rechner, eine kryptische Abkürzung nach der anderen. Der Endgegner
sind die Quoting-Regeln.

```bash
# Den Computer höflich fragen.
ANSWER=42
NAME='Deep Thought'
if [ "$ANSWER" -eq 42 ]; then
  echo "Die Antwort lautet $ANSWER, sagt $NAME."   # Zuversicht: hoch
fi
```

## SQL

SQL ist fünfzig Jahre alt und verwaltet immer noch das Geld der Welt. Man
beschreibt, *was* man will, die Datenbank entscheidet, *wie* — ein seltener
Fall gelungener Delegation.

```sql
-- Alle unwahrscheinlichen Ereignisse, die unwahrscheinlichsten zuerst.
select name, odds, 'eine Chance von eins zu einer Million' as note
from events
where odds >= 1000000            /* Scheibenwelt-Regel: genau die klappen */
order by odds desc;
```

## Lua

Lua heißt auf Portugiesisch „Mond" und stammt aus Rio de Janeiro. Es ist
klein genug, um überall eingebettet zu werden — weshalb die Hälfte aller
Spiele-Mods es spricht.

```lua
-- Der Routenplaner der Truhe.
local legs = 100
local speed = 12.5               -- km/h, geradewegs durch Wände
local sign = [[BESITZER: nicht öffnen]]
if legs > 0x10 then
  print(string.format("%d Beine, kommt näher. %s", legs, sign))
end
```

## VB / VBScript

BASIC hat einer ganzen Generation das Programmieren beigebracht; VBScript
hat derselben Generation beigebracht, Windows um drei Uhr nachts zu
automatisieren. Nostalgie, mit `End If`.

```vbscript
' Bis 42 zählen, die Panoramastrecke.
Dim total, label
total = 0
label = "Macht's gut und danke " & "für den Fisch"
For i = 1 To 6
    total = total + 7
Next
If total = 42 Then MsgBox label
```

## INI / TOML

Die INI-Datei ist die Kakerlake unter den Konfigurationsformaten: seit
dreißig Jahren für tot erklärt, in jedem zweiten Verzeichnis präsent. TOML
ist ihr gepflegter Nachfahre.

```ini
; Herz aus Gold — Hauptkonfiguration
[drive]
type = "infinite-improbability"
factor = 42
brownian_source = "eine schöne heiße Tasse Tee"   # Bewegungsquelle
```

## YAML

YAML Ain't Markup Language: bedeutsamer Whitespace und überraschende
Typregeln — im alten YAML bedeutet `no` „falsch", bekannt als das
Norwegen-Problem. Mit Bedacht einrücken.

```yaml
# Reiseführer-Eintrag, strukturiert.
entry: Erde
status: "größtenteils harmlos"
edition: 42
coordinates: [54.3, -1.5]
remastered: true              # nach den Vogonen
```

## JSON

JSON wurde laut Douglas Crockford „entdeckt, nicht erfunden" — es steckte
die ganze Zeit in JavaScript. Es gibt genau einen Weg, Dinge zu tun, und
keine Kommentare. Niemals.

```json
{
  "ship": "Herz aus Gold",
  "improbability": 42,
  "temperature": 99.5,
  "towels": true,
  "crew": ["Zaphod", "Trillian", "Marvin"]
}
```

## CSS

CSS ist die Kunst, sechs Stunden lang eine Box drei Pixel nach links zu
schieben. Diesen Block färbt das SynEdit-Backend, das feste Ansichten über
Selektoren hat.

```css
/* Die Stadt grün anmalen, geschmackvoll. */
.guide-entry {
  color: #2a6f2a;
  margin: 4px 8px;
  content: "Keine Panik";
}
```

## Markdown

Ja — diese Seite highlightet Markdown innerhalb von Markdown. Die
Schildkröten reichen bis ganz nach unten.

```markdown
# Reiseführer
**Größtenteils** *harmlos* — siehe [Eintrag 42](erde.md).
- Handtuch: eingepackt
```

---

Alles andere — Notizen, Klingonisch, die selbstgebaute DSL — erscheint in
der Code-Grundfarbe:

```irgendwas
++++++++[>++++++++<-]>+.   (alles in Ordnung)
```
