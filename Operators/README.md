# Operators – `Operators.ijnb`

This notebook shows how to **compare values** and **combine true/false conditions** in Java. Every result is a `boolean` (`true` or `false`). Later, the [Conditionals](../Conditionals/README.md) lesson uses these results to make decisions.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## A note on the labels

Every cell prints the label `"is a equal to b : "` (or `"is a equal to c : "`), and most end with the comment `// Output: false`. These labels and comments were **copied from the first cell** and were not updated. The **operator** in each cell is what decides the result. The tables below list the operator and the actual result.

## Part A – Comparison operators

Each cell has the same pattern:

```java
int a = ...;
int b = ...;

boolean is_equal = (b <operator> a);
System.out.println("is a equal to b : "+is_equal);
```

| Cell | `a` | `b` | Expression | Meaning | Result |
|---|---|---|---|---|---|
| 1 | 21 | 32 | `a == b` | equal to | `false` |
| 2 | 21 | 32 | `b > a` | greater than | `true` ⚠️ |
| 3 | 32 | 32 | `b >= a` | greater than **or** equal to | `true` |
| 4 | 32 | 32 | `b != a` | **not** equal to | `false` |
| 5 | 31 | 32 | `b != a` | **not** equal to | `true` |
| 6 | 32 | 21 | `b < a` | less than | `true` |
| 7 | 32 | 32 | `b <= a` | less than **or** equal to | `true` |

> ⚠️ **Cell 2:** 32 > 21 is `true`, but the output saved in the notebook shows `false`. The saved output is out of date (the cell was probably edited after it last ran). Run the cell again and you will get `true`.

Remember:
- `=` **assigns** a value (`int a = 5;`).
- `==` **compares** two values (`a == 5` → `true`/`false`).

## Part B – Logical operators

Logical operators combine or flip `boolean` values.

### `&&` – AND (true only if **both** sides are true)

```java
int a = 32;
int b = 32;
int c = 64;

boolean sum = (b == c && c == a);
System.out.println("is a equal to c : "+sum);
```

`b == c` → `32 == 64` → `false`, so the whole expression is **`false`**.
(Java stops at the first `false` and doesn't check the right side. This is called *short-circuit* evaluation.)

### `||` – OR (true if **at least one** side is true)

```java
boolean sum = (b == c || b == a);
```

`b == c` is `false`, but `b == a` → `32 == 32` → `true`, so the result is **`true`**.

### `!` – NOT (flips true ↔ false)

```java
boolean sum = true;
boolean result = !sum;
System.out.println("is a equal to c : "+result);
```

`!true` → **`false`**.

## Summary

| Operator | Name | Example (`a = 5`, `b = 3`) | Result |
|---|---|---|---|
| `==` | equal to | `a == b` | `false` |
| `!=` | not equal to | `a != b` | `true` |
| `>` | greater than | `a > b` | `true` |
| `<` | less than | `a < b` | `false` |
| `>=` | greater than or equal | `a >= 5` | `true` |
| `<=` | less than or equal | `b <= 2` | `false` |
| `&&` | AND | `a > 1 && b > 1` | `true` |
| `\|\|` | OR | `a > 10 \|\| b > 1` | `true` |
| `!` | NOT | `!(a > b)` | `false` |

**Previous lesson:** [Variables](../variables/README.md) · **Next lesson:** [Conditionals](../Conditionals/README.md)
