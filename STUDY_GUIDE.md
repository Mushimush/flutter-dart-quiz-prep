# MAD Quiz Study Guide — Flutter & Dart for Absolute Beginners

> **Goal:** By the end of this guide, you should recognize every concept the quiz tests and know *why* each correct answer is correct — not just memorize.

---

## How to Use This Guide

1. **Read Part 1** (Concepts) — learn the ideas.
2. **Read Part 2** (Cheat Sheet) — keep this open during practice.
3. **Read Part 3** (Quiz Answer Key with Reasoning) — verify your understanding.
4. **Quick-recap the bold rules at the bottom** the night before.

---

# PART 1 — THE 9 KEY CONCEPTS

---

## Concept 1: What is Flutter? What is Dart?

**The big idea.** These are two different things that work together:

| | What it is | Made by |
|---|---|---|
| **Dart** | A programming **language** (like English) | Google |
| **Flutter** | A UI **framework / toolkit** built using Dart | Google |

- You **write Dart code** that **uses Flutter** to build apps.
- **One Dart codebase → runs on Android, iOS, Web, Windows, macOS, Linux.** That's called **cross-platform**.
- **Both are open source.**
- **DartPad** (dartpad.dev) lets you try **both Dart and Flutter** online — no installation.
- Dart is a **pure object-oriented language** — *everything in Dart is an object* (even numbers, booleans, null).

**Analogy:** Dart is the *language* (English). Flutter is the *screenplay-writing kit* that uses that language. You write Dart sentences; Flutter gives you the stage, lights, and actors.

**Beginner pitfall:** Saying "I'm coding in Flutter." → You code in **Dart**, using the **Flutter** framework.

---

## Concept 2: Dart Entry Point — `void main()`

Every Dart program starts at a function named exactly **`main`**:

```dart
void main() {
  // your program starts here
}
```

**Rules:**
- Lowercase `m` → `main`, not `Main`.
- Return type is `void`, not `Void`.
- Curly braces `{}` for the function body.

**Only `void main() {}` is valid.** `Void Main()`, `void Main()`, `Void main()` are all WRONG (Dart is case-sensitive).

---

## Concept 3: Dart Variables & Types

### The four ways to declare a variable

```dart
var name = 'Alex';           // Dart infers the type
String name2 = 'Alex';       // you specify the type
final age = 30;              // set ONCE, cannot change
const pi = 3.14;             // compile-time constant
```

### CRITICAL rule about `final`

```dart
final e;       // ❌ COMPILE ERROR
e = 10;        // too late — final must be initialized at declaration
```
Fix: `final e = 10;`

### Types are strict

- `int` (whole: `5`) and `double` (decimal: `5.0`) are **different types**.
- `int i = 5;` → `i` is an `int`, **not also a double**.
- `double d = 5.0;` → `d` is a `double`, **not also an int**.

### Booleans must be `bool` with literal `true`/`false`

```dart
bool isValid = true;       // ✅ correct
bool isValid = "true";     // ❌ that's a String
bool isValid = 1;          // ❌ that's an int
boolean isValid = false;   // ❌ keyword is "bool" not "boolean"
```

### Strings — single OR double quotes

```dart
var s = 'Hi';         // ✅ String
var s = "Hi";         // ✅ String
String s = "Hi";      // ✅ String
var s = {"Hi"};       // ❌ THIS IS A SET, NOT A STRING — curly braces make a Set
```

### String interpolation

```dart
var name = 'Sam';
var age = 21;
print('Hi $name, next year: ${age + 1}');
// Hi Sam, next year: 22
```
- `$variable` → drop in a variable.
- `${expression}` → drop in a calculation (needs curly braces).

### Parsing strings into numbers

```dart
int.parse('11')        // → 11 (int)
double.parse('11.8')   // → 11.8 (double)
```

---

## Concept 4: Dart Collections

Three "containers" — tell them apart by their **brackets**:

