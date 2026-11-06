# Maps – `Maps.ijnb`

This notebook shows how to **store key → value pairs**, like a dictionary (`roll number → name`, `word → count`). It starts with the `Map` interface and `HashMap`, then covers **`LinkedHashMap`** (keeps insertion order) and **`TreeMap`** (keeps keys sorted). Each method has its own cell, so you can run one at a time and see what it does.

> New to notebooks? See the [main README](../../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## How the notebook is organised

| Part | Cells | What it covers |
|---|---|---|
| 1. Map / HashMap | 1 text + 1 of your examples + 15 code | Create, `put`, `get`, `putIfAbsent`, search, remove, replace, views, looping, `merge`, `compute`, `Map.of`, `equals`, `clear` |
| 2. LinkedHashMap | 1 text + 3 code | Insertion order, access order, Java 21 first/last methods |
| 3. TreeMap | 1 text + 5 code | Sorted keys, `firstKey`/`lastKey`, `floorKey`/`ceilingKey`, `headMap`/`tailMap`, `Comparator` |
| 4. Comparison | 1 text cell | `HashMap` vs `LinkedHashMap` vs `TreeMap` vs `Hashtable` |

Each code cell **creates its own map first**, so every cell can be run on its own and in any order. Every method has the same 3-line comment as in `Arrays.ijnb`:

```java
// Method: put(key, value)
// What:   adds the pair; if the key already exists it replaces the value and returns the OLD value (else null)
// Use:    to add or update a value
students.put(101, "Zoya");
```

> `Map`, `HashMap`, `LinkedHashMap` and `TreeMap` are in `java.util`. The notebook imports `java.util` for you. In a normal `.java` file, add `import java.util.*;` at the top.

---

## Part 1 – Map and HashMap

`Map` is an **interface**. `HashMap` is the most common class that implements it.

**Properties**
- **Keys are unique**: `put` with an existing key **replaces** the value.
- **Values can repeat**.
- **No index**: read with `get(key)`, not `get(0)`.
- `HashMap` has **no fixed order**.
- Keys and values are objects: use `Integer`, not `int`.
- Allows one `null` key and many `null` values.
- A `Map` is not a `Collection`: there is no `add()`, use `put()`.

**Syntax**

```java
//Map<KeyType, ValueType> variable_name = new HashMap<KeyType, ValueType>();
Map<Integer, String> students = new HashMap<Integer, String>();
```

**Example**

```java
Map<Integer, String> students = new HashMap<>();
students.put(101, "Zoya");
students.put(102, "Jane");
students.put(103, "Doe");
String old = students.put(102, "Arbaz");          // replaces Jane

System.out.println(old);                          // Jane
System.out.println(students);                     // {101=Zoya, 102=Arbaz, 103=Doe}
System.out.println(students.get(101));            // Zoya
System.out.println(students.getOrDefault(999, "Unknown")); // Unknown
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new HashMap<>()` | Creates an empty map | `{}` |
| 2 | `put(key, value)` | Adds or replaces; returns the old value | `Jane` → `{101=Zoya, 102=Arbaz, 103=Doe}` |
| 3 | `get(key)` / `getOrDefault(key, default)` | Read a value (`null` / default if missing) | `Zoya` / `null` / `Unknown` |
| 4 | `putIfAbsent(key, value)` | Adds only if the key is missing | `{101=Zoya, 102=Doe}` |
| 5 | `putAll(otherMap)` | Copies all pairs in | `{101=Zoya Khan, 102=Doe, 103=Arbaz}` |
| 6 | `containsKey(key)` / `containsValue(value)` | Is the key / value there? | `true` / `false` |
| 7 | `remove(key)` / `remove(key, value)` | Remove a pair | `Zoya` / `false` / `true` |
| 8 | `replace(key, value)` / `replace(key, old, new)` | Replace only if the key exists | `{101=Zoya Khan, 102=Jane Doe}` |
| 9 | `replaceAll((k, v) -> ...)` | Change every value | `{101=ZOYA KHAN, 102=JANE DOE}` |
| 10 | `size()` / `isEmpty()` | Number of pairs / is it empty | `2` / `false` |
| 11 | `keySet()` / `values()` / `entrySet()` | All keys / all values / all pairs | `[Zoya, Jane, Doe]` / `[85, 92, 78]` |
| 12 | for-each over `entrySet()` / `forEach((k, v) -> ...)` | Go through every pair | `Zoya scored 85` |
| 13 | `merge(key, 1, Integer::sum)` | Add or combine (counters) | `{and=2, bird=1, cat=1, dog=1, the=3}` |
| 14 | `compute` / `computeIfPresent` / `computeIfAbsent` | Calculate a new value | `{D=[Doe], J=[Jane, John], Z=[Zoya, Zara]}` |
| 15 | `Map.of` / `Map.ofEntries` / `Map.copyOf` | Immutable maps | `put` → error |
| 16 | `equals(otherMap)` | Same pairs? (order does not matter) | `true` |
| 17 | `clear()` | Removes everything | `{}` |

**Looping over a map**

```java
for (Map.Entry<String, Integer> entry : marks.entrySet()) {
    System.out.println(entry.getKey() + " scored " + entry.getValue());
}
// or
marks.forEach((name, score) -> System.out.println(name + " scored " + score));
```

**Counting words with `merge`**

```java
Map<String, Integer> wordCount = new TreeMap<>();
for (String word : "the cat and the dog and the bird".split(" ")) {
    wordCount.merge(word, 1, Integer::sum);
}
System.out.println(wordCount); // {and=2, bird=1, cat=1, dog=1, the=3}
```

---

## Part 2 – LinkedHashMap

A `HashMap` that **remembers the insertion order** of its keys.

**Syntax**

```java
//Map<KeyType, ValueType> variable_name = new LinkedHashMap<KeyType, ValueType>();
Map<String, Integer> marks = new LinkedHashMap<String, Integer>();
```

**Example**

```java
Map<String, Integer> linked = new LinkedHashMap<>();
Map<String, Integer> hash = new HashMap<>();
for (String city : List.of("Pune", "Mumbai", "Goa", "Delhi")) {
    linked.put(city, city.length());
    hash.put(city, city.length());
}
System.out.println(linked); // {Pune=4, Mumbai=6, Goa=3, Delhi=5}   ← order kept
System.out.println(hash);   // {Delhi=5, Goa=3, Pune=4, Mumbai=6}   ← any order
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new LinkedHashMap<>()` | Map that keeps insertion order | `{Pune=4, Mumbai=6, Goa=3, Delhi=5}` |
| 2 | `new LinkedHashMap<>(16, 0.75f, true)` | Access order: used keys move to the end | `get(A)` → `{B=2, C=3, A=1}` |
| 3 | `firstEntry()` / `lastEntry()` | First / last pair (**Java 21+**) | `Zoya=85` / `Doe=78` |
| 4 | `putFirst(k, v)` / `putLast(k, v)` | Put at the start / end (**Java 21+**) | `{Arbaz=88, Jane=92, Doe=78, Zoya=90}` |
| 5 | `pollFirstEntry()` / `pollLastEntry()` | Remove and return first / last (**Java 21+**) | `Arbaz=88` |
| 6 | `reversed()` | Reversed view (**Java 21+**) | `{Zoya=90, Doe=78, Jane=92}` |

---

## Part 3 – TreeMap

Keeps its pairs **sorted by key**. It does **not** allow a `null` key. Declare the variable as `TreeMap` to use its extra methods.

**Syntax**

```java
//TreeMap<KeyType, ValueType> variable_name = new TreeMap<KeyType, ValueType>();
TreeMap<Integer, String> ranks = new TreeMap<Integer, String>();
```

**Example**

```java
TreeMap<Integer, String> grades = new TreeMap<>();
grades.put(0, "F");
grades.put(40, "D");
grades.put(60, "C");
grades.put(75, "B");
grades.put(90, "A");

System.out.println(grades.firstKey());                // 0
System.out.println(grades.floorKey(68));              // 60
System.out.println(grades.floorEntry(68).getValue()); // C  ← marks 68 = grade C
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `firstKey()` / `lastKey()` | Smallest / biggest key | `1` / `4` |
| 2 | `firstEntry()` / `lastEntry()` | Pair with smallest / biggest key | `1=Zoya` / `4=Arbaz` |
| 3 | `floorKey(x)` / `ceilingKey(x)` | Biggest key `<= x` / smallest key `>= x` | `floorKey(68)` = `60`, `ceilingKey(68)` = `75` |
| 4 | `lowerKey(x)` / `higherKey(x)` | Biggest key `< x` / smallest key `> x` | `40` / `75` |
| 5 | `floorEntry(x)` | Pair for a range lookup | `68 → C` |
| 6 | `headMap(to)` / `tailMap(from)` / `subMap(from, to)` | Part of the map (`to` excluded) | `headMap(3)` = `{1=Zoya, 2=Jane}` |
| 7 | `descendingMap()` / `descendingKeySet()` | Big → small | `{3=Doe, 2=Jane, 1=Zoya}` |
| 8 | `pollFirstEntry()` / `pollLastEntry()` | Remove and return first / last pair | `1=Zoya` / `3=Doe` |
| 9 | `new TreeMap<>(Comparator.reverseOrder())` | Sort keys in reverse | `{Zoya=85, Jane=92, Doe=78, Arbaz=88}` |

---

## Summary

| | `HashMap` | `LinkedHashMap` | `TreeMap` | `Hashtable` |
|---|---|---|---|---|
| Order of keys | None | Insertion (or access) | Sorted | None |
| `null` key | ✅ one | ✅ one | ❌ | ❌ |
| Speed | Fastest | Fast | Slower | Slower (locking) |
| Thread-safe | ❌ | ❌ | ❌ | ✅ (legacy) |
| Use when | Default choice | You need the order you added | You need sorted keys | Old code only |

## Notes on your first example

Your `Map` cell was moved here from `Arrays.ijnb`, right after the properties cell.

- `hasValueTwo` checks `map.containsValue("fifth")`, but the message prints `Has value 'Two'`. That is why the output says `false`. Change it to `containsValue("Two")` to get `true`.

**Previous lesson:** [Sets](../Sets/README.md) · **Next lesson:** [Loops](../../Loops/README.md)
