# Python Classes & Objects — The Complete Beginner-to-Expert Guide

Welcome! Think of me as your teacher for this topic. I will not skip steps.
We will go slow, use easy words, use real-life comparisons, and after every
topic you will get **practice scenarios** to build with your own hands.
By the end, you should be able to *explain* this topic in your own words
(theory) AND *build* things with it (practice).

---

## Table of Contents

0. Before We Start — What is OOP and why it exists
1. What is a Class?
2. What is an Object?
3. The `__init__` method and `self`
4. Instance Attributes vs Class Attributes
5. Instance Methods
6. Class Methods and Static Methods
7. Dunder (Magic) Methods
8. Encapsulation — Controlling Access
9. Object Identity, Equality, and Memory
10. Composition — Objects Inside Objects
11. Mini Projects to Practice Everything
12. How to Write Theory Answers (definitions you can memorize)
13. Resources to Go Deeper

---

## 0. Before We Start — What is OOP and Why Does It Exist?

### The problem OOP solves

Before OOP, programmers wrote code in a "list of instructions" style called
**procedural programming**. This works fine for small programs, but as
programs grow, data and the functions that use that data get scattered
everywhere. It becomes messy and hard to manage.

**Object-Oriented Programming (OOP)** is a way of organizing code by
grouping **data** (called attributes/properties) and **behavior** (called
methods/functions) together into one unit called an **object**.

### Real-life analogy

Think about a **car**.

- A car **has data**: color, brand, speed, fuel level.
- A car **can do things**: start, stop, accelerate, brake.

In real life, you don't think of "color" and "start()" as two separate,
unrelated things floating in space — they belong to the car. OOP lets your
code think the same way.

### Procedural vs OOP — same problem, two styles

**Procedural style (data and functions are separate):**
```python
name = "Ali"
balance = 5000

def deposit(balance, amount):
    return balance + amount

balance = deposit(balance, 1000)
print(balance)
```
This works, but imagine 100 bank customers. You'd need 100 separate
variables and keep passing balance around manually. Messy.

**OOP style (data and functions live together):**
```python
class BankAccount:
    def __init__(self, name, balance):
        self.name = name
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

ali_account = BankAccount("Ali", 5000)
ali_account.deposit(1000)
print(ali_account.balance)  # 6000
```
Now every customer is their own self-contained package of data + actions.
This is the whole point of OOP: **real-world modeling, organization, and
reusability.**

### The 4 Pillars of OOP (just an overview for now)

| Pillar | One-line meaning |
|---|---|
| **Encapsulation** | Keep data and the methods that use it bundled together, and control who can change it |
| **Abstraction** | Hide complex details, show only what's necessary to use it |
| **Inheritance** | Let one class reuse and extend another class's code |
| **Polymorphism** | Let different classes respond differently to the same action/method name |

This guide focuses deeply on **Classes and Objects** (the foundation all
four pillars sit on), plus the basics of Encapsulation. Inheritance and
Polymorphism deserve their own dedicated guide once this foundation is
rock-solid — trying to learn everything at once is how people get confused.

### Why this matters for your career

Almost every real-world Python codebase (Django, Flask apps, data science
pipelines with classes like `pandas.DataFrame`, game engines, GUI apps) is
built using classes and objects. If you don't understand this topic deeply,
you will struggle to read professional code, use most libraries properly,
or pass any technical interview.

---

## 1. What is a Class?

### Simple definition

A **class** is a **blueprint** or **template** for creating objects. It
defines *what data* an object will hold and *what actions* it can perform —
but it is not the actual thing itself.

### Real-life analogy

- A **cookie cutter** is the class. The **cookies** made from it are objects.
- An **architectural blueprint** of a house is the class. The actual
  **houses built** from that blueprint are objects.
- The blueprint says "every house will have a door, windows, and a roof" —
  but the blueprint itself is not a house you can live in.

### Syntax

```python
class ClassName:
    # attributes and methods go here
    pass
```

- Class names conventionally start with a **capital letter** and use
  **PascalCase** (e.g., `BankAccount`, `StudentRecord`, `Car`).