| Type | Looks like | Purpose |
|---|---|---|
| **List** | `[1, 2, 3]` | Ordered list (duplicates OK) |
| **Set** | `{1, 2, 3}` | Unique items |
| **Map** | `{'name': 'Sam', 'age': 21}` | Key → value pairs |

**Trick to remember Map vs Set:** if it has `key: value` pairs, it's a Map. If it's just bare values in `{}`, it's a Set.

```dart
var r = {'Betty': 10, 'Allan': 30};   // ✅ this is a MAP
```

---

## Concept 5: Null Safety `??`

In Dart, normal variables **cannot be null**. To allow null, add `?` to the type:

```dart
int? x;        // x can be null
int y = 40;
var val = x ?? y;       // if x is null, use y
print(val);             // → 40
```

`??` = "use the left side, but if it's null, use the right side." Like a backup plan.

---

## Concept 6: Dart Functions — Positional vs Named Parameters

### Positional parameters — order matters

```dart
int add(int a, int b) => a + b;
add(9, 10);    // a=9, b=10
```

### Named parameters — wrap in `{}` in declaration, use `name:` when calling

```dart
void greet({required String name, int age = 0}) { ... }
greet(name: 'Sam', age: 21);    // ✅
greet(name: 'Sam');             // ✅ age defaults to 0
greet('Sam');                   // ❌ named params need the label
```

### Mixed: positional first, then named

```dart
void getResult(String operator, int n1, {int n2 = 1}) { ... }

getResult('+', 9, 10);          // ✅ all positional, n2=10
getResult('sqrt', 9);           // ✅ n2 defaults to 1
getResult('max', n2: 10);       // ❌ missing required positional n1
getResult(100, n2: 101, 'min'); // ❌ positional must come BEFORE named
```

---

## Concept 7: Flutter Widgets — Stateless vs Stateful

**Everything in Flutter is a Widget.** A widget is a description of a piece of UI.

| | StatelessWidget | StatefulWidget |
|---|---|---|
| Changes after build? | ❌ Never | ✅ Yes |
| Example | `Text` | `TextField` |
| Where `build()` lives | In the widget class itself | In the **State** class (NOT the widget class) |
| Analogy | Printed photo | Digital photo frame |

### `build()` — where the UI is drawn

- For **StatelessWidget**: `build()` is overridden inside the widget class.
- For **StatefulWidget**: `build()` is overridden inside the **State** subclass.

```dart
class Hello extends StatelessWidget {
  Widget build(BuildContext c) => Text('Hi');   // build lives HERE
}

class Counter extends StatefulWidget {
  State<Counter> createState() => _CounterState();  // no build here
}
class _CounterState extends State<Counter> {
  Widget build(BuildContext c) => Text('count');    // build lives HERE
}
```

### `runApp()` — starts the app

```dart
void main() {
  runApp(MyApp());     // ✅ takes a WIDGET
  runApp(Text('Hi'));  // ✅ also a widget
  runApp('Hi');        // ❌ Strings are NOT widgets
}
```

---

## Concept 8: Common Widgets & Their Key Parameters

| Widget | Key parameter | Notes |
|---|---|---|
| `MaterialApp` | **`home:`** | The root screen of your app |
| `Scaffold` | **`appBar:`**, `body:` | Page layout — `appBar` goes on Scaffold, not MaterialApp |
| `Center` | **`child:`** (singular) | Centers ONE child |
| `Container` | **`child:`** (singular) | A flexible box (padding, color, size) |
| `Row` | **`children:`** (plural) | Horizontal layout — takes a list `[...]` |
| `Column` | **`children:`** (plural) | Vertical layout — takes a list `[...]` |
| `Text` | first arg is the text | **Stateless** — for display only |
| `TextField` | `controller:` | **Stateful** — for user input |
| `FilledButton`, `TextButton`, `OutlinedButton` | **`onPressed:`** (required), **`child:`** (required) | Always need both |

### `child:` vs `children:` — the #1 quiz trick

- **`child:` (singular)** → ONE widget. Used by `Center`, `Container`, all buttons.
- **`children:` (plural)** → a LIST of widgets in `[]`. Used by `Row`, `Column`.

