# Loops – `loops.ijnb`

This notebook shows how to **repeat code** in Java. Instead of writing the same line ten times, you write it once inside a loop and tell Java how many times (or for which items, or until which condition) to run it. The examples loop over the `ArrayList` and `List` types from the [Arrays](../Arrays/Array/README.md) lesson, use `if … else` from the [Conditionals](../Conditionals/README.md) lesson to decide when to stop, and read numbers typed by the user with `Scanner`.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## The four loops in this notebook

| Loop | Cells | Use it when… | Example |
|---|---|---|---|
| **`for`** (counting loop) | 1–3, 6 | You know how many times to repeat, or you need the **index** `i` | `for (int i = 0; i < 10; i++)` |
| **for-each** (enhanced `for`) | 4–6 | You want to visit **every item** in a list or array and do not need the index | `for (String name : arr)` |
| **`while`** | 7–9 | You do **not** know the count in advance; repeat **while** a condition is true, checking it **before** each run | `while (arr.size() > 0)` |
| **`do … while`** | 10–11 | Like `while`, but the body must run **at least once** (ask for input, then check it) | `do { … } while (age < 1);` |

All of them can be stopped early with **`break`**.

> `ArrayList`, `List` and `Scanner` are in `java.util`. The notebook imports `java.util` for you. In a normal `.java` file, add `import java.util.*;` at the top.

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

## Cell 7 – The `while` loop

**Syntax**

```java
while (condition) {
    // runs again and again while condition is true
}
```

A `while` loop checks the condition **before** every iteration. If the condition is `false` the very first time, the body never runs. Use it when you do **not** know in advance how many times to repeat.

**Code**

```java
ArrayList<String> arr = new ArrayList<String>();
arr.addAll(List.of("John", "Jane", "Jack", "Jill", "James","Jenny", "Joe", "Jasmine", "Jordan", "Javier"));

while(arr.size() > 0){
    System.out.println("the number of iterations for :" + arr);
    arr.remove(0);
}
```

**How it runs**

- The condition is `arr.size() > 0`: keep going while the list still has items.
- Each iteration prints the whole list, then removes the **first** item with `arr.remove(0)`.
- The list gets shorter by one every time, so after 10 iterations it is empty, `0 > 0` is `false`, and the loop stops.

**Output (shortened)**

```
the number of iterations for :[John, Jane, Jack, Jill, James, Jenny, Joe, Jasmine, Jordan, Javier]
the number of iterations for :[Jane, Jack, Jill, James, Jenny, Joe, Jasmine, Jordan, Javier]
...
the number of iterations for :[Jordan, Javier]
the number of iterations for :[Javier]
```

> Removing items inside a `while` loop is fine, because the loop is not walking through the list with an iterator the way for-each does. The condition is checked fresh every time, so it always sees the new size. Note that this loop **empties the list**: `arr` is `[]` when it finishes.

---

## Cell 8 – `while` with keyboard input (`Scanner`)

**Code**

```java
ArrayList<Integer> arr = new ArrayList<Integer>();
int limit = 5;
while(arr.size() <= (limit - 1)){
    Scanner scn = new Scanner(System.in);
    int num = scn.nextInt();
    arr.add(num);
}

System.out.println("the numbers entered are : " + arr);
```

**How it runs**

- `Scanner` reads what the user types. `System.in` is the keyboard, and `nextInt()` waits for the user to type a whole number and press Enter.
- The condition `arr.size() <= (limit - 1)` is the same as `arr.size() < 5`: keep asking while the list has fewer than 5 numbers.
- Every number typed is added to the list. After the 5th one the condition is `false` and the loop ends.

**Output** (depends on what you type; this is the saved run)

```
the numbers entered are : [12, 12, 45, 65, 32]
```

> In a notebook, VS Code shows an **input box** at the top of the window each time `nextInt()` runs. Type a number and press Enter. Typing letters instead of a number throws `InputMismatchException`.

> The cell creates a **new** `Scanner` on every iteration. It works, but it is wasteful. The usual pattern is to create it **once** before the loop (`Scanner scn = new Scanner(System.in);`) and reuse it, as Cell 10 does.

---

## Cell 9 – Counting down with `while`

**Code**

```java
int interation = 10;

while(interation > 0){
    System.out.println("Iteration remaining: " + interation);
    interation--;
}
```

**How it runs**

- The counter starts at `10`. Each iteration prints it and then **decreases** it by one (`interation--` means `interation = interation - 1`).
- When it reaches `0`, `0 > 0` is `false` and the loop stops. So it prints `10` down to `1`.

**Output**

```
Iteration remaining: 10
Iteration remaining: 9
...
Iteration remaining: 2
Iteration remaining: 1
```

> A `while` loop has no built-in update step like `for` has. **You** must change the variable inside the body. Forget the `interation--` line and the condition stays `true` forever: an **infinite loop**. (The variable name is a typo for `iteration`, which does not matter to Java, but spell it right in your own code.)

This cell does the same job as `for (int i = 10; i > 0; i--)`. When you know the count, `for` is shorter; `while` is clearer when the stopping point depends on something else, like user input or the size of a list.

---

## Cell 10 – The `do … while` loop

**Syntax**

```java
do {
    // runs FIRST, then the condition is checked
} while (condition);
```

`do … while` is a `while` loop with the check at the **end**. The body always runs **at least once**, even if the condition is `false` from the start. Note the **semicolon** after the closing `while (...)`.

**Code**

```java
Scanner scn = new Scanner(System.in);
int age;
do {
    System.out.print("Please enter your age (Must be between 1 and 120): ");
    age = scn.nextInt();

    // if (age < 1 || age > 120) {
    //     System.out.println("Error: That age is physically impossible!");
    // }else{
    //     System.out.println("Thank you! Your age is: " + age);
    // }

    System.out.println("Thank you! Your age is: " + age);

} while (age < 1 || age > 120);
```

