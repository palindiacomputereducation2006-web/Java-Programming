# Arrays – `Arrays.ijnb`

This notebook shows how to **store many values in one variable**. It starts with a normal array (`String[]`), then covers the three list types you will use most in Java: **`ArrayList`**, **`List`** and **`Vector`**. Each method has its own cell, so you can run one at a time and see what it does.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## How the notebook is organised

The notebook is grouped by type. Each group starts with a **text cell that lists its properties**, followed by its code cells:

| Part | Cells | What it covers |
|---|---|---|
| 1. Array | 1 text + 1 code | `String[]`: create and read by index |
| 2. ArrayList | 1 text + 24 code | Create, add and print, your examples, then one operation per cell |
| 3. List | 1 text + 13 code | `List` interface, `List.of`, `Arrays.asList`, `List.copyOf`, Java 21 methods |
| 4. Vector | 1 text + 15 code | Capacity and legacy methods |
| 5. Comparison | 1 text cell | Array vs `ArrayList` vs `List` vs `Vector` |

Each code cell **creates its own list first**, so every cell can be run on its own and in any order.

Your own first examples now sit inside the group they belong to:

| Group | Placed after | Methods used |
|---|---|---|
| ArrayList | the create and add cells | `add`, `addAll`, `contains`, `containsAll` |
| ArrayList | | `clear`, `isEmpty` |
| ArrayList | | `set`, `add(index, item)` |
| ArrayList | | `remove(index)` |
| List | the create cell | `indexOf` |
| Vector | the create and add cells | `add` |

> `ArrayList`, `List`, `Vector` and `Arrays` are in `java.util`. The notebook imports `java.util` for you. In a normal `.java` file, add `import java.util.*;` at the top.

### Comments in every cell

Every method has a 3-line comment above the line where it is first used in that cell. The comment says what the method is and what we use it for:

```java
// Method: remove(index) / remove(item)
// What:   removes the item at an index (returns it), or the first matching item (returns true/false)
// Use:    to take a value out of the list
fruits.remove(0);
```

- Methods that only exist on `Vector` are tagged `[Vector only, legacy]` and name the modern method to use instead (for example `addElement` → `add()`).
- Methods added in Java 21 are tagged `[Java 21+]`.
- `System.out.println` is not commented, and neither are `List.of(...)` / `Arrays.asList(...)` when they are only used to fill a list in one line.

### What this lesson does not cover (yet)

This lesson is only about **Array, `ArrayList`, `List` and `Vector`**. These topics were left out on purpose and will come in later lessons:

- Loops over a list (`for`, for-each, `while`, `do … while`, `Iterator`).
- Error handling with `try … catch`.
- The rest of the Collections Framework (`LinkedList`, `Stack`, the `Collections` and `Comparator` helpers, streams).

---

## Part 1 – Array

An array holds a **fixed number** of values of the **same type**. The size cannot change after it is created.

```java
//data_type[] variable_name = {values};
String[] names = {"Zoya", "Jane", "Doe"};
System.out.println("The first name is: " + names[0]); // Zoya
```

- Indexes start at `0`, so `names[0]` is the first item.
- `names.length` gives the number of items (no brackets, it is a property, not a method).
- Can store primitives (`int`, `double`, …) as well as objects.
- Reading an index that does not exist (`names[3]`) throws `ArrayIndexOutOfBoundsException`.

---

## Part 2 – ArrayList

A **resizable array**. It is the list you will use most often.

**Properties**
- Grows automatically (default capacity 10, grows by about 50% when full).
- Keeps insertion order; index-based starting at `0`.
- Allows duplicates and `null`.
- Stores objects only: use `Integer`, not `int`.
- **Not synchronized** → faster than `Vector`, but not thread-safe.