```dart
Center(child: Text('Solo'));            // singular
Column(children: [Text('A'), Text('B')]);  // plural with []
```

### Buttons require BOTH `onPressed` AND `child`

```dart
OutlinedButton(child: Text('Submit'), onPressed: () {});   // ✅
OutlinedButton(onLongPress: () {}, child: Text('Reset'));  // ❌ missing onPressed
```

---

## Concept 9: TextField & TextEditingController

How to **read** what the user typed into a TextField:

```dart
final _nameController = TextEditingController();

// Attach to the TextField:
TextField(controller: _nameController);

// Read the typed text:
print(_nameController.text);      // ✅ .text gives you the input

// Clear the typed text:
_nameController.text = '';        // ✅ empty string clears it
```

**There is no `.value`, `.number`, or `.string` property — only `.text`.**

Because the contents change as the user types, **TextField is a StatefulWidget**.

---

# PART 2 — CHEAT SHEET (Memorize These!)

| Fact | Answer |
|---|---|
| Entry point | `void main() {}` (lowercase) |
| Open source? | **Both** Flutter and Dart |
| Cross-platform? | Yes — Android, iOS, Web, Windows, macOS, Linux |
| `Text` is | **Stateless** |
| `TextField` is | **Stateful** |
| `runApp()` needs | A **Widget** (not a String) |
| Build method for StatefulWidget lives in | The **State** class |
| `home:` belongs to | **MaterialApp** |
| `appBar:` belongs to | **Scaffold** |
| `child:` (singular) used by | Center, Container, Buttons |
| `children:` (plural, list) used by | Row, Column |
| Get TextField input | `controller.text` |
| Clear TextField input | `controller.text = '';` |
| Buttons require | Both `onPressed` and `child` |
| `final x;` then `x = 10;` | ❌ Compile error |
| `int` and `double` | Are **different types** |
| `bool` literal | `true` or `false` (not `"true"`, not `1`) |
| `{'key': value}` is a | **Map** |
| `{'value'}` (no key) is a | **Set** (NOT a String!) |
| `'Hi'` or `"Hi"` | Both valid Strings |
| Dart is pure OOP | **True** — everything is an object |
| `x ?? y` means | "use x, but if x is null, use y" |

---

# PART 3 — ANSWER KEY (with reasoning)

