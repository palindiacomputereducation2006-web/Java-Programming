# Conditionals – `conditionals.ijnb`

This notebook shows how a Java program **makes decisions**. It runs different code depending on whether a condition is `true` or `false`. The conditions use the comparison operators from the [Operators](../Operators/README.md) lesson.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

All three cells compare a variable `a` with the number **32**. The messages say *"…than b"*, but there is no variable `b` in this notebook. "b" just means the number 32.

## Cell 1 – `if`

**Syntax**

```java
if (condition) {
    // runs only when condition is true
}
```

**Code**

```java
int a = 42;

if(a > 32){
    int we = 12;
    int b = 32;
    int sum = we+b;
    System.out.println("a is greater than b : "+sum);
}
```

**How it runs**

- `a > 32` → `42 > 32` → `true`, so the block runs.
- `sum = 12 + 32 = 44`.
- Expected output: `a is greater than b : 44`

> The output saved in the notebook for this cell is **empty**. It is out of date, like a cell that was last run before the `println` line was added. Run the cell again to see the line above.

If `a` were 32 or less, nothing would print, because a plain `if` has no "otherwise" branch.

## Cell 2 – `if … else`

**Syntax**

```java
if (condition) {
    // runs when condition is true
} else {
    // runs when condition is false
}
```

**Code**

```java
int a = 43;

if(a > 32){
    int number = 12;
    int number1 = 32;
    int sum = number + number1;
    System.out.println("a is greater than b : "+sum);
}else{
    int number = 12;
    int number1 = 32;
    int sum = number1 - number;
    System.out.println("a is less than b : "+sum);
}
```

**How it runs**

- `43 > 32` → `true`, so the `if` block runs: `12 + 32 = 44`.
- **Output:** `a is greater than b : 44`
- If you change `a` to something like `10`, the `else` block runs instead: `32 - 12 = 20` → `a is less than b : 20`.

Exactly **one** of the two blocks always runs.

## Cell 3 – `if … else if … else`

**Syntax**

```java
if (condition1) {
    // condition1 is true
} else if (condition2) {
    // condition1 is false AND condition2 is true
} else {
    // none of the conditions are true
}
```

**Code**

```java
int a = 32;

if(a > 32){
    ... sum = number + number1;   // 44
    System.out.println("a is greater than b : "+sum);
}else if(a < 32){
    ... sum = number1 - number;   // 20
    System.out.println("a is less than b : "+sum);
}else{
    ... sum = number1 * number;   // 384
    System.out.println("a is equal to b : "+sum);
}
```

**How it runs**

- `32 > 32` → `false`
- `32 < 32` → `false`
- So the final `else` runs: `32 * 12 = 384`
- **Output:** `a is equal to b : 384`

Try changing `a`:

| `a` | Branch that runs | Output |
|---|---|---|
| `50` | `if (a > 32)` | `a is greater than b : 44` |
| `10` | `else if (a < 32)` | `a is less than b : 20` |
| `32` | `else` | `a is equal to b : 384` |

Java checks the conditions **from top to bottom** and runs **only the first** branch whose condition is `true`.

## Concept: block scope

Each branch declares its own `number`, `number1` and `sum`. That is allowed because a variable declared inside `{ }` exists **only inside that block**. Once the block ends, the variable is gone, so the next block can reuse the same name.

```java
if (true) {
    int x = 5;   // x lives only inside these braces
}
// System.out.println(x);  // ❌ error: cannot find symbol x
```

## Summary

| Form | Use it when… |
|---|---|
| `if` | You want to do something only when a condition is true |
| `if … else` | You have exactly two possible paths |
| `if … else if … else` | You have three or more paths, checked in order |

**Previous lesson:** [Operators](../Operators/README.md)
