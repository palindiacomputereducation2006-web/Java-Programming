# Strings – `String.ijnb`

This notebook shows how to **work with text** in Java. A `String` is a sequence of characters, like a name or a sentence. The notebook starts by creating a string, then shows one **String method** per cell: search, trim, cut, split, change case, join, compare and measure.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## A note on the comments

Most cells end the method line with the comment `// true`. It was copied from the `contains` cell, where the result really is `true`, and was not updated. Ignore it: the **saved output** under each cell shows the real result, and the tables below list it too.

## How the notebook is organised

| Cells | What they cover |
|---|---|
| 1 | Create a `String` and print it |
| 2 – 3 | `contains` |
| 4 – 9 | Change or cut the text: `trim`, `substring`, `split`, `toUpperCase`, `toLowerCase`, `charAt` |
| 10 – 11 | Join and compare: `concat`, `compareTo` |
| 12 – 14 | Check and measure: `startsWith`, `endsWith`, `length` |

Each cell **creates its own string first**, so every cell can be run on its own and in any order.

> `String` lives in `java.lang`, which is always imported. Only `Arrays.toString` (cell 6) needs `java.util`, and the notebook imports it for you.

---

## Cell 1 – Create a String

**Syntax**

```java
//data_type variable_name = "value";
String name = "John Doe";
```

**Code**

```java
String name = "John Doe";
System.out.println("Name: " + name);
```

**Output:** `Name: John Doe`

- Text goes inside **double quotes** `" "`. Single quotes `' '` are for a single `char`.
- `String` starts with a capital **S**. It is a class, not a primitive like `int`.
- `+` joins strings together. `"Name: " + name` → `Name: John Doe`.

### Strings cannot be changed

A `String` is **immutable**. None of the methods below change the original string. They all **return a new one**, so you have to store the result:

```java
String name = "  John  ";
name.trim();                  // ❌ does nothing useful: result is thrown away
String clean = name.trim();   // ✅ "John"
```

---

## Cells 2 – 3 – `contains`

Checks whether one string appears inside another. Returns a `boolean`.

```java
String name = "John Doe";
boolean hasJohn = name.contains("John"); // true
System.out.println("Contains 'John': " + hasJohn);
```

| Cell | String | `contains(...)` | Result |
|---|---|---|---|
| 2 | `"John Doe"` | `"John"` | `true` |
| 3 | `"My name is John Wick and i worked in a movie called John Wick 4"` | `"worked"` | `true` |

`contains` is **case-sensitive**: `"John Doe".contains("john")` is `false`.

---

## Cells 4 – 9 – Change or cut the text

From here on every cell uses the same sentence:

```java
String name = "My name is John Wick and i worked in a movie called John Wick 4";
```

### Cell 4 – `trim()`

Removes **spaces at the start and end** (not the spaces between words). The string in this cell has many spaces after the `4`.

```java
String data = name.trim();
System.out.println("Trimmed: " + data);
```

**Output:** `Trimmed: My name is John Wick and i worked in a movie called John Wick 4`

> The extra spaces are hard to see in the output. Compare `name.length()` (80) with `data.length()` (63) to prove they are gone. Java 11+ also has `strip()`, which does the same and handles more kinds of white space.

### Cell 5 – `substring(begin, end)`

Cuts out a part of the string. `begin` is **included**, `end` is **excluded**.

```java
String data = name.substring(0, 15);
System.out.println("Substring: " + data);
```

**Output:** `Substring: My name is John`

Indexes `0` to `14` are kept, which is exactly 15 characters. `substring(begin)` with one argument keeps everything from `begin` to the end.

### Cell 6 – `split(separator)`

Breaks the string into a **`String[]` array**, cutting at every separator. Here the separator is a single space.

```java
String[] data = name.split(" ");
System.out.println("Split: " + Arrays.toString(data));
```

**Output:** `Split: [My, name, is, John, Wick, and, i, worked, in, a, movie, called, John, Wick, 4]`

> Printing an array directly (`System.out.println(data)`) shows something like `[Ljava.lang.String;@1b6d3586`. Wrap it in `Arrays.toString(...)` to see the items, as done here.

### Cell 7 – `toUpperCase()`

```java
String data = name.toUpperCase();
```

**Output:** `Uppercase: MY NAME IS JOHN WICK AND I WORKED IN A MOVIE CALLED JOHN WICK 4`

### Cell 8 – `toLowerCase()`

```java
String data = name.toLowerCase();
```

**Output:** `Lowercase: my name is john wick and i worked in a movie called john wick 4`

Both are useful for **case-insensitive** checks: `a.toLowerCase().equals(b.toLowerCase())`. (Or use `a.equalsIgnoreCase(b)`.)

### Cell 9 – `charAt(index)`

Returns the **single character** (`char`) at a position. Indexes start at `0`.

```java
char data = name.charAt(4);
System.out.print("Character at index 4: " + data);
```

**Output:** `Character at index 4: a`

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| Char | `M` | `y` | ` ` | `n` | `a` | `m` | `e` |