```java
ArrayList<String> fruits = new ArrayList<String>();
fruits.add("Apple");
fruits.add("Banana");
System.out.println("The list is: " + fruits); // [Apple, Banana]
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new ArrayList<>()` / `new ArrayList<>(20)` | Creates an empty list (optionally with a start capacity) | `[]` |
| 2 | `add(item)` | Adds at the end | `[Apple, Banana, Mango, Orange, Banana]` |
| 3 | `add(index, item)` | Inserts at an index, others shift right | `[Apple, Grapes, Banana, Mango]` |
| 4 | `addAll(collection)` / `addAll(index, collection)` | Adds many items | `[Apple, Kiwi, Papaya, Banana, …]` |
| 5 | `get(index)` | Reads an item | `Apple` |
| 6 | `set(index, item)` | Replaces an item, returns the old one | `Banana` → `[Apple, Cherry, Mango]` |
| 7 | `remove(index)` / `remove(object)` | Removes by position or by value (first match) | `[Mango, Orange, Banana]` |
| 8 | `remove(Integer.valueOf(x))` | On `Integer` lists, removes the **value** instead of the index | `[30, 40]` |
| 9 | `size()` / `isEmpty()` | Number of items / is it empty | `3` / `false` |
| 10 | `contains(item)` / `containsAll(collection)` | Is it in the list? | `true` / `false` |
| 11 | `indexOf(item)` / `lastIndexOf(item)` | First / last position, `-1` if missing | `1` / `3` / `-1` |
| 12 | `removeAll(collection)` / `retainAll(collection)` | Remove those items / keep only those items | `[Apple, Orange]` |
| 13 | `removeIf(condition)` | Removes items that match a rule | `[12, 20, 18]` |
| 14 | `sort(null)` | Sorts A→Z (natural order) | `[Apple, Banana, Mango, Orange]` |
| 15 | `subList(from, to)` | Part of the list (`to` is excluded) | `[Banana, Mango, Orange]` |
| 16 | `toArray(new String[0])` | Converts to a normal array | `[Apple, Banana, Mango]` |
| 17 | `replaceAll(rule)` | Changes every item | `[APPLE, BANANA, MANGO]` |
| 18 | `new ArrayList<>(other)` / `equals()` | Copy a list / compare two lists | `true` → `false` |
| 19 | `ensureCapacity(n)` / `trimToSize()` | Reserve space / free unused space | |
| 20 | `clear()` | Removes everything | `[]` |

---

## Part 3 – List

`List` is an **interface**: it describes what an ordered collection can do. You can't write `new List<>()`; you pick an implementation:

```java
List<String> cities = new ArrayList<>();   // most common
List<String> cities = new Vector<>();      // same methods, different inside
```

Declaring the variable as `List` (instead of `ArrayList`) is called **programming to the interface**. You can switch to another implementation later by changing only the right side.

**Shortcut ways to create a List**

| Way | Can `add` / `remove`? | Can `set`? |
|---|---|---|
| `new ArrayList<>()` | ✅ | ✅ |
| `List.of("a", "b")` | ❌ immutable | ❌ |
| `Arrays.asList("a", "b")` | ❌ fixed size | ✅ |
| `List.copyOf(list)` | ❌ immutable | ❌ |

Changing a list you are not allowed to change stops the program with an error. In the notebook these lines are commented out (`//cities.add("Goa");`) so the cells still run.

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `List<String> x = new ArrayList<>()` + `add` | Create and add | `[Mumbai, Delhi, Pune]` |
| 2 | `List.of(...)` | Immutable list | `add` → error |
| 3 | `Arrays.asList(...)` | Fixed-size list | `set` works, `add` → error |
| 4 | `List.copyOf(list)` | Immutable copy | copy doesn't change |
| 5 | `get` / `set` | Read / replace by index | `Delhi` → `[Mumbai, Kolkata, Pune]` |
| 6 | `add(index, item)` / `remove(index)` / `remove(object)` | Insert / remove | `[Jaipur, Mumbai]` |
| 7 | `size`, `isEmpty`, `contains`, `indexOf`, `lastIndexOf` | Look up information | `4`, `false`, `true`, `1`, `3` |
| 8 | `sort(null)` | Sort A→Z | `[Delhi, Goa, Mumbai, Pune]` |
| 9 | `replaceAll` / `removeIf` | Change all / remove matching | `[MUMBAI, PUNE]` |
| 10 | `subList(from, to)` | Part of the list | `[Delhi, Pune]` |
| 11 | `getFirst`, `getLast`, `addFirst`, `addLast`, `removeFirst`, `removeLast` | Work with both ends (**Java 21+**) | `[Goa, Mumbai, Delhi, Pune, Jaipur]` |
| 12 | `reversed()` | Reversed view (**Java 21+**) | `[Pune, Delhi, Mumbai]` |
| 13 | `equals` / `toArray` | Compare (same items, same order) / convert to array | `true` |

