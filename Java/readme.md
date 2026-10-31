# Java Cheat Sheet

## Basic Syntax

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- `public` — Accessible from anywhere.
- `static` — Belongs to the class.
- `void` — Does not return a value.
- `main()` — Entry point of a Java program.

## Data Types

```java
int age = 20;
long population = 8000000L;
float price = 10.5f;
double salary = 50000.50;
char grade = 'A';
boolean isJavaFun = true;
String name = "Java";
```

| Type | Description |
|---|---|
| `int` | Integer numbers |
| `long` | Large integer numbers |
| `float` | Decimal numbers |
| `double` | Double-precision decimal numbers |
| `char` | Single character |
| `boolean` | `true` or `false` |
| `String` | Sequence of characters |

## Variables & Constants

```java
int x = 10;
String name = "John";

final int MAX_VALUE = 100;
```

- `final` — Prevents reassignment of a variable.
- `static` — Creates a class-level variable or method.

## Type Casting

```java
// Widening (automatic)
int a = 10;
double b = a;

// Narrowing (manual)
double x = 9.8;
int y = (int) x;
```

## Operators

| Operator | Description |
|---|---|
| `+` `-` `*` `/` `%` | Arithmetic |
| `==` `!=` `>` `<` `>=` `<=` | Comparison |
| `&&` `\|\|` `!` | Logical |
| `=` `+=` `-=` `*=` `/=` | Assignment |
| `++` `--` | Increment / Decrement |
| `&` `\|` `^` `~` `<<` `>>` | Bitwise |

## User Input

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);

int age = sc.nextInt();
double price = sc.nextDouble();
String word = sc.next();

// Read a complete line after nextInt/next
sc.nextLine();
String fullName = sc.nextLine();

sc.close();
```

## Control Flow

### Conditional Statements

```java
if (a > b) {
    // code
} else if (a == b) {
    // code
} else {
    // code
}
```

### Ternary Operator

```java
// condition ? valueIfTrue : valueIfFalse

int age = 20;
String result = age >= 18 ? "Adult" : "Minor";
```

### Switch Statement

```java
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

### Loops

```java
// For loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// While loop
while (i < 5) {
    i++;
}

// Do-while loop
do {
    i++;
} while (i < 5);

// Enhanced for loop
for (String name : names) {
    System.out.println(name);
}
```

### Loop Control

```java
break;     // Exit the loop
continue;  // Skip current iteration
```

## Methods

```java
static int add(int a, int b) {
    return a + b;
}

// Method call
int result = add(10, 20);
```

- `void` — Method does not return a value.
- `return` — Returns a value from a method.
- Method overloading — Multiple methods with the same name but different parameters.

## Object-Oriented Programming (OOP)

### Classes and Objects

```java
class Car {
    String color = "Red";

    void drive() {
        System.out.println("Car is moving");
    }
}

Car myCar = new Car();
myCar.drive();
```

### Constructors

```java
class Car {
    String model;

    Car() {
        this.model = "Default";
    }

    Car(String model) {
        this.model = model;
    }
}
```

### Getters and Setters

```java
class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

### Inheritance

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Bark");
    }
}
```

### Polymorphism

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}

Animal myDog = new Dog();
myDog.sound();  // Bark
```

### Abstraction

```java
abstract class Animal {
    abstract void sound();

    void sleep() {
        System.out.println("Sleeping");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

### Interface

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}
```

## Access Modifiers

| Modifier | Accessibility |
|---|---|
| `public` | Accessible everywhere |
| `private` | Within the same class |
| `protected` | Same package and subclasses |
| Default | Within the same package |

## Generics

Generics allow classes, interfaces and methods to work with different data types while maintaining type safety.

### Generic Class

```java
class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

// Usage
Box<String> box = new Box<>();
box.set("Java");

System.out.println(box.get());
```

### Generic Method

```java
public static <T> void print(T value) {
    System.out.println(value);
}

// Usage
print("Hello");
print(100);
```

### Generic Types

| Symbol | Meaning |
|---|---|
| `T` | Type |
| `E` | Element |
| `K` | Key |
| `V` | Value |
| `N` | Number |

### Bounded Generics

Restrict the type that can be used.

```java
class Calculator<T extends Number> {
    T value;

