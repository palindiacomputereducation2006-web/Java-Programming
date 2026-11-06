# Strings – `String.ijnb`

This notebook shows how to **work with text** in Java. A `String` is a sequence of characters, like a name or a sentence. It starts with your own examples (one method per cell), then covers the rest of the `String` methods you will use most, grouped by what they do, and ends with **`StringBuilder`**, the mutable way to build text. Each method has its own cell, so you can run one at a time and see what it does.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## How the notebook is organised

The notebook is grouped by topic. Each group starts with a **text cell that lists its properties or methods**, followed by its code cells:

| Part | Cells | What it covers |
|---|---|---|
| 1. String | 1 text + 14 of your examples | Create a string, `contains`, `trim`, `substring`, `split`, `toUpperCase`, `toLowerCase`, `charAt`, `concat`, `compareTo`, `startsWith`, `endsWith`, `length` |
| 2. Compare and check | 1 text + 5 code | `equals` vs `==`, `equalsIgnoreCase`, `compareToIgnoreCase`, `isEmpty` / `isBlank`, `matches` |
| 3. Search | 1 text + 3 code | `indexOf`, `indexOf(text, from)`, `lastIndexOf`, looping over characters with `charAt` and `toCharArray` |
| 4. Change text | 1 text + 7 code | Immutability, `substring(begin)`, `replace`, `replaceAll` / `replaceFirst`, `strip` family, `split` variants, `repeat`, `String.join` |
| 5. Convert and format | 1 text + 5 code | `String.valueOf`, `Integer.parseInt`, `String.format` / `formatted`, text blocks, `Character` helpers |
| 6. StringBuilder | 1 text + 4 code | `append`, `toString`, `insert`, `replace`, `delete`, `reverse`, `setCharAt`, building text in a loop |
| 7. Comparison | 1 text cell | `String` vs `StringBuilder` vs `StringBuffer` |

Each code cell **creates its own string first**, so every cell can be run on its own and in any order. Every method, including the ones in your own 14 cells, has the same 3-line comment as in `Arrays.ijnb` and `Sets.ijnb`:

```java
// Method: equals(other)
// What:   returns true when both strings have exactly the same characters (case matters)
// Use:    to check if two strings are the same text; never use == for that
System.out.println("a.equals(b): " + a.equals(b));
```

- Methods added in Java 11 or later are tagged `[Java 11+]` / `[Java 15+]`.
- `String`, `StringBuilder` and `Character` live in `java.lang`, which is always imported. Only `Arrays.toString` and `List.of` need `java.util`, and the notebook imports it for you.

### A note on your first examples

Your 14 cells kept their code, and each one now has the 3-line comment above the method, plus a short note on the line where the method is used (for example why `charAt(4)` gives `a`). The old `// true` comments, copied from the `contains` cell, were replaced by these notes. The `trim` cell also prints the length before and after, so you can see that the 17 trailing spaces are really gone.

---

## Part 1 – String

A `String` is a **class** that holds text. Its most important property is that it is **immutable**: no method can change a string, they all return a new one.

**Properties**
- Written inside **double quotes** `"Hello"`. Single quotes are for one `char`: `'H'`.
- **Immutable**: `trim`, `toUpperCase`, `replace`… return a **new** string. Always store the result: `name = name.trim();`.
- Every character has an **index** starting at `0`.
- `length()` is a **method** (brackets). On an array, `length` is a property (no brackets).
- Compare text with **`equals`**, never with `==`.
- `+` joins strings and converts numbers: `"Age: " + 20` → `"Age: 20"`.

**Syntax**

```java
//data_type variable_name = "value";
String name = "John Doe";
```

**Example**

```java
String name = "John Doe";
System.out.println("Name: " + name);                       // Name: John Doe
System.out.println("Contains 'John': " + name.contains("John")); // true
```