Asking for an index that does not exist (`name.charAt(100)`) throws `StringIndexOutOfBoundsException`.

> This cell and the ones after it use `System.out.print` instead of `println`. `print` does not add a line break at the end, which is why these outputs have no blank line under them.

---

## Cells 10 – 11 – Join and compare

### Cell 10 – `concat(other)`

Joins two strings into a new one. Same as `+`.

```java
String name = "My name is John Wick";
String data = "and i worked in a movie called John Wick 4";

String complete_Data = name.concat(" " + data);
System.out.print("Complete Data: " + complete_Data);
```

**Output:** `Complete Data: My name is John Wick and i worked in a movie called John Wick 4`

The `" " + data` adds the missing space between `Wick` and `and`. In everyday code `name + " " + data` is more common than `concat`.

### Cell 11 – `compareTo(other)`

Compares two strings **alphabetically** (by character codes) and returns an `int`:

| Result | Meaning |
|---|---|
| `0` | Both strings are exactly equal |
| negative | This string comes **before** the other |
| positive | This string comes **after** the other |

```java
String data  = "My name is John Wick and i worked in a movie called John Wick 5";
String data2 = "My name is John Wick and i worked in a movie called John Wick 4";

int is_comapred = data.compareTo(data2);
System.out.print("Is compared: " + is_comapred);
```

**Output:** `Is compared: 1`

The two strings are identical until the last character: `'5'` vs `'4'`. The result is the difference of their codes, `'5' - '4' = 1`, so `data` sorts after `data2`.

> ⚠️ **Never compare strings with `==`.** `==` checks whether two variables point to the **same object**, not whether the text is the same. Use `equals` for "is it the same text?" and `compareTo` for "which one comes first?":
>
> ```java
> String a = new String("hi");
> String b = "hi";
> a == b          // false  (different objects)
> a.equals(b)     // true   (same text)
> a.compareTo(b)  // 0      (same text)
> ```

---

## Cells 12 – 14 – Check and measure

### Cell 12 – `startsWith(prefix)`

```java
String name = "My name is John Wick and i worked in a movie called John Wick 4";
boolean is_start = name.startsWith("My name");
System.out.print("Starts with 'My name': " + is_start);
```

**Expected output:** `Starts with 'My name': true`

> ⚠️ The output saved in the notebook for this cell shows **`false`**. That is out of date: the string does start with `My name`, so the real result is `true`. The cell was probably edited after it last ran. Run it again to refresh the output.

### Cell 13 – `endsWith(suffix)`

```java
boolean is_start = name.endsWith("John Wick 4");
System.out.print("ends with 'John Wick 4': " + is_start);
```

**Output:** `ends with 'John Wick 4': true`

### Cell 14 – `length()`

Number of characters, including spaces.

```java
int length = name.length();
System.out.print("Length of the string: " + length);
```

**Output:** `Length of the string: 63`

> `length()` on a `String` has **brackets**: it is a method. `length` on an array has **no brackets**: it is a property. `"abc".length()` but `names.length`.

---

## What this lesson does not cover (yet)

- `equals` / `equalsIgnoreCase` (shown above, but not in the notebook), `isEmpty`, `isBlank`.
- `indexOf` / `lastIndexOf` on strings, `replace` / `replaceAll`, `repeat`, `join`.
- `String.format` and text blocks (`"""`).
- `StringBuilder`, the mutable alternative for building long strings in a loop.
- Converting between strings and numbers: `Integer.parseInt("42")`, `String.valueOf(42)`.

## Summary

| Method | Returns | What it does | Example |
|---|---|---|---|
| `contains(s)` | `boolean` | Is `s` inside the string? | `"John Doe".contains("John")` → `true` |
| `trim()` | `String` | Removes leading/trailing spaces | `"  hi  ".trim()` → `"hi"` |
| `substring(b, e)` | `String` | Characters from `b` up to (not including) `e` | `"My name".substring(0, 2)` → `"My"` |
| `split(sep)` | `String[]` | Cuts into pieces at each `sep` | `"a b c".split(" ")` → `[a, b, c]` |
| `toUpperCase()` | `String` | ALL CAPS | `"hi".toUpperCase()` → `"HI"` |
| `toLowerCase()` | `String` | all lowercase | `"HI".toLowerCase()` → `"hi"` |
| `charAt(i)` | `char` | Character at index `i` | `"My name".charAt(4)` → `'a'` |
| `concat(s)` | `String` | Joins `s` onto the end | `"a".concat("b")` → `"ab"` |
| `compareTo(s)` | `int` | `0` equal, `<0` before, `>0` after | `"b".compareTo("a")` → `1` |
| `startsWith(s)` | `boolean` | Does it begin with `s`? | `"My name".startsWith("My")` → `true` |
| `endsWith(s)` | `boolean` | Does it end with `s`? | `"Wick 4".endsWith("4")` → `true` |
| `length()` | `int` | Number of characters | `"John Doe".length()` → `8` |

**Previous lesson:** [Loops](../Loops/README.md)
