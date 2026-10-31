# Sets – `Sets.ijnb`

This notebook shows how to **store unique values** (no duplicates) in one variable. It starts with the `Set` interface and `HashSet`, then covers the two other sets you will use: **`LinkedHashSet`** (keeps insertion order) and **`TreeSet`** (keeps values sorted). Each method has its own cell, so you can run one at a time and see what it does.

> New to notebooks? See the [main README](../../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## How the notebook is organised

| Part | Cells | What it covers |
|---|---|---|
| 1. Set / HashSet | 1 text + 2 of your examples + 8 code | Create, add, remove, search, size, bulk methods, `removeIf` |
| 2. Set operations and more | 1 text + 6 code | Union / intersection / difference, `Set.of`, list ↔ set, looping, `equals`, `clear` |
| 3. LinkedHashSet | 1 text + 2 code | Insertion order, Java 21 first/last methods |
| 4. TreeSet | 1 text + 5 code | Sorted set, `first`/`last`, `floor`/`ceiling`, `headSet`/`tailSet`, `Comparator` |
| 5. Comparison | 1 text cell | `HashSet` vs `LinkedHashSet` vs `TreeSet`, and `Set` vs `List` |

Each code cell **creates its own set first**, so every cell can be run on its own and in any order. Every method has the same 3-line comment as in `Arrays.ijnb`:

```java
// Method: add(item)
// What:   adds the item if it is not already there; returns true if added, false if it was a duplicate
// Use:    to put new unique values into the set
fruits.add("Apple");
```

> `Set`, `HashSet`, `LinkedHashSet` and `TreeSet` are in `java.util`. The notebook imports `java.util` for you. In a normal `.java` file, add `import java.util.*;` at the top.

---

## Part 1 – Set and HashSet

`Set` is an **interface** (like `List`). `HashSet` is the most common class that implements it.

**Properties**
- **No duplicates**: adding a value that is already there does nothing, and `add` returns `false`.
- **No index**: no `get(i)` or `set(i, x)`. You check a value with `contains`.
- `HashSet` has **no fixed order**: items may print in any order.
- Stores objects only: use `Integer`, not `int`.
- Allows one `null`.
- `add`, `remove` and `contains` are very fast.

**Syntax**

```java
//Set<DataType> variable_name = new HashSet<DataType>();
Set<String> fruits = new HashSet<String>();
```

**Example**

```java
Set<String> fruits = new HashSet<String>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Mango");
boolean added = fruits.add("Banana");                 // duplicate

System.out.println("Was Banana added again? " + added); // false
System.out.println("The set is: " + fruits);            // [Apple, Mango, Banana]
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new HashSet<>()` | Creates an empty set | `[]` |
| 2 | `add(item)` | Adds if not there; `true` / `false` | `false` for a duplicate |
| 3 | `addAll(collection)` | Adds many, skips duplicates | `[Apple, Kiwi, Mango, Banana]` |
| 4 | `remove(item)` | Removes by value; `true` / `false` | `true` / `false` |
| 5 | `contains(item)` / `containsAll(collection)` | Is it in the set? | `true` / `false` |
| 6 | `size()` / `isEmpty()` | Number of items / is it empty | `3` / `false` |
| 7 | `removeAll(collection)` / `retainAll(collection)` | Remove those / keep only those | `[3, 4, 5, 6]` → `[3, 4]` |
| 8 | `removeIf(condition)` | Removes items that match a rule | `[18, 20, 12]` |
| 9 | `Set.of(...)` / `Set.copyOf(collection)` | Immutable set / immutable copy | `add` → error |
| 10 | `new LinkedHashSet<>(list)` | Removes duplicates from a list | `[Zoya, Jane, Doe]` |
| 11 | `new ArrayList<>(set)` / `toArray(new String[0])` | Back to a list / to an array | |
| 12 | for-each / `forEach(action)` | Go through every item | |
| 13 | `equals(otherSet)` | Same items? (order does not matter) | `true` |
| 14 | `clear()` | Removes everything | `[]` |

---

## Part 2 – Set operations

| Operation | Meaning | How |
|---|---|---|
| Union `A ∪ B` | in A **or** B | `copy.addAll(b)` |
| Intersection `A ∩ B` | in A **and** B | `copy.retainAll(b)` |
| Difference `A − B` | in A, **not** in B | `copy.removeAll(b)` |

These methods **change** the set, so work on a copy:

```java
Set<Integer> a = new HashSet<>(Set.of(1, 2, 3, 4));
Set<Integer> b = new HashSet<>(Set.of(3, 4, 5, 6));

Set<Integer> union = new HashSet<>(a);
union.addAll(b);                // [1, 2, 3, 4, 5, 6]

Set<Integer> intersection = new HashSet<>(a);
intersection.retainAll(b);      // [3, 4]

Set<Integer> difference = new HashSet<>(a);
difference.removeAll(b);        // [1, 2]
```

---

## Part 3 – LinkedHashSet

A `HashSet` that **remembers the insertion order**.

**Syntax**

```java
//Set<DataType> variable_name = new LinkedHashSet<DataType>();
Set<String> cities = new LinkedHashSet<String>();
```

**Example**

```java
Set<String> linked = new LinkedHashSet<>();
Set<String> hash = new HashSet<>();
for (String city : List.of("Pune", "Mumbai", "Goa", "Delhi", "Pune")) {
    linked.add(city);
    hash.add(city);
}
System.out.println(linked); // [Pune, Mumbai, Goa, Delhi]   ← order kept
System.out.println(hash);   // [Delhi, Goa, Pune, Mumbai]   ← any order
```

| # | Method | What it does | Example result |
|---|---|---|---|
| 1 | `new LinkedHashSet<>()` | Set that keeps insertion order | `[Pune, Mumbai, Goa, Delhi]` |
| 2 | `getFirst()` / `getLast()` | First / last item (**Java 21+**) | `Mumbai` / `Pune` |
| 3 | `addFirst(x)` / `addLast(x)` | Add at the start / end (**Java 21+**) | `[Goa, Mumbai, Delhi, Pune, Jaipur]` |
| 4 | `removeFirst()` / `removeLast()` | Remove from the start / end (**Java 21+**) | `[Mumbai, Delhi, Pune]` |
| 5 | `reversed()` | Reversed view (**Java 21+**) | `[Pune, Delhi, Mumbai]` |

---

## Part 4 – TreeSet

Keeps its values **sorted**. It does **not** allow `null`. Declare the variable as `TreeSet` to use its extra methods.

**Syntax**

```java
//TreeSet<DataType> variable_name = new TreeSet<DataType>();
TreeSet<Integer> marks = new TreeSet<Integer>();
```

**Example**

```java
TreeSet<Integer> marks = new TreeSet<>();
marks.add(70);
marks.add(45);
marks.add(90);
marks.add(60);
System.out.println(marks);           // [45, 60, 70, 90]
System.out.println(marks.first());   // 45
System.out.println(marks.floor(65)); // 60
```

| # | Method | What it does | Example result (`[45, 60, 70, 90]`) |
|---|---|---|---|
| 1 | `first()` / `last()` | Smallest / biggest | `45` / `90` |
| 2 | `floor(x)` / `ceiling(x)` | Biggest `<= x` / smallest `>= x` | `floor(65)` = `60`, `ceiling(65)` = `70` |
| 3 | `lower(x)` / `higher(x)` | Biggest `< x` / smallest `> x` | `lower(70)` = `60`, `higher(70)` = `90` |
| 4 | `headSet(to)` / `tailSet(from)` / `subSet(from, to)` | Part of the set (`to` excluded) | `headSet(70)` = `[45, 60]` |
| 5 | `descendingSet()` | Big → small view | `[90, 70, 60, 45]` |
| 6 | `pollFirst()` / `pollLast()` | Remove and return smallest / biggest | `45` / `90` |
| 7 | `new TreeSet<>(Comparator.reverseOrder())` | Sort in reverse | `[Zoya, Jane, Doe, Arbaz]` |
| 8 | `new TreeSet<>(String.CASE_INSENSITIVE_ORDER)` | Sort text ignoring case | `[Apple, banana, Cherry]` |

---

## Summary

| | `HashSet` | `LinkedHashSet` | `TreeSet` |
|---|---|---|---|
| Order | None | Insertion order | Sorted |
| Duplicates | ❌ | ❌ | ❌ |
| `null` | ✅ one | ✅ one | ❌ |
| Speed | Fastest | Fast | Slower |
| Use when | Only uniqueness matters | You need the order you added | You need sorted values |

| | `List` | `Set` |
|---|---|---|
| Duplicates | ✅ | ❌ |
| Index (`get(i)`) | ✅ | ❌ |
| `contains` speed | Slow | Very fast |

## Notes on your first examples

Your two `Set` cells were moved here from `Arrays.ijnb`, right after the properties cell.

- Both cells name the set `arr`. It works, but a name like `numbers` is clearer, since it is a set, not an array.
- The comment says `vlaues`; it should be `values`.

**Previous lesson:** [Arrays](../Array/README.md) · **Next lesson:** [Maps](../Maps/README.md)