From cell 4 on, your examples use the same sentence: `"My name is John Wick and i worked in a movie called John Wick 4"`.

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `String name = "John Doe"` | Create a string | `Name: John Doe` |
| 2 | `contains("John")` | Is the text inside? | `true` |
| 3 | `contains("worked")` | Same, on the long sentence | `true` |
| 4 | `trim()` | Removes spaces at both ends | `Length before: 80, after: 63` |
| 5 | `substring(0, 15)` | Characters 0 to 14 | `My name is John` |
| 6 | `split(" ")` | Cuts into a `String[]` at every space | `[My, name, is, John, Wick, …, 4]` |
| 7 | `toUpperCase()` | ALL CAPS | `MY NAME IS JOHN WICK …` |
| 8 | `toLowerCase()` | all lowercase | `my name is john wick …` |
| 9 | `charAt(4)` | Character at index 4 | `a` |
| 10 | `concat(" " + data)` | Joins two strings (same as `+`) | `My name is John Wick and i worked …` |
| 11 | `compareTo(data2)` | `0` equal, negative before, positive after | `1` (`'5' - '4'`) |
| 12 | `startsWith("My name")` | Does it begin with…? | `true` |
| 13 | `endsWith("John Wick 4")` | Does it end with…? | `true` |
| 14 | `length()` | Number of characters, spaces included | `63` |

> Cells 9 to 14 use `System.out.print` instead of `println`. `print` adds no line break, which is why those outputs have no blank line under them.

---

## Part 2 – Compare and check

Methods that **ask a question** about the text and return a `boolean` (or an `int` for `compareTo`).

**Example**

```java
String a = "John Doe";
String c = new String("John Doe");  // new object, same text
System.out.println(a.equals(c));    // true   ← compares the text
System.out.println(a == c);         // false  ← compares the objects
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `equals(other)` vs `==` | Same text? vs same object? | `equals` → `true`, `==` → `false` for `new String(...)` |
| 2 | `equalsIgnoreCase(other)` | Same text, ignoring case | `"John Doe"` vs `"john doe"` → `true` |
| 3 | `compareTo` / `compareToIgnoreCase` | Alphabetical order; `compareTo` puts all capitals before all small letters | `"apple".compareTo("Banana")` → `31`, `compareToIgnoreCase` → `-1` |
| 4 | `isEmpty()` / `isBlank()` **[Java 11+]** | No characters at all / nothing but white space | `"     ".isEmpty()` → `false`, `.isBlank()` → `true` |
| 5 | `matches(regex)` | Does the **whole** text fit a pattern? (`\d{6}` = six digits) | `"411001".matches("\\d{6}")` → `true` |

> **Why `==` is wrong for strings.** `==` asks "are these the same object in memory?". Two string literals with the same text often *are* the same object (Java reuses them), so `==` sometimes looks like it works. The moment a string is built at run time (`new String`, user input, `substring`…) it stops working. `equals` always compares the characters, so always use `equals`.

---

## Part 3 – Search

Methods that **find a position**. They return an `int` index, or `-1` when nothing is found.

**Example**

```java
String name = "My name is John Wick and i worked in a movie called John Wick 4";
int first = name.indexOf("John");            // 11
int second = name.indexOf("John", first + 1); // 52
System.out.println(name.lastIndexOf("John")); // 52
System.out.println(name.indexOf("Neo"));      // -1
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `indexOf(text)` / `indexOf(char)` | First position, or `-1` | `11` / `16` / `-1` |
| 2 | `indexOf(text, from)` / `lastIndexOf(text)` | First match at or after `from` / last match | `52` / `52`, `lastIndexOf(" ")` → `61` |
| 3 | `charAt(i)` in a `for` loop / `toCharArray()` in a for-each | Look at every character | `'s'` appears 4 times in `Mississippi`; 4 vowels |

The loop cell uses what you learned in [Loops](../Loops/README.md):

```java
for (int i = 0; i < word.length(); i++) {      // counting loop: you need the index for charAt
    if (word.charAt(i) == 's') count++;
}
for (char ch : word.toCharArray()) {           // for-each: you only need the characters
    if ("aeiouAEIOU".indexOf(ch) != -1) vowels++;
}
```

