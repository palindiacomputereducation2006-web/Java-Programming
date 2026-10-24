# Variables – `variable.ijnb`

This notebook shows how to **store values in variables** in Java. It covers the common data types, how to make a constant, and how to change a variable's value.

> New to notebooks? See the [main README](../README.md#part-3--run-java-code-as-a-notebook) for how to open and run this file in VS Code.

## What is a variable?

A variable is a named box that holds a value. In Java, every variable has a **type**, and the type decides what kind of value the box can hold:

```java
type name = value;
//  int  age  =  21;
```

## Cell-by-cell walkthrough

### 1. Adding two `int` numbers

```java
int number = 12;
int number1 = 5;

int sum = number1 + number;
System.out.print("the addition of " +number+ " and " +number1+ " is : " + sum);
```

**Output:** `the addition of 12 and 5 is : 17`

- `int` stores **whole numbers** (no decimal point).
- `+` between two numbers **adds** them. `+` between a `String` and anything else **joins them into text** (string concatenation).
- `print` does **not** add a new line at the end. `println` does.

> The comment in this cell says it "will cause a compilation error due to duplicate variable declaration". That comment is out of date: the cell runs fine and prints 17.

### 2. `String` – text

```java
String message = "Hello, World!";
System.out.println(message);
```

**Output:** `Hello, World!`

`String` holds text. Text goes inside **double quotes** `" "`.

### 3. `Boolean` – true / false

```java
Boolean isJavaFun = false;
Boolean isJava = true;

System.out.println(isJavaFun); // false
System.out.println(isJava);    // true
```

**Output:**
```
false
true
```

A boolean can only be `true` or `false`.

> Note: `Boolean` (capital **B**) is the *wrapper class*. `boolean` (lowercase) is the *primitive type*. Both work here. For simple variables, `boolean` is the usual choice.

### 4. `char` – a single character

```java
char letter = 'A';
System.out.println("this is the letter i was printing : "+letter);

char letter = 'A';
System.out.println("this is the letter i was printing : "+letter+" values");
```

**Output:**
```
this is the letter i was printing : A
this is the letter i was printing : A values
```

- `char` holds **one** character, written in **single quotes** `' '`.
- This cell declares `letter` **twice**. A notebook allows that (the second declaration replaces the first, like `jshell`). In a normal `.java` file, the same code would **fail to compile** with *"variable letter is already defined"*.

### 5. `float` – decimal number (single precision)

```java
float decimalNumber = 3.14464565f;
System.out.println("this is the decimal number i was printing : "+decimalNumber);
```

**Output:** `this is the decimal number i was printing : 3.1446457`

- A `float` value needs an **`f`** at the end (`3.14f`).
- A `float` keeps only about **7 significant digits**, so `3.14464565` gets rounded to `3.1446457`.

### 6. `double` – decimal number (double precision)

```java
double decimalNumber = 3.14464565;
System.out.println("this is the decimal number i was printing : "+decimalNumber);
```

**Output:** `this is the decimal number i was printing : 3.14464565`

A `double` keeps about **15–16 significant digits**, so the full value is printed. `double` is Java's default type for decimal numbers.

### 7. `final` – constants

```java
final float pi = 3.14f;
System.out.println("this is the value of pi : "+pi);
```

**Output:** `this is the value of pi : 3.14`

`final` means the value **cannot be changed** after it is set. Writing `pi = 3.15f;` later would be a compile error.

### 8. Changing a variable's value

```java
int arbaz = 321;
arbaz = 43232;
System.out.println("this is the value of arbaz : "+arbaz);
```

**Output:** `this is the value of arbaz : 43232`

A normal (non-`final`) variable can get a new value at any time. You write the type only the first time (`int arbaz = …`). After that, you use just the name (`arbaz = …`).

## Summary

| Type | Holds | Example |
|---|---|---|
| `int` | Whole numbers | `int age = 21;` |
| `float` | Decimals, about 7 digits, needs `f` | `float pi = 3.14f;` |
| `double` | Decimals, about 15–16 digits | `double price = 99.99;` |
| `char` | One character, single quotes | `char grade = 'A';` |
| `boolean` / `Boolean` | `true` or `false` | `boolean ok = true;` |
| `String` | Text, double quotes | `String name = "Arbaz";` |
| `final` | Makes a value constant | `final int MAX = 10;` |

**Next lesson:** [Operators](../Operators/README.md)
