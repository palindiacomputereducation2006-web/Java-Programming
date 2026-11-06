# Loops – `loops.ijnb`

This notebook shows how to **repeat code** in Java. Instead of writing the same line ten times, you write it once inside a loop and tell Java how many times (or for which items) to run it. The examples loop over the `ArrayList` and `List` types from the [Arrays](../Arrays/Array/README.md) lesson, and use `if … else` from the [Conditionals](../Conditionals/README.md) lesson to decide when to stop.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## The two loops in this notebook

| Loop | Use it when… | Example |
|---|---|---|
| **`for`** (counting loop) | You know how many times to repeat, or you need the **index** `i` | `for (int i = 0; i < 10; i++)` |
| **for-each** (enhanced `for`) | You want to visit **every item** in a list or array and do not need the index | `for (String name : arr)` |

Both loops can be stopped early with **`break`**.

> `ArrayList` and `List` are in `java.util`. The notebook imports `java.util` for you. In a normal `.java` file, add `import java.util.*;` at the top.

---

## Cell 1 – The `for` loop

**Syntax**

```java
for (initialization; condition; update) {
    // runs while condition is true
}
```

| Part | Example | When it runs |
|---|---|---|
| initialization | `int i = 1` | Once, before the loop starts |
| condition | `i < 10` | Before **every** iteration. If `false`, the loop ends |
| update | `i++` | After **every** iteration (`i++` means `i = i + 1`) |

**Code**

```java
for (int i = 1; i < 10; i++) {
    System.out.println("the iteration number is : "+i);
}

System.out.println("---------------------------------------------------");

for (int i = 1; i <= 10; i++) {
    System.out.println("the iteration number is : "+i);
}
```

**How it runs**

- The first loop uses `i < 10`, so it prints `1` to **`9`** (9 lines). When `i` becomes 10, `10 < 10` is `false` and the loop stops.
- The second loop uses `i <= 10`, so it prints `1` to **`10`** (10 lines).

**Output (shortened)**

```
the iteration number is : 1
...
the iteration number is : 9
---------------------------------------------------
the iteration number is : 1
...
the iteration number is : 10
```

> `<` vs `<=` is the most common loop mistake. With `<`, the end value is **not** included. With `<=`, it **is** included.

---

## Cell 2 – Stop early with `break`

**Code**

```java
ArrayList<Integer> arr = new ArrayList<Integer>();
int size = 20;

for (int i = 0; i < 30; i++) {
    if(size == i){
        break;
    }else{
        arr.add(i);
    }
}

System.out.println(arr);
System.out.println("The size of the array list is : "+arr.size());
```

**How it runs**

- The loop is written to run 30 times (`i` from 0 to 29).
- Each time, `i` is added to the list, **unless** `i == 20`. Then `break` ends the loop immediately.
- So only `0` to `19` are added: **20 items**.

**Output**

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
The size of the array list is : 20
```

> `break` jumps out of the **whole loop**. The rest of that iteration and all later iterations are skipped. Here the `else` is not really needed: `break` already leaves the loop, so `arr.add(i)` after the `if` would never run for `i == 20`.

---

## Cell 3 – Fill a list, then replace one value

**Code**

```java
List<Integer> list = new ArrayList<Integer>();

int position = 7;
int value = 100;

for (int i = 1; i <= 20; i++) {
    list.add(i);
}
System.out.println(list);

for (int i = 1; i < list.size(); i++){
    int index = list.indexOf(i);
    if(index == position){
        list.set(index,value);
    }
}

System.out.println(list);
```

**How it runs**

- The first loop fills the list with `1` to `20`.
- The second loop looks up where each number `i` sits (`indexOf(i)`). When that index equals `7`, it replaces that item with `100`.
- Indexes start at `0`, so index `7` holds the **8th** item, which is the number `8`.

**Output**

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
[1, 2, 3, 4, 5, 6, 7, 100, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
```

> You do not need a loop for this. `list.set(position, value);` does the same thing in one line. The loop is here to practise `indexOf` and `set` together.

---

## Cell 4 – The for-each loop

**Syntax**

```java
for (Type item : collection) {
    // runs once for every item, in order
}
```

**Code**

```java
ArrayList<String> arr = new ArrayList<String>();
String [] names = {"John", "Jane", "Jack", "Jill", "James","Jenny", "Joe", "Jasmine", "Jordan", "Javier"};
arr.addAll(List.of(names));

for (String name : arr) {
    System.out.println("the number of iterations for :" + name);
}
```

**How it runs**

- `List.of(names)` turns the array into a list, and `addAll` copies it into `arr`.
- `for (String name : arr)` visits each name from first to last. On every iteration `name` holds the current item.
- No counter, no index, no `size()`: Java handles that for you.

**Output**

```
the number of iterations for :John
the number of iterations for :Jane
...
the number of iterations for :Javier
```

> Use for-each when you only need the **items**. Use a counting `for` when you need the **index** too (for example, to call `set(index, …)`).