---

## Part 4 – Vector

`Vector` is the original (Java 1.0) resizable array. It works like `ArrayList`, and it also implements `List`.

**Properties**
- **Synchronized**: thread-safe, but slower.
- Default capacity 10, **doubles** when full, or grows by your own `capacityIncrement`: `new Vector<>(5, 3)`.
- Has extra **legacy methods** (`addElement`, `elementAt`, `firstElement`, `removeElement`, …).
- For new code, prefer `ArrayList`. You will still see `Vector` in older code and in interviews.

```java
Vector<String> colors = new Vector<String>();
colors.add("Red");
colors.addElement("Blue");
System.out.println(colors);                 // [Red, Blue]
System.out.println(colors.capacity());      // 10
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new Vector<>()` / `capacity()` | Create; check capacity | `Size: 0 , Capacity: 10` |
| 2 | `add` / `addElement` | Add at the end | `[Red, Green, Blue, Yellow]` |
| 3 | `new Vector<>(5, 3)` | Capacity growth: default doubles, custom grows by 3 | `11 → 20`, `6 → 8` |
| 4 | `add(index, item)` / `insertElementAt(item, index)` | Insert | `[Black, Red, White, Green, Blue]` |
| 5 | `get` / `elementAt` / `firstElement` / `lastElement` | Read | `Green`, `Blue`, `Red`, `Yellow` |
| 6 | `set` / `setElementAt(item, index)` | Replace | `[Pink, Green, Purple]` |
| 7 | `remove`, `removeElement`, `removeElementAt` | Remove by index or value | `[Yellow, White]` |
| 8 | `contains`, `indexOf`, `indexOf(item, from)`, `lastIndexOf`, `isEmpty` | Search | `true`, `1`, `3`, `3`, `false` |
| 9 | `ensureCapacity` / `trimToSize` | Grow / shrink capacity | `50` → `2` |
| 10 | `setSize(n)` | Bigger fills with `null`, smaller cuts the end | `[Red, Green, Blue, Yellow, null, null]` |
| 11 | `copyInto(array)` / `toArray` | Copy into an array | `[Red, Green, Blue]` |
| 12 | `sort(null)` | Sort A→Z | `[Blue, Green, Red, Yellow]` |
| 13 | `addAll`, `removeAll`, `retainAll`, `subList` | Bulk operations | `[Red, Blue, Yellow]` |
| 14 | `removeAllElements` / `clear` | Remove everything | `[]` |

> Note: `capacity()` exists only on `Vector`. `ArrayList` has a capacity too, but you cannot read it.

---

## Summary

| | Array | `ArrayList` | `List` | `Vector` |
|---|---|---|---|---|
| What it is | Language feature | Class | Interface | Class (legacy) |
| Size | Fixed | Grows ~50% | Depends | Grows ×2 |
| Primitives (`int`) | ✅ | ❌ use `Integer` | ❌ | ❌ |
| Size of it | `arr.length` | `size()` | `size()` | `size()` |
| Read | `arr[i]` | `get(i)` | `get(i)` | `get(i)` / `elementAt(i)` |
| Thread-safe | ❌ | ❌ | Depends | ✅ |
| Use when | Size is known | Default choice | Variable / parameter type | Old code |

## Notes on your first examples

- **Array cell:** the comment says `// Output: The first name is: John`, but the array starts with `"Zoya"`, so the real output is `Zoya`.
- **ArrayList – `clear` cell:** has an unfinished line `namesList.` before the last `println`. The saved output is from before that line was added. Delete the line, or the cell will not run.
- **ArrayList – `contains` cell:** declares `boolean is_exist` three times. A notebook allows this (each one replaces the last), but in a normal `.java` file it is a compile error. Use a different name for each, or declare it once and reassign it. Its saved output also has an extra `The list is: …` line from an older version of the code. Run the cell again to refresh it.

**Previous lesson:** [Conditionals](../Conditionals/README.md)