    Calculator(T value) {
        this.value = value;
    }
}
```

### Wildcards

```java
List<?> list;                  // Any type
List<? extends Number> list;   // Number or its subclasses
List<? super Integer> list;    // Integer or its supertypes
```

- `?` — Unknown type.
- `? extends T` — Accepts T or its subclasses.
- `? super T` — Accepts T or its parent types.

## Exception Handling

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println(e.getMessage());
} finally {
    System.out.println("Execution completed");
}
```

### Throw & Throws

```java
// Explicitly throw an exception
throw new IllegalArgumentException("Invalid input");

// Declare a possible exception
void readFile() throws IOException {
    // code
}
```

- `try` — Contains code that may cause an exception.
- `catch` — Handles an exception.
- `finally` — Executes after try/catch.
- `throw` — Explicitly throws an exception.
- `throws` — Declares possible exceptions.

## Collections Framework

### List

Ordered collection that allows duplicates.

```java
import java.util.ArrayList;
import java.util.List;

List<String> names = new ArrayList<>();

names.add("John");
names.add("Alex");
names.get(0);
names.set(0, "Sam");
names.remove("Alex");
names.size();
names.contains("John");
```

### Set

Stores unique elements without duplicates.

```java
import java.util.HashSet;
import java.util.Set;

Set<Integer> numbers = new HashSet<>();

numbers.add(10);
numbers.add(20);
numbers.add(10);  // Duplicate ignored

numbers.contains(10);
numbers.remove(20);
numbers.size();
```

### Map

Stores data as key-value pairs. Keys are unique.

```java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> users = new HashMap<>();

users.put("John", 25);
users.put("Alex", 22);

users.get("John");
users.containsKey("Alex");
users.remove("John");
users.size();
```

### Common Collection Methods

| Method | Description |
|---|---|
| `add()` | Add an element |
| `get()` | Retrieve an element |
| `set()` | Update an element |
| `remove()` | Remove an element |
| `contains()` | Check if an element exists |
| `size()` | Get collection size |
| `isEmpty()` | Check if collection is empty |
| `clear()` | Remove all elements |

## Common Java 8 Features

### 1. Lambda Expressions

A shorter way to write implementations of functional interfaces.

```java
// Basic lambda
(a, b) -> a + b

// Single parameter
name -> System.out.println(name)

// Multiple statements
(a, b) -> {
    int sum = a + b;
    return sum;
}
```

### 2. Functional Interfaces

An interface containing exactly one abstract method.

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

Calculator calc = (a, b) -> a + b;

System.out.println(calc.add(10, 20));
```

**Common Functional Interfaces**

| Interface | Description | Example |
|---|---|---|
| `Predicate<T>` | Takes input and returns boolean | `n -> n > 10` |
| `Function<T, R>` | Takes input and returns a result | `n -> n * 2` |
| `Consumer<T>` | Takes input, returns nothing | `n -> System.out.println(n)` |
| `Supplier<T>` | Returns a value without input | `() -> "Hello"` |

```java
Predicate<Integer> isEven = n -> n % 2 == 0;

Function<Integer, Integer> square = n -> n * n;

Consumer<String> print = s -> System.out.println(s);

Supplier<String> message = () -> "Hello Java";
```

### 3. Stream API

Used to process collections without writing traditional loops.

```java
import java.util.*;
import java.util.stream.Collectors;

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
```

**Common Stream Methods**

| Method | Description |
|---|---|
| `stream()` | Create a stream |
| `filter()` | Filter elements |
| `map()` | Transform elements |
| `sorted()` | Sort elements |
| `distinct()` | Remove duplicates |
| `limit()` | Limit the number of elements |
| `forEach()` | Perform an action on each element |
| `collect()` | Collect results into a collection |
| `count()` | Count elements |
| `findFirst()` | Get the first matching element |
| `anyMatch()` | Check if any element matches a condition |
| `reduce()` | Combine elements into one result |

**Stream Examples**

```java
// Filter even numbers
numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println);

// Transform numbers into squares
numbers.stream()
       .map(n -> n * n)
       .forEach(System.out::println);

// Collect results into a List
List<Integer> evenNumbers = numbers.stream()
       .filter(n -> n % 2 == 0)
       .collect(Collectors.toList());

// Sort numbers
numbers.stream()
       .sorted()
       .forEach(System.out::println);

// Count matching elements
long count = numbers.stream()
       .filter(n -> n > 2)
       .count();

// Find the first matching element
Optional<Integer> result = numbers.stream()
       .filter(n -> n > 3)
       .findFirst();
```

### Stream with Objects

Useful for filtering objects and extracting their properties.

```java
class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

List<User> users = Arrays.asList(
    new User("John", 22),
    new User("Alex", 17),
    new User("Sam", 25)
);

// Get names of users aged 18 or above
List<String> adultNames = users.stream()
       .filter(user -> user.getAge() >= 18)
       .map(User::getName)
       .collect(Collectors.toList());
```

### 4. Method References

A shorter alternative to certain lambda expressions.

```java
// Lambda
names.forEach(name -> System.out.println(name));

// Method reference
names.forEach(System.out::println);
```

### 5. Default & Static Methods in Interfaces

Interfaces can contain methods with implementations.

```java
interface Animal {
    default void sound() {
        System.out.println("Animal sound");
    }

    static void info() {
        System.out.println("Animal interface");
    }
}
```

### 6. Optional Class

Helps handle values that might be absent.

```java
Optional<String> name = Optional.of("Java");

System.out.println(name.isPresent());
System.out.println(name.orElse("Unknown"));

name.ifPresent(System.out::println);
```

### 7. Date & Time API

Java 8 introduced the `java.time` package.

```java
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;

LocalDate date = LocalDate.now();
LocalTime time = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.now();

LocalDate tomorrow = date.plusDays(1);
```

## Input / Output

### Scanner

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);

int number = sc.nextInt();
String text = sc.nextLine();

sc.close();
```

### File I/O

```java
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

// Read a file
File file = new File("input.txt");

try (Scanner reader = new Scanner(file)) {
    while (reader.hasNextLine()) {
        System.out.println(reader.nextLine());
    }
} catch (IOException e) {
    e.printStackTrace();
}

// Write to a file
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write("Hello Java");
} catch (IOException e) {
    e.printStackTrace();
}
```

## Useful Keywords & Concepts

- `this` — Refers to the current object.
- `super` — Refers to the parent class.
- `static` — Belongs to the class.
- `final` — Prevents reassignment, overriding or inheritance depending on its use.
- `new` — Creates an object.
- `instanceof` — Checks an object's type.
- `null` — Represents the absence of an object reference.
- `@Override` — Indicates that a method overrides another method.
- `extends` — Inherits a class.
- `implements` — Implements an interface.
- `abstract` — Declares an incomplete class or method.
- `package` — Organizes related classes.
- `import` — Imports classes and packages.

## Common Java Commands

```bash
javac Main.java       # Compile Java source code
java Main             # Run the compiled class
java -version         # Check Java version
javac -version        # Check compiler version
```