---

## Part 4 – Change text

Every method here **returns a new string**. The original is never modified.

**Example (immutability)**

```java
String name = "john wick";
name.toUpperCase();                    // result thrown away
System.out.println(name);              // john wick   ← unchanged
name = name.toUpperCase();             // store it back
System.out.println(name);              // JOHN WICK
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | *(immutability demo)* | Calling a method without storing the result changes nothing | `john wick` → still `john wick` |
| 2 | `substring(begin)` / `substring(begin, end)` | From `begin` to the end / from `begin` up to (not including) `end` | `"holiday-photo.jpeg"` → `jpeg`, `holiday-photo`, `holiday` |
| 3 | `replace(oldChar, newChar)` / `replace(oldText, newText)` | Changes **every** occurrence (plain text) | `My_name_is_John_Wick_…`, `My name is Neo and …` |
| 4 | `replaceAll(regex, text)` / `replaceFirst(regex, text)` | Pattern-based replace: all matches / first match only (`\s+` = spaces, `\d` = digit) | `Order number: 1234, total: 99`, `… ####, … ##` |
| 5 | `trim()` / `strip()` / `stripLeading()` / `stripTrailing()` **[strip: Java 11+]** | Remove white space at both ends / only at the start / only at the end | `[John Wick]`, `[John Wick   ]`, `[   John Wick]` |
| 6 | `split(regex)` / `split("\\s+")` / `split(regex, limit)` | Cut into pieces; empty pieces are kept; `limit` caps the number of pieces | `[Zoya, Jane, , Doe]`, `[one, two, three]`, `[key, value=with=equals]` |
| 7 | `repeat(n)` **[Java 11+]** / `String.join(sep, …)` | Repeat text / glue pieces with a separator (the opposite of `split`) | `--------------------`, `Zoya, Jane, Doe`, `Mumbai -> Delhi -> Pune` |

> **`replace` vs `replaceAll`.** Both replace every match. The difference is that `replace` takes **plain text**, while `replaceAll` takes a **regular expression**. `"a.b".replace(".", "-")` gives `a-b`, but `"a.b".replaceAll(".", "-")` gives `---`, because `.` in a regex means "any character". Use `replace` unless you really need a pattern.

> **`split` uses a regex too.** To split on `.`, `|`, `+` or `*` you must escape them: `split("\\.")`, `split("\\|")`.

---

## Part 5 – Convert and format

Going **between text and other types**, and building text with placeholders.

**Example**

