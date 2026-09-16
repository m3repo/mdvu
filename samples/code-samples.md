# Code highlighting — showcase

*[Deutsche Version](code-samples.de.md)*

Every fenced code block below names its language (` ```pascal `, ` ```sql `, …).
Comments, strings, numbers (including hex), keywords and identifiers each get
their own style from the stylesheet. Unknown languages simply stay in the
plain code color — never wrongly colored.

## Pascal / Delphi

Named after Blaise Pascal, designed by Niklaus Wirth to teach clean
programming — then Delphi taught it to build real applications and pay
mortgages. Wirth also coined Wirth's law: software gets slower faster than
hardware gets faster.

```pascal
{ Calculates the Answer. Takes 7.5 million years, give or take. }
program DeepThought;
const
  TheAnswer = 42;             // decimal
  Mask      = $2A;            // the same, wearing hex
var
  Question: string;
begin
  Question := 'It''s 6 × 9, isn''t it?';
  if TheAnswer <> 54 then
    WriteLn('Don''t panic: ', TheAnswer);
end.
```

## C / C++

C was born at Bell Labs as a language for writing operating systems, and it
still trusts you completely — including with the loaded footgun. C++ added
classes, templates and forty years of committee meetings.

```c
/* A whale's first thoughts, briefly. */
#include <stdio.h>
#define GROUND 0x2A
int main(void) {
    double altitude = 1609.5;           // and falling
    const char *thought = "Hello, ground!\n";
    for (int i = 0; i < 3; i++)
        printf("%s", thought);
    return GROUND;                      /* graceful landing */
}
```

## Java

Write once, run anywhere — after downloading a runtime the size of a small
moon. Java was almost called Oak, after the tree outside James Gosling's
office window.

```java
// A perfectly normal factory for improbable things.
public class ImprobabilityFactory {
    private static final int ANSWER = 42;
    private static final double TEA_TEMP = 99.5;   // Celsius, ideally
    public static void main(String[] args) {
        String note = "Share and enjoy!";
        System.out.println(note + " 0x" + Integer.toHexString(ANSWER));
    }
}
```

## C#

Microsoft's answer to Java, designed by Anders Hejlsberg — the same mind
that gave the world Turbo Pascal and Delphi. It is a small universe after all.

```csharp
// Luggage tracking, sapient pearwood edition.
class Luggage {
    const int Legs = 100;               // approximately
    static void Main() {
        var owner = "Rincewind";
        double speed = 88.8;            // surprisingly fast for furniture
        System.Console.WriteLine($"{owner}, run! 0x{Legs:X} legs behind you");
    }
}
```

## JavaScript / TypeScript

Famously designed in ten days, JavaScript went on to run the entire visible
web. TypeScript adds types, so you can be wrong with confidence — at compile
time.

```js
// Mostly harmless.
const answer = 42;
let guide = { towel: true, panic: false };
async function research(entry) {
  const note = `Entry ${entry}: mostly harmless`;   // template string
  return note.length > 0x10 ? note : "stub";
}
```

## Go

Go was invented at Google, allegedly while waiting for a C++ build to
finish. Its mascot is a gopher; its error handling is a lifestyle.

```go
// Small, fast, and pathologically tidy.
package main

import "fmt"

func main() {
    const answer = 42
    temp := 99.5                        // gopher-approved tea temperature
    if err := fmt.Errorf("towel not found"); err != nil {
        fmt.Println("don't panic:", answer, temp)
    }
}
```

## Rust

Rust promises memory safety without garbage collection; in exchange you must
argue with the borrow checker until it is satisfied. It is always right,
which is the annoying part.

```rust
// The borrow checker giveth, and the borrow checker taketh away.
fn main() {
    let answer: u32 = 42;
    let hex = 0x2A;
    let advice = "Bring a towel. Obviously.";
    if answer == hex {
        println!("{} ({})", advice, answer as f64 / 2.0);
    }
}
```

## Python

Named after Monty Python, not the snake — the early docs were full of spam
and lumberjacks. Whitespace is syntax, which divides programmers into two
irreconcilable camps.

```python
# The kettle is watching.
def brew(cups: int = 2) -> str:
    """Brews proper tea. No replicated substitutes."""
    temperature = 99.5
    flags = 0b101010
    return f"{cups} cups at {temperature} degrees (flags={flags})"
```

## Shell

The shell is the oldest user interface still in daily use: a conversation
with your computer, one cryptic abbreviation at a time. The quoting rules
are the real final boss.

```bash
# Ask the computer nicely.
ANSWER=42
NAME='Deep Thought'
if [ "$ANSWER" -eq 42 ]; then
  echo "The answer is $ANSWER, says $NAME."   # confidence: high
fi
```

## SQL

SQL is fifty years old and still runs the world's money. You describe *what*
you want and the database decides *how* — a rare case of successful
delegation.

```sql
-- All improbable events, most improbable first.
select name, odds, 'it''s a million-to-one chance' as note
from events
where odds >= 1000000            /* Discworld rules: those always work */
order by odds desc;
```

## Lua

Lua means "moon" in Portuguese and comes from Rio de Janeiro. It is small
enough to embed anywhere — which is why half of all game mods speak it.

```lua
-- The Luggage's route planner.
local legs = 100
local speed = 12.5               -- km/h, straight through walls
local sign = [[OWNER: do not open]]
if legs > 0x10 then
  print(string.format("%d legs and closing. %s", legs, sign))
end
```

## VB / VBScript

BASIC taught a whole generation to program; VBScript then taught the same
generation to automate Windows at three in the morning. Nostalgia, with
`End If`.

```vbscript
' Counting to 42, the scenic route.
Dim total, label
total = 0
label = "So long, and thanks for " & "all the fish"
For i = 1 To 6
    total = total + 7
Next
If total = 42 Then MsgBox label
```

## INI / TOML

The INI file is the cockroach of configuration formats: declared obsolete
for thirty years, present in every second directory. TOML is its
well-groomed descendant.

```ini
; Heart of Gold — main configuration
[drive]
type = "infinite-improbability"
factor = 42
brownian_source = "a nice hot cup of tea"   # motion generator
```

## YAML

YAML Ain't Markup Language: significant whitespace and surprising type
rules — in old YAML, `no` means false, which is known as the Norway
problem. Indent with care.

```yaml
# Guide entry, structured.
entry: Earth
status: "mostly harmless"
edition: 42
coordinates: [54.3, -1.5]
remastered: true              # after the Vogons
```

## JSON

JSON was "discovered, not invented", says Douglas Crockford — it was hiding
inside JavaScript all along. It has exactly one way to do things and no
comments. Ever.

```json
{
  "ship": "Heart of Gold",
  "improbability": 42,
  "temperature": 99.5,
  "towels": true,
  "crew": ["Zaphod", "Trillian", "Marvin"]
}
```

## CSS

CSS is the art of moving a box three pixels to the left for six hours.
This one is highlighted by the SynEdit backend, which has strong opinions
about selectors.

```css
/* Paint the town green, tastefully. */
.guide-entry {
  color: #2a6f2a;
  margin: 4px 8px;
  content: "Don't panic";
}
```

## Markdown

Yes — this page highlights Markdown inside Markdown. The turtles go all the
way down.

```markdown
# Guide
**Mostly** *harmless* — see [entry 42](earth.md).
- towel: packed
```

---

Everything else — random notes, Klingon, your homemade DSL — renders in the
plain code color:

```whatever
++++++++[>++++++++<-]>+.   (this is fine)
```