**How it runs**

- This is the classic use of `do … while`: **ask, then check, then ask again if the answer was bad**. You have to ask at least once, so the body goes first.
- The condition `age < 1 || age > 120` is `true` when the age is **invalid**, so the loop repeats until a valid age is typed. (`||` is the logical OR from the [Operators](../Operators/README.md) lesson.)
- `System.out.print` (without `ln`) keeps the cursor on the same line, so the typed value appears right after the prompt.

**Output** (saved run: the user typed `0`, then `12`)

```
Please enter your age (Must be between 1 and 120): Thank you! Your age is: 0
Please enter your age (Must be between 1 and 120): Thank you! Your age is: 12
```

> The first answer, `0`, is not allowed, so the loop asked again. But the cell still printed `Thank you! Your age is: 0`, because the `if … else` that checks the age is **commented out**. Remove the `//` from those lines (and delete the plain `println` below them) to print an error message for a bad age and a thank-you only for a good one.

---

## Cell 11 – Search a list with `do … while` and `break`

**Code**

```java
ArrayList<String> arr = new ArrayList<String>();
arr.addAll(List.of("John", "Jane", "Jack", "Jill", "James","Jenny", "Joe", "Jasmine", "Jordan", "Javier"));

int i = 0;
int arr_length = arr.size();
do{
    String current_name = arr.get(i);
    System.out.println("the number of iterations for :" + current_name);
    if(current_name == "Jill"){
        System.out.println("the name is found at index : " + i);
        break;
    }else{
        System.out.println("the name is not found at index : " + i);
        i++;
    }

}while(arr_length != i);
```

**How it runs**

- `i` is the index we are looking at, starting at `0`. Each iteration reads `arr.get(i)`.
- If the name is `Jill`, it prints the index and `break`s out of the loop. Otherwise it prints "not found" and moves to the next index with `i++`.
- The condition `arr_length != i` is the safety net: if `Jill` were not in the list, the loop would stop once `i` reaches `10` instead of calling `arr.get(10)` and throwing `IndexOutOfBoundsException`.
- `Jill` is the 4th name, so the loop stops at index `3`.

**Output**

```
the number of iterations for :John
the name is not found at index : 0
the number of iterations for :Jane
the name is not found at index : 1
the number of iterations for :Jack
the name is not found at index : 2
the number of iterations for :Jill
the name is found at index : 3
```

> ⚠️ **Compare strings with `equals`, not `==`.** `current_name == "Jill"` happens to work here because both strings are literals that Java stores only once. For text that was typed in, read from a file or built with `+`, `==` returns `false` even when the letters match. Write `current_name.equals("Jill")` instead. See [Strings – Part 2](../Strings/README.md#part-2--compare-and-check).

> `arr.indexOf("Jill")` gives the same answer (`3`) in one line. The loop is here to practise `do … while` with an index.

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

`break` works the same way in `while` and `do … while` loops (Cell 11 uses it to stop a `do … while` as soon as the name is found).

Its partner is **`continue`**, which skips the rest of the **current** iteration and jumps to the next one. It is not used in this notebook, but you will meet it soon:

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue;     // skip 2
    }
    System.out.println(i);   // prints 0, 1, 3, 4
}
```

## Concept: `while` vs `do … while`

The only difference is **when the condition is checked**.

```java
int n = 0;

while (n > 0) {                 // checked first: false, so the body never runs
    System.out.println("while");
}

do {                            // body runs first, then the check
    System.out.println("do-while");   // prints once
} while (n > 0);
```

- Pick **`while`** when it is fine to run zero times (there may be nothing to do).
- Pick **`do … while`** when the body must happen at least once, typically **asking the user for input and validating it** (Cell 10).
- Both need something inside the body that eventually makes the condition `false` (`arr.remove(0)`, `interation--`, `i++`, a new value from `nextInt()`), or you get an infinite loop. In VS Code, stop a runaway cell with the **Interrupt** button in the notebook toolbar.

## What this lesson does not cover (yet)

- **`continue`** (shown above, but not in the notebook).
- Looping with an **`Iterator`**, which lets you remove items safely while looping.
- `forEach(...)` with lambdas and **streams**.

## Summary

| | `for` | for-each | `while` | `do … while` |
|---|---|---|---|---|
| Syntax | `for (int i = 0; i < n; i++)` | `for (Type item : collection)` | `while (cond) { … }` | `do { … } while (cond);` |
| Best for | A known number of repeats | Every item of a collection | An unknown number of repeats | Run once, then maybe repeat |
| Condition checked | Before each run | (automatic) | **Before** each run | **After** each run |
| Minimum runs | 0 | 0 | 0 | **1** |
| Gives you the index? | ✅ `i` | ❌ (use `indexOf` if you really need it) | Only if you keep your own counter | Only if you keep your own counter |
| Gives you the item? | `list.get(i)` | ✅ `item` | `list.get(i)` | `list.get(i)` |
| Who updates the counter? | The `update` part | Java | **You**, inside the body | **You**, inside the body |
| Safe to `add`/`remove` inside? | Careful with indexes | ❌ throws an exception | ✅ (Cell 7) | ✅ |
| `break` works? | ✅ | ✅ | ✅ | ✅ |

**Scanner in one look**

```java
Scanner scn = new Scanner(System.in);   // create once
int num = scn.nextInt();                // whole number
double d = scn.nextDouble();            // decimal number
String word = scn.next();               // one word
String line = scn.nextLine();           // whole line
```

**Previous lesson:** [Maps](../Arrays/Maps/README.md) · **Next lesson:** [Strings](../Strings/README.md)