- `pass` is a placeholder meaning "nothing here yet" (used for empty classes).

### Example 1 — A simple empty class
```python
class Dog:
    pass
```

### Example 2 — A class with attributes and a method
```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

    def honk(self):
        print("Beep beep!")
```

### Example 3 — A class modeling a Student
```python
class Student:
    def __init__(self, name, roll_number):
        self.name = name
        self.roll_number = roll_number

    def introduce(self):
        print(f"Hi, I am {self.name}, roll number {self.roll_number}.")
```

### Why classes are important
- They let you **model real-world things** in code (students, cars, orders, bank accounts).
- They **avoid repeating code** — write the structure once, reuse it forever.
- They make large programs **organized and maintainable**.
- They are the entry point to using almost every serious Python library.

### 🧪 Practice Scenarios — Classes
Try writing (just the class skeleton, don't worry about objects yet):
1. A `Book` class that will hold a title, author, and number of pages.
2. A `Movie` class that will hold a title, genre, and duration.
3. A `SmartPhone` class that will hold a brand, model, and battery percentage.
4. A `Employee` class that will hold a name, department, and salary.

*(Goal: get comfortable writing the `class Name:` structure before adding logic.)*

---

## 2. What is an Object?

### Simple definition

An **object** (also called an **instance**) is a real, usable thing created
**from** a class. If the class is the blueprint, the object is the actual
built product with real values filled in.

### Creating an object

```python
class Dog:
    pass

my_dog = Dog()      # my_dog is now an OBJECT of class Dog
your_dog = Dog()    # a completely SEPARATE object
```

`my_dog` and `your_dog` are two independent objects — changing one does
not affect the other.

### Example — Multiple objects from one class

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

car1 = Car("Toyota", "Red")
car2 = Car("Honda", "Blue")

print(car1.brand)  # Toyota
print(car2.brand)  # Honda
```

Notice: **one class, many objects, each with its own data.** This is the
core superpower of OOP.

### Checking the type
```python
print(type(car1))          # <class '__main__.Car'>
print(isinstance(car1, Car))  # True
```

### Why objects are important
- Each object keeps its **own copy** of data (like each student has their own name and marks).
- You can create **as many objects as you want** from a single class definition.
- Objects let a program represent **many real-world entities at once** (thousands of users, products, orders — all objects of their respective classes).

### 🧪 Practice Scenarios — Objects
1. Using your `Book` class from before, create 3 different book objects with different titles/authors and print their details.
2. Create 2 `SmartPhone` objects and prove they are independent by changing the battery percentage of one and showing the other is unaffected.
3. Create a list of 5 `Employee` objects and loop through printing each employee's name.

---

## 3. The `__init__` Method and `self`

### The problem without `__init__`

Look at this:
```python
class Car:
    pass

car1 = Car()
car1.brand = "Toyota"   # manually attaching data after creation — messy and error-prone
```

This works but is unreliable — you might forget to set `brand` for one car
and your program breaks later. We need a guaranteed way to set up data
**the moment an object is created**.

### `__init__` — the constructor

`__init__` is a special method that **runs automatically** every time you
create a new object. It's used to set up (initialize) the object's starting
data. "init" is short for "initialize."

```python
class Car:
    def __init__(self, brand, color):
        self.brand = brand
        self.color = color

car1 = Car("Toyota", "Red")  # __init__ runs automatically here
```

You never call `__init__` directly — Python calls it for you the moment
you write `Car("Toyota", "Red")`.

### What is `self`?

`self` refers to **the specific object being created or used**. It is how
an object refers to *itself* inside the class.

**Analogy:** Imagine a form letter template that says "Dear [self], your
balance is [self.balance]." When Ali fills it out, `self` becomes Ali. When
Sara fills it out, `self` becomes Sara. Same template, different person
each time — that's `self`.

```python
class Person:
    def __init__(self, name):
        self.name = name   # "this particular object's" name = the value passed in

    def greet(self):
        print(f"Hello, my name is {self.name}")

p1 = Person("Ali")
p2 = Person("Sara")

p1.greet()   # Hello, my name is Ali
p2.greet()   # Hello, my name is Sara
```

`self.name` inside `greet()` automatically refers to the correct object's
name — Python handles this for you behind the scenes.

### Important rule
`self` must be the **first parameter** of every regular method in a class
(you don't pass it manually — Python passes it automatically).

### Common beginner mistake
```python
class Car:
    def __init__(self, brand):
        self.brand = brand

    def show(self):          # ❌ forgetting self here causes an ERROR
        print(brand)          # ❌ should be self.brand
```
**Fix:**
```python
    def show(self):
        print(self.brand)
```

### More examples

**Example — BankAccount with validation in `__init__`:**
```python
class BankAccount:
    def __init__(self, owner, starting_balance=0):
        self.owner = owner
        self.balance = starting_balance

acc = BankAccount("Ayesha")
print(acc.balance)  # 0 (used the default value)
```

**Example — Rectangle:**
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

r = Rectangle(5, 3)
print(r.area())  # 15
```

### Why `__init__` and `self` matter
- `__init__` guarantees every object starts with **valid, complete data** — no forgetting to set attributes.
- `self` is what makes **one class produce many independent objects** — without it, all objects would share the same data, which defeats the purpose of OOP.
- Understanding `self` deeply is the #1 thing that separates beginners from confident Python OOP programmers.

### 🧪 Practice Scenarios — `__init__` and `self`
1. Build a `Student` class with `__init__(self, name, marks)`. Create 3 students and print each one's marks.
2. Build a `Circle` class with `__init__(self, radius)` and a method `area(self)` that returns `3.14 * radius * radius`.
3. Build a `Login` class with `__init__(self, username, password)` and a method `check_password(self, attempt)` that returns `True` or `False`.
4. On purpose, remove `self` from a method and run the code — read the error message carefully so you recognize it in the future.

---

## 4. Instance Attributes vs Class Attributes

### Instance attributes

These belong to **one specific object**. Defined using `self.` inside
`__init__` (usually). Each object has its own separate copy.

```python
class Dog:
    def __init__(self, name):
        self.name = name   # instance attribute

d1 = Dog("Rex")
d2 = Dog("Bruno")
print(d1.name)  # Rex
print(d2.name)  # Bruno
```

### Class attributes

These belong to **the class itself**, and are **shared by all objects** of
that class. Defined directly inside the class, outside any method.

```python
class Dog:
    species = "Canine"    # class attribute — same for EVERY dog

    def __init__(self, name):
        self.name = name  # instance attribute — different per dog

d1 = Dog("Rex")
d2 = Dog("Bruno")
print(d1.species)  # Canine
print(d2.species)  # Canine  (shared!)
```

### Comparison table

| | Instance Attribute | Class Attribute |
|---|---|---|
| Belongs to | one specific object | the class, shared by all objects |
| Defined | usually with `self.` in `__init__` | directly inside class body |
| Changes affect | only that one object | (usually) all objects, unless overridden |
| Use case | data that differs per object (name, age, balance) | data common to all objects (species, bank interest rate, school name) |

### A very useful real use case — counting objects

```python
class User:
    total_users = 0   # class attribute, shared counter

    def __init__(self, username):
        self.username = username      # instance attribute
        User.total_users += 1         # update the SHARED counter

u1 = User("ali99")
u2 = User("sara_k")
u3 = User("dev_khan")

print(User.total_users)   # 3
```
This is a classic real-world pattern: tracking how many objects have been
created (used in games for "player count," in apps for "total signups," etc).

### ⚠️ Common trap — mutable class attributes
```python
class Team:
    members = []   # ❌ DANGER: shared list across ALL objects!

    def add_member(self, name):
        self.members.append(name)

t1 = Team()
t2 = Team()
t1.add_member("Ali")
print(t2.members)  # ['Ali']  ← Surprise! t2 got affected too!
```
**Fix:** define mutable data (lists, dicts) inside `__init__` as instance attributes:
```python
class Team:
    def __init__(self):
        self.members = []   # ✅ each object gets its own list
```

### Why this distinction matters
- Misunderstanding this is the **#1 source of subtle bugs** in beginner OOP code (the "shared list" trap above is extremely common).
- Knowing when data should be **per-object** vs **shared** is core to correct real-world modeling (e.g., interest rate is same for all bank accounts = class attribute; balance differs per account = instance attribute).

### 🧪 Practice Scenarios — Instance vs Class Attributes
1. Create a `Car` class with a class attribute `wheels = 4` (same for all cars) and instance attributes `brand` and `color`.
2. Create a `School` class where every `Student` object has a class attribute `school_name = "Greenfield High"` shared by all students, but each student has their own `name` and `grade`.
3. Recreate the `User.total_users` counter example above from scratch without looking, then add a `total_users()` printout after creating 5 users.
4. Deliberately build the "shared list bug" above, observe the wrong behavior, then fix it. This exercise alone will save you hours of debugging in the future.

---

## 5. Instance Methods

### Simple definition

A **method** is just a function that lives inside a class and operates on
an object's data (through `self`). "Instance method" = a method meant to be
called on a specific object.

### Syntax
```python
class ClassName:
    def method_name(self, other_params):
        # do something with self.attribute
        pass
```

### Example — Methods that read data
```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def circumference(self):
        return 2 * 3.14159 * self.radius

c = Circle(5)
print(c.area())            # 78.53975
print(c.circumference())   # 31.4159
```

### Example — Methods that change data (state)
```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited {amount}. New balance: {self.balance}")
        else:
            print("Deposit amount must be positive.")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient funds.")
        else:
            self.balance -= amount
            print(f"Withdrew {amount}. New balance: {self.balance}")

acc = BankAccount("Zara", 1000)
acc.deposit(500)     # Deposited 500. New balance: 1500
acc.withdraw(2000)   # Insufficient funds.
```

### Example — A method calling another method of the same object
```python
class Order:
    def __init__(self, price, quantity):
        self.price = price
        self.quantity = quantity

    def subtotal(self):
        return self.price * self.quantity

    def total_with_tax(self, tax_rate=0.1):
        return self.subtotal() * (1 + tax_rate)   # reusing self.subtotal()

o = Order(100, 3)
print(o.total_with_tax())   # 330.0
```

### Why methods matter
- They keep **behavior next to the data it acts on** — instead of a separate `deposit(account, amount)` function floating around, `deposit` naturally belongs to the account.
- They let objects **change their own state safely** and **respond to actions** — this is how you model real-world behavior (a car accelerates, a user logs in, an order gets shipped).
- Methods calling other methods lets you **build complex behavior from small reusable pieces** — a key programming skill.

### 🧪 Practice Scenarios — Instance Methods
1. Add a method `celebrate_birthday(self)` to a `Person` class that increases `self.age` by 1 and prints a message.
2. Build a `Cart` class with a method `add_item(self, item, price)` that stores items in a list, and a method `total(self)` that returns the sum of all prices.
3. Build a `TrafficLight` class with a method `change_color(self)` that cycles the light through "Red" → "Yellow" → "Green" → "Red"...
4. Build a `Player` class for a game with `health = 100`, and methods `take_damage(self, amount)` and `heal(self, amount)`, making sure health never goes below 0 or above 100.

---

## 6. Class Methods and Static Methods

So far every method used `self` (acts on one object). Python also gives you
two other kinds of methods.

### Class Methods — work with the class itself, not one object

Marked with `@classmethod`, and use `cls` instead of `self` (refers to the
**class**, not an object).

**Most common real use: alternative constructors** — extra ways to create
objects.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = 2026 - birth_year
        return cls(name, age)   # cls(...) is the same as Student(...)

s1 = Student("Ali", 20)                          # normal way
s2 = Student.from_birth_year("Sara", 2005)       # alternative way, using birth year
print(s2.age)   # 21
```

This pattern (`from_something`) is used constantly in real Python code —
for example `dict.fromkeys(...)`.

### Static Methods — utility functions that logically belong to the class but don't touch object OR class data

Marked with `@staticmethod`. No `self`, no `cls`.

```python
class MathHelper:
    @staticmethod
    def is_even(number):
        return number % 2 == 0

print(MathHelper.is_even(10))   # True — called without creating an object!
```

### Comparison table

| Type | Decorator | First param | Can access object data? | Can access class data? | Typical use |
|---|---|---|---|---|---|
| Instance method | (none) | `self` | ✅ | ✅ | normal object behavior |
| Class method | `@classmethod` | `cls` | ❌ | ✅ | alternative constructors, class-wide operations |
| Static method | `@staticmethod` | (none) | ❌ | ❌ | utility/helper functions related to the class's purpose |

### More examples

```python
class Pizza:
    def __init__(self, toppings):
        self.toppings = toppings

    @classmethod
    def margherita(cls):
        return cls(["cheese", "tomato"])   # a preset "recipe" constructor

    @classmethod
    def pepperoni(cls):
        return cls(["cheese", "pepperoni"])

    @staticmethod
    def is_valid_topping(topping):
        allowed = ["cheese", "tomato", "pepperoni", "mushroom", "olive"]
        return topping in allowed

p = Pizza.margherita()
print(p.toppings)                         # ['cheese', 'tomato']
print(Pizza.is_valid_topping("cheese"))   # True
```

### Why this matters
- Class methods let you offer **multiple sensible ways to build an object** (from a string, from a dict, from a birth year, from a preset "recipe") — very common in real libraries (`datetime.fromtimestamp()`, `dict.fromkeys()`).
- Static methods keep **related helper logic organized inside the class** instead of scattered as loose functions, improving readability.

### 🧪 Practice Scenarios — Class & Static Methods
1. Add a `@classmethod` called `from_string` to a `Student` class that takes `"Ali-20"` and splits it into name and age.
2. Build a `Temperature` class storing Celsius, with a `@staticmethod` called `celsius_to_fahrenheit(c)` and a `@classmethod` `from_fahrenheit(cls, f)` that creates a `Temperature` object.
3. Build a `Employee` class with class methods for creating a `manager()` (fixed department "Management") and a `intern()` (fixed salary 0).

---

## 7. Dunder (Magic) Methods

"Dunder" = **D**ouble **UNDER**score, like `__init__`, `__str__`. These are
special methods Python calls automatically in certain situations (printing,
comparing, adding, measuring length, etc). They let your custom objects
behave like Python's built-in types.

### `__str__` — human-readable printing

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

p = Point(3, 4)
print(p)          # (3, 4)   — instead of the default ugly <__main__.Point object at 0x...>
```

### `__repr__` — developer/debug-friendly representation

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __repr__(self):
        return f"Point(x={self.x}, y={self.y})"

p = Point(3, 4)
p             # in a console/notebook: Point(x=3, y=4)
```
**Rule of thumb:** `__str__` is for end users (nice display), `__repr__` is
for developers/debugging (unambiguous detail). If you only define one,
define `__repr__` — Python falls back to it for `print()` too.

### `__eq__` — custom equality (`==`)

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

p1 = Point(1, 2)
p2 = Point(1, 2)
print(p1 == p2)   # True — without __eq__, this would be False (see Section 9)
```

### `__add__` — operator overloading (`+`)

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
print(p1 + p2)    # (4, 6)   — the + symbol now works on our own objects!
```

### `__len__` — makes `len()` work on your object

```python
class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        return len(self.songs)

pl = Playlist(["Song A", "Song B", "Song C"])
print(len(pl))    # 3
```

### A short reference table of common dunder methods

| Method | Triggered by | Purpose |
|---|---|---|
| `__init__` | `ClassName(...)` | initialize a new object |
| `__str__` | `print(obj)`, `str(obj)` | friendly display text |
| `__repr__` | typing `obj` in console, `repr(obj)` | unambiguous debug text |
| `__eq__` | `obj1 == obj2` | define what "equal" means |
| `__lt__` | `obj1 < obj2` | define what "less than" means (enables sorting) |
| `__len__` | `len(obj)` | define a "length" for the object |
| `__add__` | `obj1 + obj2` | define what "+" does |
| `__getitem__` | `obj[index]` | make the object indexable like a list |

### Why dunder methods matter
- They let your custom classes **feel like native Python types** — printable, comparable, addable, sortable.
- This is heavily used in real libraries: `pandas.DataFrame` overloads `+`, `[]`, `len()`, etc. Understanding dunders is what lets you read and eventually **write your own libraries**.

### 🧪 Practice Scenarios — Dunder Methods
1. Give your `Rectangle` class a `__str__` method that prints `"Rectangle(5 x 3)"`.
2. Give your `Point` class a `__eq__` and test comparing two points with the same coordinates.
3. Build a `Money` class storing an amount, and implement `__add__` (add two Money objects) and `__str__` (print as `"$50"`).
4. Build a `Playlist` class and implement `__len__` and `__getitem__` so you can do `len(playlist)` and `playlist[0]`.

---

## 8. Encapsulation — Controlling Access to Data

### Simple definition

**Encapsulation** means bundling data and methods together, AND
**restricting direct outside access** to some of that data — forcing people
to go through controlled methods instead.

### Real-life analogy

Think of an **ATM machine**. You can't reach in and directly grab cash from
the vault. You must go through the ATM's controlled interface (insert card,
enter PIN, request withdrawal) — the machine validates everything before
letting money out. That controlled interface *is* encapsulation.

### Three levels of "privacy" in Python (by convention)

| Prefix | Name | Meaning |
|---|---|---|
| `name` | Public | Anyone can access/change it freely |
| `_name` | Protected (convention only) | "Please don't touch this from outside" — but Python doesn't enforce it |
| `__name` | Private (name-mangled) | Python actively makes it hard to access directly from outside |

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner          # public
        self._pin = "1234"          # protected (convention: internal use)
        self.__balance = balance    # private (name-mangled)

acc = BankAccount("Ali", 1000)
print(acc.owner)          # ✅ works fine — public
print(acc._pin)           # ⚠️ works, but you're "not supposed to" touch this
print(acc.__balance)      # ❌ AttributeError! Python hid this name
```

### Why hide `__balance`? Because we want controlled access:

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance     # private

    def deposit(self, amount):
        if amount <= 0:
            print("Amount must be positive.")
            return
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount("Ali", 1000)
acc.deposit(-500)              # rejected safely: "Amount must be positive."
print(acc.get_balance())       # 1000 — protected from invalid direct changes
```
Without encapsulation, someone could do `acc.balance = -99999999` directly
and break the whole system. Encapsulation prevents this by forcing changes
through validated methods.

### The Pythonic way — `@property`

Instead of writing `get_balance()` / `set_balance()` manually, Python gives
you `@property` to make a method **look like a normal attribute** while
still running validation logic.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.__balance = balance

    @property
    def balance(self):          # acts like reading an attribute
        return self.__balance

    @balance.setter
    def balance(self, value):   # acts like setting an attribute, but validated
        if value < 0:
            raise ValueError("Balance cannot be negative!")
        self.__balance = value

acc = BankAccount("Ali", 1000)
print(acc.balance)     # 1000   — looks like a normal attribute, no parentheses!
acc.balance = 2000      # ✅ goes through the validated setter
acc.balance = -50       # ❌ raises ValueError automatically
```

### Why encapsulation matters
- It **protects data from invalid states** (negative balance, negative age, empty username).
- It lets you **change internal implementation later** without breaking code that uses your class (you can change how `balance` is stored internally, and users of your class won't even notice, because they always interacted through the property/method).
- It is a **core professional coding habit** — production code almost never allows raw, unrestricted access to important internal data.

### 🧪 Practice Scenarios — Encapsulation
1. Build a `Person` class with a private `__age`, and a `@property age` getter, and a setter that rejects negative ages.
2. Build a `Product` class with a private `__price`, and a setter that rejects prices of 0 or below.
3. Build a `Password` class that stores a private `__password` and provides a method `check(self, attempt)` — never expose the raw password directly.

---

## 9. Object Identity, Equality, and Memory

### `id()` — every object has a unique identity

```python
p1 = Point(1, 2)
p2 = Point(1, 2)
print(id(p1))   # some unique number, e.g. 140718392
print(id(p2))   # a DIFFERENT unique number
```
Even though `p1` and `p2` hold the *same data*, they are **two separate
objects** living at different memory locations.

### `is` vs `==`

- `is` checks: **"are these literally the same object in memory?"**
- `==` checks: **"do these count as equal in value?"** (uses `__eq__` if defined)

```python
p1 = Point(1, 2)
p2 = Point(1, 2)
p3 = p1

print(p1 == p2)   # depends on __eq__ (True if defined properly, False by default)
print(p1 is p2)   # False — different objects
print(p1 is p3)   # True  — p3 is literally the SAME object as p1
```

### Why this matters practically

```python
p1 = Point(1, 2)
p3 = p1          # p3 now points to the SAME object as p1, not a copy!
p3.x = 999
print(p1.x)       # 999  — because p1 and p3 are the exact same object
```
This trips up beginners a lot: assigning an object to a new variable does
**not** create a new copy — both names point to the same object in memory.

### Why this matters
- Understanding `is` vs `==` avoids subtle bugs, especially with `None` checks (`if x is None:` is the correct Python style, not `if x == None:`).
- Understanding that variables are **references** to objects (not the objects themselves) is essential before you touch mutable data, function arguments, or copying objects correctly.

### 🧪 Practice Scenarios — Identity & Equality
1. Create two `Student` objects with identical data and check `==` before and after adding `__eq__`.
2. Assign one object to two variable names, mutate it through one name, and observe the change through the other name. Explain in your own words why this happens.
3. Write a short paragraph (theory practice!) explaining the difference between `is` and `==` using your own analogy (not the one from this guide).

---

## 10. Composition — Objects Inside Objects

### Simple definition

**Composition** means building a class using **other objects as its
attributes**. This models "has-a" relationships (a Car *has an* Engine, a
House *has a* Kitchen).

```python
class Engine:
    def __init__(self, horsepower):
        self.horsepower = horsepower

    def start(self):
        print("Engine roaring to life!")

class Car:
    def __init__(self, brand, horsepower):
        self.brand = brand
        self.engine = Engine(horsepower)   # Car "has an" Engine — composition!

    def start(self):
        print(f"{self.brand} starting...")
        self.engine.start()

car = Car("Toyota", 300)
car.start()
# Toyota starting...
# Engine roaring to life!
```

### Another example — Library system

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

class Library:
    def __init__(self):
        self.books = []            # a Library "has" many Books

    def add_book(self, book):
        self.books.append(book)

    def list_books(self):
        for book in self.books:
            print(f"{book.title} by {book.author}")

lib = Library()
lib.add_book(Book("1984", "George Orwell"))
lib.add_book(Book("Dune", "Frank Herbert"))
lib.list_books()
```

### Why composition matters
- It reflects how **real-world things are naturally built from smaller parts** — modeling this accurately makes your code intuitive and organized.
- It's often **preferred over inheritance** in modern software design (the principle "favor composition over inheritance") because it creates more flexible, less tangled relationships between classes.

### 🧪 Practice Scenarios — Composition
1. Build a `Kitchen` class and a `House` class where `House` contains a `Kitchen` object.
2. Build an `Order` class that contains a list of `Product` objects, and a method `total_cost(self)` that sums each product's price.
3. Build a `Team` class containing a list of `Player` objects, with a method `average_score(self)`.

---

## 11. Mini Projects — Practice Everything Together

Once you're comfortable with sections 1–10, build these full mini-projects.
They force you to combine `__init__`, methods, class attributes,
encapsulation, and dunder methods in one place — which is exactly how real
code is written.

1. **Library Management System** — `Book` and `Library` classes. Add books, remove books, search by title, track total books borrowed (class attribute).
2. **Bank System** — `BankAccount` class with private balance, deposit/withdraw methods, a `Bank` class holding multiple accounts, and transfer-between-accounts logic.
3. **Student Result Management** — `Student` class storing subject marks (a dict), methods to calculate average, highest, and pass/fail status.
4. **E-commerce Cart** — `Product` and `Cart` classes. Add/remove items, apply a discount code, calculate total with tax.
5. **Contact Book** — `Contact` and `ContactBook` classes. Add, search, delete, and list contacts sorted alphabetically (use `__lt__` for sorting!).
6. **Simple Zoo Simulation** — `Animal` class (base data), individual animal objects (Lion, Elephant) built via composition or attributes, `Zoo` class holding all animals with a `feed_all()` method.

For each project: write the class, create several objects, use `__str__`
to display them nicely, and add at least one validation rule using
encapsulation (e.g., can't withdraw more money than you have, can't add a
negative-priced product).

---

## 12. How to Write Theory Answers (Definitions to Memorize & Practice Explaining)

Being an "expert" means you can both **code it** and **explain it in
words** clearly — for interviews, exams, or teaching others. Practice
writing short answers like these in your own words:

> **Q: What is a class?**
> A class is a blueprint or template that defines the attributes (data) and
> methods (behavior) that its objects will have. It does not hold real
> data itself — it only describes the structure.

> **Q: What is an object?**
> An object is a specific instance created from a class, with its own real
> values stored in memory. Many objects can be created from one class,
> each independent of the others.

> **Q: What is `self`?**
> `self` is a reference to the specific object a method is currently being
> called on. It lets each object access and modify its own data separately
> from other objects of the same class.

> **Q: What is the difference between a class attribute and an instance attribute?**
> A class attribute is shared by all objects of the class, while an
> instance attribute belongs to one specific object and can differ between
> objects.

> **Q: What is `__init__` used for?**
> `__init__` is a constructor method that runs automatically when a new
> object is created. It is used to initialize the object's starting
> attributes.

> **Q: What is encapsulation?**
> Encapsulation is the practice of bundling data and the methods that
> operate on it together, while restricting direct outside access to some
> data to protect it from invalid changes — typically through private
> attributes and controlled methods or properties.

> **Q: What is the difference between `is` and `==`?**
> `is` checks whether two variables refer to the exact same object in
> memory, while `==` checks whether two objects are considered equal in
> value (which can be customized with `__eq__`).

> **Q: What is a dunder/magic method?**
> A dunder method is a special method with double underscores (like
> `__init__` or `__str__`) that Python calls automatically in certain
> situations, allowing custom objects to behave like built-in types (e.g.,
> support printing, comparison, or arithmetic operators).

**Practice tip:** After finishing each section above, close the guide and
try writing a 2–3 sentence explanation of that topic completely from
memory, in your own words. If you struggle, that tells you exactly what to
re-read.

---

## 13. Resources to Go Deeper

- **Official Python Docs — Classes:** https://docs.python.org/3/tutorial/classes.html (the authoritative source, written by Python's own maintainers)
- **Official Python Docs — Data Model (all dunder methods):** https://docs.python.org/3/reference/datamodel.html
- **Real Python — OOP in Python 3:** https://realpython.com/python3-object-oriented-programming/ (excellent, beginner-friendly, example-heavy)
- **Corey Schafer's OOP YouTube series** — search "Corey Schafer Python OOP" — widely recommended for visual/video learners, covers everything in this guide plus inheritance.
- **Practice coding platforms:** HackerRank (OOP section), LeetCode (for applying OOP in problem-solving), Exercism.org (has a dedicated Python track with mentor feedback).
- **Book:** *"Python Crash Course" by Eric Matthes* — has an excellent classes chapter with projects, great for beginners.
- **Book (once comfortable):** *"Fluent Python" by Luciano Ramalho* — goes deep into dunder methods and how Python's own object model works internally; this is more advanced/intermediate.

---