```java
String ageText = "20";
int age = Integer.parseInt(ageText);
System.out.println(ageText + 1);   // 201  ← text joining
System.out.println(age + 1);       // 21   ← maths
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `String.valueOf(x)` / `Integer.toString(n)` / `x + ""` | Number (or anything) → text | `"20"`, `"99.5"`, `"true"` |
| 2 | `Integer.parseInt(text)` / `Double.parseDouble(text)` | Text → number; throws `NumberFormatException` for `"abc"` or `" 20 "` | `21`, `199.0` |
| 3 | `String.format(template, …)` / `template.formatted(…)` **[formatted: Java 15+]** | Fill `%s` (text), `%d` (whole number), `%.1f` (one decimal); `%-10s` / `%5d` pad to a width | `John Wick acted in 4 movies with a rating of 7.5`, `\|Name      \|    1\|` |
| 4 | Text block `""" … """` **[Java 15+]** | Multi-line string without `\n` and `+`; indentation before the closing `"""` is removed | A 4-line JSON object |
| 5 | `Character.isLetter` / `isDigit` / `isUpperCase` / `toUpperCase(ch)` | Questions about, and changes to, a single `char` | `letters: 4, digits: 4, capitals: 1`, `mumbai` → `Mumbai` |

> **`"20" + 1` is `"201"`, not `21`.** When one side of `+` is a string, Java joins text. Convert first with `parseInt` when you want maths. The same trap in reverse: `1 + 2 + "3"` is `"33"` (maths first, left to right), but `"1" + 2 + 3` is `"123"`.

---

## Part 6 – StringBuilder

`StringBuilder` is a **mutable** piece of text. Its methods change the object itself and return it, so calls can be chained.

**Properties**
- `append`, `insert`, `delete`, `reverse`… change the builder **in place**.
- Much faster than `+=` in a loop: `+=` copies the whole string every time, `append` adds to the same buffer.
- Default capacity 16, grows automatically (like an `ArrayList`).
- Call `toString()` to get a normal `String` when you are done.
- Not thread-safe. The thread-safe twin is `StringBuffer`.

**Syntax**

```java
//StringBuilder variable_name = new StringBuilder();
StringBuilder sb = new StringBuilder();
StringBuilder sb2 = new StringBuilder("John Wick");  // start with text
```

**Example**

```java
StringBuilder sb = new StringBuilder();
sb.append("John").append(' ').append("Wick").append(' ').append(4);
System.out.println(sb);            // John Wick 4
String result = sb.toString();     // back to a normal String
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new StringBuilder()` / `append(x)` / `toString()` | Create; add any type at the end (chainable); get a `String` | `John Wick 4`, length `11` |
| 2 | `insert(index, x)` / `replace(start, end, text)` / `delete(start, end)` / `deleteCharAt(i)` | Add at a position / overwrite a range / remove a range or one char | `Mr. John Wick` → `Mr. Neo Wick` → `Neo Wick` → `Neo Wic` |
| 3 | `reverse()` / `setCharAt(i, ch)` / `charAt(i)` | Flip the text / overwrite one character / read one | `level` reversed is `level` → palindrome; `jack` → `Jack` |
| 4 | `append` in a loop / `setLength(n)` | Build text piece by piece; cut it to `n` characters (to drop a trailing `", "`) | `Zoya, Jane, Doe, Arbaz` |

> **`StringBuilder.replace` vs `String.replace`.** The builder's version works by **position** (`replace(4, 8, "Neo")`), the string's version by **content** (`replace("John", "Neo")`). Same name, different idea.

---

## Summary

### String methods by purpose

| Purpose | Methods |
|---|---|
| Ask a question | `equals`, `equalsIgnoreCase`, `contains`, `startsWith`, `endsWith`, `isEmpty`, `isBlank`, `matches` |
| Order | `compareTo`, `compareToIgnoreCase` |
| Find a position | `indexOf`, `indexOf(text, from)`, `lastIndexOf` |
| Read characters | `charAt`, `length`, `toCharArray` |
| Cut | `substring(begin)`, `substring(begin, end)`, `split` |
| Change | `replace`, `replaceAll`, `replaceFirst`, `toUpperCase`, `toLowerCase`, `trim`, `strip`, `stripLeading`, `stripTrailing`, `repeat` |
| Join | `+`, `concat`, `String.join`, `String.format`, `formatted` |
| Convert | `String.valueOf`, `Integer.toString`, `Integer.parseInt`, `Double.parseDouble` |

### String vs StringBuilder vs StringBuffer

| | `String` | `StringBuilder` | `StringBuffer` |
|---|---|---|---|
| Can it change? | ❌ Immutable | ✅ Mutable | ✅ Mutable |
| Thread-safe | ✅ (never changes) | ❌ | ✅ Synchronized |
| Building text in a loop | Slow (`+=` copies) | Fastest | Slower (locking) |
| Compare content | `equals` | `toString().equals(...)` or `compareTo` | same |
| Use when | Text that does not change (default) | Building or editing text step by step | Shared between threads (rare) |

### Three things to remember

1. **Strings never change.** Store the result: `name = name.trim();`.
2. **Compare with `equals`,** never with `==`.
3. **`"20" + 1` is `"201"`.** Use `Integer.parseInt` before doing maths on text.

**Previous lesson:** [Loops](../Loops/README.md)