| # | Question (short form) | Answer | Why |
|---|---|---|---|
| 1 | Is `Text` a StatefulWidget? | **false** | `Text` extends `StatelessWidget` — its content doesn't change after build. |
| 2 | Is `FilledButton`'s `onPressed` required? | **true** | Required named parameter (passing `null` disables the button, but you must pass it). |
| 3 | Is `TextField` a StatefulWidget? | **true** | The text inside changes as the user types — needs state. |
| 4 | Is `TextButton`'s `child` required? | **true** | A button must have something inside to display. |
| 5 | Flutter is a low-code framework for cross-platform apps. | **false** | Flutter is a full SDK, not low-code/no-code. (Note: it IS cross-platform — but it's not "low-code".) |
| 6 | Dart only works on Android/Windows/Web, NOT iOS. | **false** | Dart/Flutter fully supports iOS. |
| 7 | Flutter develops high-performance native apps for Android and iOS. | **true** | Compiles to native ARM/x64 code on both. |
| 8 | DartPad only runs Dart, not Flutter. | **false** | DartPad runs both Dart console programs AND Flutter previews. |
| 9 | Get user input from a TextField controller. | **`_nameController.text`** | The `.text` property holds the entered string. |
| 10 | Clear user input. | **`_numController.text = '';`** | Setting `.text` to empty string clears the field. |
| 11 | Parameter of `Row`. | **`children`** | Row holds multiple widgets in a list. |
| 12 | Parameter of `Column`. | **`children`** | Column also holds a list of widgets. |
| 13 | Which class's `build()` is overridden for a StatefulWidget? | **`State`** | The build method lives in the State subclass, not the widget itself. |
| 14 | What CANNOT be passed to `runApp()`? | **A String object** | `runApp()` requires a Widget; String is not a widget. |
| 15 | Output of `print('The difference is ${m-n}')` where `m=11`, `n=11.8`. | **"The difference is -0.8"** | `11 - 11.8 = -0.8`, interpolated into the string. |
| 16 | Correct boolean declaration. | **`bool isValid = true;`** | `bool` is the keyword; `true`/`false` are the literal values. |
| 17 | `var r = {'Betty':10, 'Allan':30};` — what is `r`? | **It's a Map** | Curly braces with `key: value` pairs create a Map. (The question has a typo using `v` — ignore it.) |
| 18 | `final e; e = 10;` causes compilation error. | **true** | `final` must be initialized at declaration. |
| 19 | Correct call to `getResult(String operator, int n1, {int n2=1})`. | **`getResult('sqrt', 9);`** | Provides the two required positional args; `n2` uses its default. (Note: `getResult('+', 9, 10);` works too because positional args may follow positional args — if both appear as options, `getResult('+', 9, 10)` is also valid.) |
| 20 | Correct call to `getProduct(double, double, double, {double d4=1})`. | **`getProduct(16, 9, 19);`** | Provides exactly the three required positional args; `d4` defaults to 1. |
| 21 | NOT a correct OutlinedButton creation. | **The one missing `onPressed`** | `onPressed` is required; `onLongPress` alone isn't enough. |
| 22 | `int? x; var y=40; var val = x ?? y; print(val);` | **40** | `x` is null, so `??` returns `y` (40). |
| 23 | Only Dart is open source. | **false** | Both are open source. |
| 24 | Both Flutter and Dart are open source. | **true** | Both released under BSD-style license. |
| 25 | Everything in Dart is an object. | **true** | All values, including numbers and null, are objects. |
| 26 | Dart is a pure OOP language. | **true** | Official Dart description — every value is an object. |
| 27 | Flutter is a UI framework, Dart is a programming language. | **true** | That's exactly the relationship. |
| 28 | `int i=5;` — is `i` both int AND double? | **false** | Dart treats int and double as distinct types. |
| 29 | `double d=5.0;` — is `d` both double AND int? | **false** | Same reason — distinct types. |
| 30 | Which has a `home` parameter? | **MaterialApp** | `MaterialApp.home` defines the root screen. |
| 31 | Parameter of `Center`. | **`child`** | Center holds exactly one child. |
| 32 | Which has an `appBar` parameter? | **Scaffold** | `Scaffold.appBar` puts an AppBar at the top. |
| 33 | NOT a correct String creation. | **`var s = {"Hi"};`** | Curly braces create a Set, not a String. |
| 34 | Valid Dart entry point. | **`void main(){}`** | Lowercase main, void return, no params required. |
| 35 | Widget for user input. | **`TextField`** | The Material input widget. |
| 36 | Class where build is overridden for StatefulWidget. | **`State`** | The UI is built in the State subclass's build method. |

---

# PART 4 — NIGHT-BEFORE RECAP

Read these out loud:

1. **Flutter = UI toolkit. Dart = language. Both open source. Both by Google.**
2. **`void main() {}`** — lowercase, void, entry point.
3. **`Text` is Stateless. `TextField` is Stateful.**
4. **`runApp()` takes a Widget — never a String.**
5. **Build method for StatefulWidget lives in the State class.**
6. **`home:` → MaterialApp. `appBar:` → Scaffold.**
7. **`child:` (singular) → Center, Container, Buttons.**
8. **`children:` (list `[...]`) → Row, Column.**
9. **Buttons need BOTH `onPressed` AND `child`.**
10. **Get TextField input with `controller.text`. Clear with `controller.text = '';`**
11. **`final` must be initialized at declaration.**
12. **`int` ≠ `double` in Dart's type system.**
13. **`{'Hi'}` is a Set. `'Hi'` or `"Hi"` is a String.**
14. **`{'key': value}` is a Map.**
15. **`x ?? y` = "use y if x is null."**
16. **Everything in Dart is an object → Dart is pure OOP.**

You've got this. 🚀