---

## Cell 5 – Find an index inside for-each, then `break`

**Code**

```java
ArrayList<String> arr = new ArrayList<String>();
String [] names = {"John", "Jane", "Jack", "Jill", "James","Jenny", "Joe", "Jasmine", "Jordan", "Javier"};
arr.addAll(List.of(names));

System.out.println("these are the names : " + arr);

int index = 5;
String change_name = "Javed";

for (String name : arr){
    int indexOfName = arr.indexOf(name);
    if(indexOfName == index){
        arr.set(indexOfName,change_name);
        break;
    }
}

System.out.println("these are the names after the change : " + arr);
```

**How it runs**

- A for-each loop has no index, so the cell asks the list for it with `arr.indexOf(name)`.
- When the index is `5` (the 6th name, `Jenny`), it is replaced with `Javed` and `break` stops the loop.

**Output**

```
these are the names : [John, Jane, Jack, Jill, James, Jenny, Joe, Jasmine, Jordan, Javier]
these are the names after the change : [John, Jane, Jack, Jill, James, Javed, Joe, Jasmine, Jordan, Javier]
```

> ⚠️ **Changing a list while looping over it with for-each is risky.** `set` is safe because it does not change the size. `add` or `remove` inside a for-each throws `ConcurrentModificationException`. The `break` right after `set` also makes sure the loop does not continue after the change. A plain `for (int i …)` loop, or simply `arr.set(5, "Javed");`, is the safer way to write this.

---

## Cell 6 – Nested loops: replace many names

**Code**

```java
ArrayList<String> arr = new ArrayList<String>();
String [] names = {"John", "Jane", "Jack", "Jill", "James","Jenny", "Joe", "Jasmine", "Jordan", "Javier"};
arr.addAll(List.of(names));

List<Integer> data_array = new ArrayList<Integer>();
data_array.addAll(List.of(0,1,2,3,4,5,6));

List<String> replacement_names = new ArrayList<String>();
replacement_names.addAll(List.of("Junaid","Humaira","Ali","Ayesha","Hassan","Hina","Sana"));

for (int i = 0; i < data_array.size(); i++){
    for (String name : arr){
        int indexOfName = arr.indexOf(name);
        if(indexOfName == data_array.get(i)){
            arr.set(indexOfName,replacement_names.get(i));
            break;
        }
    }
}

System.out.println("these are the names after the change Final names : " + arr);
```

**How it runs**

- `data_array` lists the **indexes to replace** (`0` to `6`), and `replacement_names` lists the **new names**, in the same order.
- The **outer** `for` loop goes through `data_array` one index at a time.
- For each index, the **inner** for-each loop searches `arr` for the name at that index, replaces it, and `break`s out of the inner loop only. The outer loop then moves to the next index.
- The last three names (index `7`, `8`, `9`) are not in `data_array`, so they stay the same.

**Output**

```
these are the inital names : [John, Jane, Jack, Jill, James, Jenny, Joe, Jasmine, Jordan, Javier]
these are the names after the change Final names : [Junaid, Humaira, Ali, Ayesha, Hassan, Hina, Sana, Jasmine, Jordan, Javier]
```

> A `break` inside a nested loop only leaves the **innermost** loop it is in. Also, the inner loop is doing more work than needed: `arr.set(data_array.get(i), replacement_names.get(i));` replaces the name directly without searching.

---

## Concept: `break`

`break` ends the loop **right away**, no matter what the condition says.

```java
for (int i = 0; i < 100; i++) {
    if (i == 3) {
        break;        // loop ends here, i never reaches 4
    }
    System.out.println(i);   // prints 0, 1, 2
}
```

Its partner is **`continue`**, which skips the rest of the **current** iteration and jumps to the next one. It is not used in this notebook, but you will meet it soon:

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue;     // skip 2
    }
    System.out.println(i);   // prints 0, 1, 3, 4
}
```

## What this lesson does not cover (yet)

- **`while`** and **`do … while`** loops: repeat while a condition is true, when you do not know the count in advance.
- **`continue`** (shown above, but not in the notebook).
- Looping with an **`Iterator`**, which lets you remove items safely while looping.
- `forEach(...)` with lambdas and **streams**.

## Summary

| | `for` | for-each |
|---|---|---|
| Syntax | `for (int i = 0; i < n; i++)` | `for (Type item : collection)` |
| Gives you the index? | ✅ `i` | ❌ (use `indexOf` if you really need it) |
| Gives you the item? | `list.get(i)` | ✅ `item` |
| Can count backwards / skip? | ✅ (`i--`, `i += 2`) | ❌ always first to last |
| Safe to `add`/`remove` inside? | Careful with indexes | ❌ throws an exception |
| `break` works? | ✅ | ✅ |

**Previous lesson:** [Maps](../Arrays/Maps/README.md) · **Next lesson:** [Strings](../Strings/README.md)
