# MAD Quiz Study Guide — Flutter & Dart for Absolute Beginners

> **Goal:** By the end of this guide, you should recognize every concept the quiz tests and know *why* each correct answer is correct — not just memorize.

---

## How to Use This Guide

1. **Read Part 1** (Concepts) — learn the ideas.
2. **Read Part 2** (Cheat Sheet) — keep this open during practice.
3. **Read Part 3** (Night-Before Recap) — quick-fire bold rules to skim before the test.
4. **Try `QUESTIONS.md`** — 36 practice questions with collapsible answers to test understanding.

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

### Rule about `final` — local vs instance

For a **local** `final` variable, you may declare it without an initializer **as long as it's assigned exactly once before it's read**:

```dart
void main() {
  final e;     // ✅ OK — local final, not yet assigned
  e = 10;      // ✅ first (and only) assignment
  print(e);    // → 10
  e = 20;      // ❌ COMPILE ERROR — final can't be reassigned
}
```

But for an **instance field** (declared inside a class), `final` *must* be initialized at the declaration or in the constructor:

```dart
class Box {
  final e;     // ❌ COMPILE ERROR — instance final needs init
}
```

Best practice in beginner code: just initialize at the declaration — `final e = 10;` — so the rule works everywhere.

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
| `final x;` then `x = 10;` (local var) | ✅ OK — assigned exactly once |
| `final x;` as an **instance field** | ❌ Compile error — must init at declaration / in constructor |
| `int` and `double` | Are **different types** |
| `bool` literal | `true` or `false` (not `"true"`, not `1`) |
| `{'key': value}` is a | **Map** |
| `{'value'}` (no key) is a | **Set** (NOT a String!) |
| `'Hi'` or `"Hi"` | Both valid Strings |
| Dart is pure OOP | **True** — everything is an object |
| `x ?? y` means | "use x, but if x is null, use y" |

---

# PART 3 — NIGHT-BEFORE RECAP

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
11. **`final` = assigned exactly once. For a local `final`, declaration without an initializer is fine as long as you assign it before reading. For instance/static fields, it MUST be initialized at declaration (or in the constructor).**
12. **`int` ≠ `double` in Dart's type system.**
13. **`{'Hi'}` is a Set. `'Hi'` or `"Hi"` is a String.**
14. **`{'key': value}` is a Map.**
15. **`x ?? y` = "use y if x is null."**
16. **Everything in Dart is an object → Dart is pure OOP.**

You've got this. 🚀
