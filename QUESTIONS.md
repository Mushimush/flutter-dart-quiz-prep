# MAD Quiz Prep — Tweaked Practice Questions

A 20-question set adapted from the MAD QUIZ PREP. Same concepts, different code and values. Use it to test understanding, not memorization.

---

###### 1. What's the output?

```dart
void main() {
  var a = int.parse('20');
  var b = double.parse('20.5');
  print('Difference is ${a - b}');
}
```

- A: `Difference is 0`
- B: `Difference is -0.5`
- C: `Difference is ${a - b}`
- D: No output — compile error on line 2

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's break it down:
- `int.parse('20')` → `20` (an `int`)
- `double.parse('20.5')` → `20.5` (a `double`)
- `a - b` = `20 - 20.5` = `-0.5` (Dart promotes `int` to `double` in mixed arithmetic)
- `${a - b}` is **string interpolation** — the expression is evaluated and inserted into the string

Result: `Difference is -0.5`

**Key Rule — String interpolation:**

| Syntax | When to use |
|---|---|
| `$variable` | Drop in a single variable |
| `${expression}` | Drop in a calculation (math, method call, property) |

</p>
</details>

---

###### 2. Why does this program not start?

```dart
void Main() {
  print('Welcome');
}
```

- A: `print` needs double quotes
- B: The function must be named `main`, with a small `m`
- C: `void` must be written `Void`
- D: `Main` must be given an argument

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Dart is case-sensitive, and every Dart program starts at **`main`**. `Main` is just another function name, so Dart finds no starting point.

- Single or double quotes both work for a String.
- `void` is all lowercase.
- `main` does not need arguments.

</p>
</details>

---

###### 3. Will the following code compile?

```dart
void main() {
  final k;
  k = 25;
  print(k);
}
```

- A: Yes — output is `25`
- B: Yes — output is `null`
- C: No — `final` must be initialized at declaration
- D: No — `print` requires a String

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Let's break it down:
- `final k;` declares a **local** `final` variable without an initializer — this is allowed
- `k = 25;` is the first (and only) assignment — `final` permits exactly one
- `print(k);` then reads `k` after it's been assigned → prints `25`

This is called **definite assignment**: Dart lets you declare a local `final` without an initializer as long as the compiler can prove it's assigned exactly once before use.

**Important distinction — local vs instance/static `final`:**

| Where it lives | Must initialize at declaration? |
|---|---|
| **Local** variable (inside a function) | **No** — assign later, but exactly once |
| **Instance** field (inside a class) | **Yes** — at declaration or in the constructor |
| **Top-level / static** variable | **Yes** — at declaration |

So this would fail:
```dart
class Box {
  final k;        // ✗ instance field — needs init at declaration or in constructor
}
```

But the snippet in the question is a **local** variable inside `main()`, so it compiles.

**`var` vs `final` vs `const` (local variables):**

| Keyword | Must initialize at declaration? | Can reassign later? |
|---|---|---|
| `var` | No | Yes |
| `final` | No (but must be assigned exactly once before use) | No |
| `const` | **Yes** (and must be compile-time constant) | No |

</p>
</details>

---

###### 4. For the snippet below, is `count` an `int` AND also a `double`?

```dart
int count = 12;
```

- A: True — every `int` is also a `double` in Dart
- B: True — because `12` can be written as `12.0`
- C: False — `int` and `double` are distinct types in Dart
- D: False — only `num` is both

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- `int` and `double` are **separate types** in Dart's type system
- An `int` is **not** also a `double`, and a `double` is **not** also an `int`
- Both extend the abstract type `num`, but neither is a subtype of the other

**Common confusion:**
```dart
int trips = 8;      // trips is ONLY an int
double km = 3.2;   // km is ONLY a double
```

They look interchangeable in math (`5 + 5.0 = 10.0`), but the static types are different.

**Key Rule:** In Dart, `int` and `double` are siblings under `num`, not parent/child. Don't assume one is the other.

</p>
</details>

---

###### 5. Which of the following correctly declares a boolean named `isLoggedIn`?

- A: `bool isLoggedIn = "false";`
- B: `bool isLoggedIn = 0;`
- C: `boolean isLoggedIn = true;`
- D: `bool isLoggedIn = false;`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Let's analyze each option:

| Option | Code | Issue |
|---|---|---|
| **A ✗** | `bool isLoggedIn = "false";` | `"false"` is a **String**, not a bool |
| **B ✗** | `bool isLoggedIn = 0;` | `0` is an **int** — Dart bools aren't 1/0 like C |
| **C ✗** | `boolean isLoggedIn = true;` | The keyword is `bool`, not `boolean` |
| **D ✓** | `bool isLoggedIn = false;` | Correct! `bool` type with a literal `true`/`false` |

**Key Rule:** Dart's boolean type is `bool`. Its only legal values are the literals `true` and `false`. No strings, no numbers, no `boolean` keyword.

</p>
</details>

---

###### 6. Which of the following is **NOT** correct for creating a String object `name` in Dart?

- A: `String name = 'Maria';`
- B: `var name = "Maria";`
- C: `var name = {'Maria'};`
- D: `String name = "Maria";`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Code | Resulting type |
|---|---|---|
| **A ✓** | `String name = 'Maria';` | `String` |
| **B ✓** | `var name = "Maria";` | `String` (inferred) |
| **C ✗** | `var name = {'Maria'};` | **`Set<String>`** — curly braces create a Set! |
| **D ✓** | `String name = "Maria";` | `String` |

**Key Rule — The curly brace trap:**

| Syntax | Type |
|---|---|
| `'Hi'` or `"Hi"` | `String` |
| `['Hi']` | `List<String>` |
| `{'Hi'}` | `Set<String>` |
| `{'key': 'value'}` | `Map<String, String>` |

This is one of the most common quiz tricks — quotes create Strings, braces create Sets or Maps.

</p>
</details>

---

###### 7. What is the type of `data` in the snippet below?

```dart
var data = {'apple': 3, 'banana': 7, 'cherry': 5};
```

- A: `List<String>`
- B: `Set<String>`
- C: `Map<String, int>`
- D: `String`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- Curly braces `{ ... }` with **`key: value` pairs** create a **Map**
- The keys are Strings (`'apple'`, `'banana'`, `'cherry'`)
- The values are ints (`3`, `7`, `5`)
- Dart infers the type as `Map<String, int>`

**Key Rule — Telling Set and Map apart:**

| Syntax | Type |
|---|---|
| `{1, 2, 3}` | `Set<int>` — bare values |
| `{'a': 1, 'b': 2}` | `Map<String, int>` — `key: value` pairs |
| `{}` | `Map<dynamic, dynamic>` (empty defaults to Map) |

If you want an empty Set, use `<int>{}` or `Set<int>()`.

</p>
</details>

---

###### 8. What's the output?

```dart
void main() {
  int? a;
  var b = 100;
  var result = a ?? b;
  print(result);
}
```

- A: Compile error — `a` is null
- B: `a??b`
- C: `100`
- D: `null`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- `int? a;` declares `a` as a **nullable int** — its value is `null` by default
- `var b = 100;` is a regular int with value 100
- `a ?? b` is the **null-coalescing operator**: "if `a` is null, use `b`"
- Since `a` is `null`, the expression returns `b` (which is `100`)

**Key Rule — Null safety operators:**

| Operator | Meaning |
|---|---|
| `int? x` | `x` may be `null` |
| `x ?? y` | If `x` is null, use `y` |
| `x!` | Assert `x` is non-null (throws if it is) |
| `x?.method()` | Call method only if `x` is not null |

</p>
</details>

---

###### 9. Which of the following gets the user input from a `TextField`?

Assume `_emailController` is a `TextEditingController` attached to the TextField.

- A: `_emailController.input`
- B: `_emailController.value`
- C: `_emailController.text`
- D: `_emailController.data`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- A `TextEditingController` exposes the typed text via its **`.text`** property
- `.value` exists, but it returns a `TextEditingValue` object (text + selection + composing range), not the plain string
- `.input` and `.data` don't exist on the controller

**Reading and clearing input:**
```dart
final _emailController = TextEditingController();

TextField(controller: _emailController);

print(_emailController.text);    // read
_emailController.text = '';       // clear
```

**Key Rule:** Always use `.text` on a `TextEditingController` for the typed string.

</p>
</details>

---

###### 10. Which of the following clears the user input in a `TextField`?

Assume `_ageController` is a `TextEditingController` attached to the TextField.

- A: `_ageController.value = 0;`
- B: `_ageController.clear = true;`
- C: `_ageController.text = '';`
- D: `_ageController.input = null;`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Code | Issue |
|---|---|---|
| **A ✗** | `_ageController.value = 0;` | `value` expects a `TextEditingValue`, not an int |
| **B ✗** | `_ageController.clear = true;` | `clear` is a **method** (`controller.clear()`), not a settable property |
| **C ✓** | `_ageController.text = '';` | Correct! Empty string clears the field |
| **D ✗** | `_ageController.input = null;` | `input` doesn't exist on the controller |

**Alternative:** `_ageController.clear()` also works (it's a method call).

</p>
</details>

---

###### 11. Which line compiles?

- A: `Column(child: Text('A'))`
- B: `Column(Children: [Text('A')])`
- C: `Column(children: [Text('A'), Text('B')])`
- D: `Column(children: Text('A'))`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

- **A ✗** `Column` has no `child`. It holds many widgets.
- **B ✗** Dart is case-sensitive, so `Children` does not exist.
- **C ✓** `children` with a **list** `[ ]`.
- **D ✗** `children` needs a list, even for one widget.

**Key Rule:** `child:` takes one widget (Center, Container, buttons). `children:` takes a list (Row, Column).

</p>
</details>

---

###### 12. Which line causes a compile error?

- A: `runApp(Center(child: Text('Hi')));`
- B: `runApp(Icon(Icons.home));`
- C: `runApp(3 > 2);`
- D: `runApp(Column(children: []));`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`runApp()` takes a **Widget**. `3 > 2` is a `bool`, so it is rejected. `Center`, `Icon` and `Column` are all widgets.

**Key Rule:** numbers, bools, Strings and lists are not widgets.

</p>
</details>

---

###### 13. `CartPage` is a StatefulWidget. Where does the code that draws the page go?

```dart
class CartPage extends StatefulWidget {
  // (1)
}
class _CartPageState extends State<CartPage> {
  // (2)
}
```

- A: A `build()` method at (1)
- B: A `build()` method at (2)
- C: A `createState()` method at (2)
- D: A `runApp()` call at (1)

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

- (1) is the widget class. It has only `createState()`.
- (2) is the State class. It keeps the data that changes, and its `build()` draws the page.

**Key Rule:** for a StatelessWidget, `build()` is in the widget class itself. For a StatefulWidget, it is in the State class.

</p>
</details>

---

###### 14. You want `LoginPage()` to be the first screen of the app. Which line is correct?

- A: `MaterialApp(body: LoginPage())`
- B: `MaterialApp(home: LoginPage())`
- C: `Scaffold(home: LoginPage())`
- D: `MaterialApp(child: LoginPage())`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`MaterialApp` uses `home:` for the first screen.

- `body:` belongs to `Scaffold`.
- `Scaffold` has no `home:`.
- `MaterialApp` has no `child:`.

</p>
</details>

---

###### 15. Which code shows a bar with the title 'Menu' at the top of the page?

- A: `MaterialApp(home: Text('Hi'), appBar: AppBar(title: Text('Menu')))`
- B: `Center(appBar: AppBar(title: Text('Menu')))`
- C: `Scaffold(children: [AppBar(title: Text('Menu'))])`
- D: `Scaffold(appBar: AppBar(title: Text('Menu')), body: Text('Hi'))`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`Scaffold` is the page layout. It takes `appBar:` for the bar and `body:` for the rest of the page. `MaterialApp` and `Center` have no `appBar:`, and `Scaffold` has no `children:`.

</p>
</details>

---

###### 16. A form needs a box where the user types a postal code. Which widget do you use?

- A: `Text`
- B: `Container`
- C: `Icon`
- D: `TextField`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`TextField` accepts typing. `Text` and `Icon` only display something, and `Container` is a box for layout.

</p>
</details>

---

###### 17. Given the `ElevatedButton` constructor below, which is **NOT** a correct way to create one?

```dart
ElevatedButton({
  Key? key,
  required void Function()? onPressed,
  void Function()? onLongPress,
  ButtonStyle? style,
  required Widget? child,
})
```

- A: `ElevatedButton(child: Text('Save'), onPressed: () {})`
- B: `ElevatedButton(onPressed: () {}, child: Text('Cancel'))`
- C: `ElevatedButton(onLongPress: () {}, child: Text('Delete'))`
- D: `ElevatedButton(child: Text('OK'), onPressed: () {}, style: ButtonStyle())`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Has `onPressed`? | Has `child`? | Valid? |
|---|---|---|---|
| **A** | ✓ | ✓ | ✓ Valid — order doesn't matter for named params |
| **B** | ✓ | ✓ | ✓ Valid |
| **C** | ✗ **Missing!** | ✓ | ✗ **Invalid** — `onPressed` is `required` |
| **D** | ✓ | ✓ | ✓ Valid — extra optional `style` is fine |

**Key Rule:** Buttons in Material (`ElevatedButton`, `FilledButton`, `TextButton`, `OutlinedButton`) **all require BOTH**:
- `onPressed:` — what to do when tapped (can be `null` to disable, but must be passed)
- `child:` — what to display

Setting `onPressed: null` produces a greyed-out, disabled button — but you still have to pass it.

</p>
</details>

---

###### 18. Given the function below, which call is correct?

```dart
void calculate(String op, double x, {double y = 2.0}) {
  switch (op) {
    case '+': print('$x + $y = ${x + y}');
    case '-': print('$x - $y = ${x - y}');
    case '*': print('$x * $y = ${x * y}');
  }
}
```

- A: `calculate('+', 10.5, 5.5);`
- B: `calculate('-', y: 3.0);`
- C: `calculate('*', 4.0);`
- D: `calculate(8.0, '+', y: 2.0);`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Call | Issue |
|---|---|---|
| **A ✗** | `calculate('+', 10.5, 5.5)` | `5.5` is positional but `y` is **named** — must use `y: 5.5` |
| **B ✗** | `calculate('-', y: 3.0)` | Missing the second required positional arg `x` |
| **C ✓** | `calculate('*', 4.0)` | Correct! `op = '*'`, `x = 4.0`, `y` defaults to `2.0` |
| **D ✗** | `calculate(8.0, '+', y: 2.0)` | Wrong order — first positional must be `String op`, second must be `double x` |

**Key Rule — Named parameters:**

```dart
void f(int a, int b, {int c = 0}) { ... }

f(1, 2);              // ✓ c defaults to 0
f(1, 2, c: 3);         // ✓ use 'c:' label
f(1, 2, 3);            // ✗ named params can't be called positionally
f(c: 3, 1, 2);         // ✗ named params must come AFTER positional
```

</p>
</details>

---

###### 19. Which statement(s) are true about Flutter and Dart?

**Statement 1:** Flutter is a UI framework; Dart is a programming language.
**Statement 2:** Both Flutter and Dart are open-source projects by Google.
**Statement 3:** Dart can only target Android and Web, not iOS.
**Statement 4:** Everything in Dart is an object.

- A: Statements 1 and 2 only
- B: Statements 1, 2, and 4
- C: Statements 1, 2, 3, and 4
- D: Statement 1 only

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's analyze each statement:

| # | Statement | Verdict |
|---|---|---|
| 1 | Flutter is a UI framework; Dart is a programming language | ✓ True — exactly the relationship |
| 2 | Both Flutter and Dart are open-source projects by Google | ✓ True — both are open source |
| 3 | Dart can only target Android and Web, not iOS | ✗ **False** — Dart/Flutter supports iOS, Android, Web, Windows, macOS, Linux |
| 4 | Everything in Dart is an object | ✓ True — Dart is pure OOP; even `int`, `null`, and functions are objects |

**Key Facts to memorize:**
- Flutter = UI framework (toolkit), built **using** Dart
- Dart = programming language used to write Flutter apps
- Both open source ✓
- Both by Google ✓
- Cross-platform: Android, iOS, Web, Windows, macOS, Linux
- Dart is pure OOP — everything is an object

</p>
</details>

---

###### 20. Match each widget to whether it's `StatelessWidget` or `StatefulWidget`.

Consider: `Text`, `TextField`, `Icon`, `Checkbox`

- A: All four are Stateless
- B: `Text` and `Icon` are Stateless; `TextField` and `Checkbox` are Stateful
- C: `Text` and `TextField` are Stateless; `Icon` and `Checkbox` are Stateful
- D: All four are Stateful

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's classify each:

| Widget | Type | Why |
|---|---|---|
| `Text` | **Stateless** | Just displays a string — never changes after build |
| `Icon` | **Stateless** | Just displays a glyph — never changes after build |
| `TextField` | **Stateful** | The typed text changes as the user types |
| `Checkbox` | **Stateful** | Toggles between checked and unchecked |

**Key Rule — How to tell:**

| Ask yourself | If yes → use |
|---|---|
| Does anything in this widget change after it's first drawn? | `StatefulWidget` |
| Does it just display data passed to it? | `StatelessWidget` |

**Analogy:**
- `StatelessWidget` = a printed photo — once printed, never changes
- `StatefulWidget` = a digital photo frame — same frame, but the picture inside can swap

For `StatefulWidget`, the `build()` method lives in the **`State`** subclass, not the widget itself.

</p>
</details>

---

###### 21. You want a star and the number 5 side by side. Which line compiles?

- A: `Row(child: [Icon(Icons.star), Text('5')])`
- B: `Row([Icon(Icons.star), Text('5')])`
- C: `Row(children: [Icon(Icons.star), Text('5')])`
- D: `Row(children: Icon(Icons.star), Text('5'))`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`Row` takes a **list** through the named parameter `children:`. A uses the wrong name, B leaves the name out, and D leaves out the list brackets.

</p>
</details>

---

###### 22. Which of the following parameters belongs to the `Container` widget?

- A: `Children`
- B: `children`
- C: `child`
- D: `Color`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- `Container` is a **single-child** widget — it wraps exactly ONE widget
- The parameter is **`child:`** (lowercase, singular)
- `children:` is wrong — that's plural for Row/Column
- `Children:` and `Color:` (capitalized) don't exist — Dart is case-sensitive

```dart
Container(
  color: Colors.blue,
  padding: EdgeInsets.all(8),
  child: Text('Hello'),       // child, singular
);
```

**Note:** Container *does* have a `color:` parameter (lowercase), but the question asks about `Color:` (capitalized) which is invalid.

</p>
</details>

---

###### 23. How many classes do you write for one StatelessWidget page, and for one StatefulWidget page?

- A: 1 and 1
- B: 1 and 2
- C: 2 and 1
- D: 2 and 2

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

- **Stateless: 1.** The widget class has `build()` itself.
- **Stateful: 2.** The widget class has `createState()`, and the State class has `build()`.

</p>
</details>

---

###### 24. Which of the following are `StatefulWidget`s? (Pick the correct set.)

Consider: `Checkbox`, `Switch`, `Slider`, `Text`, `Icon`

- A: All five are Stateful
- B: `Checkbox`, `Switch`, and `Slider` are Stateful; `Text` and `Icon` are Stateless
- C: Only `Checkbox` is Stateful
- D: `Text`, `Icon`, and `Slider` are Stateful

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's classify each:

| Widget | Type | Reason |
|---|---|---|
| `Checkbox` | **Stateful** | Toggles between checked/unchecked |
| `Switch` | **Stateful** | Toggles between on/off |
| `Slider` | **Stateful** | Position changes as the user drags |
| `Text` | **Stateless** | Just displays a string |
| `Icon` | **Stateless** | Just displays a glyph |

**Key Rule — How to tell:**

| Ask | If yes → |
|---|---|
| Does the widget change visually based on user interaction? | `StatefulWidget` |
| Does it just display whatever was passed in? | `StatelessWidget` |

A useful gut check: if it's an **input control** (Checkbox, Switch, Slider, TextField, DropdownButton), it's almost always Stateful.

</p>
</details>

---

###### 25. Is `ElevatedButton`'s `onPressed` parameter required?

- A: Yes — you must pass `onPressed`, even if it's `null` to disable the button
- B: No — `onPressed` is optional like `onLongPress`
- C: Only required if you also pass `child`
- D: Only required on `FilledButton`, not `ElevatedButton`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Let's break it down:
- All Material buttons (`ElevatedButton`, `FilledButton`, `TextButton`, `OutlinedButton`) **require** `onPressed`
- The constructor declares it as `required void Function()? onPressed`
- The `?` means the *value* can be `null`, but you must still pass the parameter
- Passing `null` produces a **disabled (greyed out)** button — common pattern when input is invalid

```dart
ElevatedButton(onPressed: () { print('Tapped'); }, child: Text('Tap'));   // ✓ enabled
ElevatedButton(onPressed: null, child: Text('Tap'));                       // ✓ disabled
ElevatedButton(child: Text('Tap'));                                        // ✗ ERROR
```

**Key Rule:** `required` + `?` = "must pass it, but it can be null."

</p>
</details>

---

###### 26. What is wrong with this button?

```dart
TextButton(onPressed: () {})
```

- A: Nothing, it shows an empty button
- B: `onPressed` cannot be an empty function
- C: The required `child` is missing
- D: It needs `children: []` instead

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Material buttons such as `TextButton` need **both** `onPressed` and `child`. Without `child`, this does not compile. An empty function `() {}` is fine for `onPressed`.

</p>
</details>

---

###### 27. Which statement about Flutter is **TRUE**?

- A: Flutter is a low-code, drag-and-drop framework
- B: Flutter compiles to native code for both Android and iOS
- C: Flutter only works on mobile platforms (Android + iOS)
- D: Flutter is a programming language, not a framework

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's analyze each option:

| Option | Verdict | Why |
|---|---|---|
| **A ✗** | False | Flutter is a full SDK — you write real Dart code, not low-code/no-code |
| **B ✓** | True | Flutter compiles to native ARM/x64 code for high performance |
| **C ✗** | False | Flutter also targets Web, Windows, macOS, Linux |
| **D ✗** | False | Flutter is a UI framework written in Dart; Dart is the language |

**Cross-platform reach:**

Flutter → 📱 Android, 🍎 iOS, 🌐 Web, 🪟 Windows, 💻 macOS, 🐧 Linux

**Key distinction:**
- **Dart** = the programming language
- **Flutter** = the UI framework built using Dart

</p>
</details>

---

###### 28. Which statement about DartPad is **TRUE**?

- A: DartPad can only run plain Dart programs, not Flutter apps
- B: DartPad can run both Dart programs and Flutter UI previews
- C: DartPad requires installing Flutter SDK locally
- D: DartPad is only available for paid users

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's break it down:
- **DartPad** (dartpad.dev) is the official online playground from Google
- It supports **both**:
  - Console Dart programs (with `print` output)
  - Flutter widget previews (with a live UI)
- It's free, browser-based, and needs no installation

**When to use DartPad:**
- Trying out Dart syntax quickly
- Sharing a small code snippet via URL
- Teaching Flutter without installation overhead
- Sandbox experiments without polluting your local project

**Limitations:** DartPad doesn't support arbitrary `pub` packages or platform plugins — for full apps, use the local Flutter SDK.

</p>
</details>

---

###### 29. Which statement about Dart is **TRUE**?

- A: Dart is procedural, like C
- B: Dart only supports primitive types (int, double, bool, String)
- C: Dart is a pure object-oriented language — every value is an object
- D: Dart has no support for null safety

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Verdict | Why |
|---|---|---|
| **A ✗** | False | Dart is object-oriented (with functional features), not procedural |
| **B ✗** | False | Dart has Lists, Maps, Sets, classes, generics, records, etc. |
| **C ✓** | True | Even `int`, `bool`, `null`, and functions are objects (instances of `Object`) |
| **D ✗** | False | Dart has **sound null safety** built into the type system |

**What "everything is an object" means:**

```dart
5.toString();         // 'int' has methods — it's an object
true.runtimeType;     // 'bool' is an object
null is Object?;      // even null has a type
```

Because everything is an object, you get methods on basically anything — even literals.

</p>
</details>

---

###### 30. For the snippet below, is `price` a `double` AND also an `int`?

```dart
double price = 19.99;
```

- A: True — every `double` is also an `int` when the decimal is zero
- B: True — Dart auto-converts between numeric types
- C: False — `double` and `int` are distinct types in Dart
- D: False — only `num` is both

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- `double` and `int` are **separate types** — neither is a subtype of the other
- `price` is *only* a `double`
- This is the mirror of the int-is-not-double question

```dart
double a = 5.0;
int b = a;            // ✗ Compile error — can't assign double to int
int c = a.toInt();    // ✓ explicit conversion
```

**Key Rule — Dart's number hierarchy:**

```
        num
       /   \
    int   double
```

Both `int` and `double` extend `num`, but they're siblings — not parent/child. To convert between them, use `.toInt()`, `.toDouble()`, or `.round()` explicitly.

</p>
</details>

---

###### 31. What is the correct call to the function below?

```dart
double getArea(double width, double height, {double scale = 1.0}) {
  return width * height * scale;
}
```

- A: `getArea(5.0, 10.0, 2.0);`
- B: `getArea(5.0);`
- C: `getArea(5.0, 10.0);`
- D: `getArea(scale: 2.0);`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Call | Issue |
|---|---|---|
| **A ✗** | `getArea(5.0, 10.0, 2.0)` | Third arg is positional, but `scale` is **named** — must use `scale: 2.0` |
| **B ✗** | `getArea(5.0)` | Missing required `height` |
| **C ✓** | `getArea(5.0, 10.0)` | Correct! `width = 5.0`, `height = 10.0`, `scale` defaults to `1.0` |
| **D ✗** | `getArea(scale: 2.0)` | Missing both required positional args |

**Key Rule — Calling a function with mixed parameters:**

```dart
void f(int a, int b, {int c = 0, int d = 0}) {}

f(1, 2);              // ✓ a=1, b=2, c/d default
f(1, 2, c: 3);         // ✓ named c
f(1, 2, c: 3, d: 4);   // ✓ both named
f(1, 2, 3);            // ✗ can't pass named positionally
f(c: 3, 1, 2);         // ✗ named must come AFTER positional
```

</p>
</details>

---

###### 32. Which call compiles?

```dart
double fare(double base, double km, double rate, {double discount = 0}) {
  return base + km * rate - discount;
}
```

- A: `fare(3.9, 5, 0.6, 1.5);`
- B: `fare(3.9, 5, 0.6, discount: 1);`
- C: `fare(3.9, 5);`
- D: `fare(3.9, 5, discount: 1);`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

- **A ✗** `discount` is named, so a fourth bare value is not allowed.
- **B ✓** Three positional values, then the named one with its label.
- **C ✗** `rate` is missing.
- **D ✗** `rate` is still missing. A named value cannot replace it.

</p>
</details>

---

###### 33. What's the output?

```dart
void main() {
  var name = 'Sam';
  var score = 42;
  print('Hello, $name! Your score doubled is ${score * 2}.');
}
```

- A: `Hello, $name! Your score doubled is ${score * 2}.`
- B: `Hello, Sam! Your score doubled is 84.`
- C: `Hello, Sam! Your score doubled is score * 2.`
- D: Compile error — invalid interpolation

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's break it down:
- `$name` → substitutes the value of `name` → `Sam`
- `${score * 2}` → evaluates the expression → `42 * 2 = 84`
- Result: `Hello, Sam! Your score doubled is 84.`

**Key Rule — String interpolation:**

| Syntax | When to use | Example |
|---|---|---|
| `$varname` | Single identifier | `'Hi $name'` |
| `${expression}` | Anything else (math, methods, properties) | `'Total: ${a + b}'`, `'Upper: ${s.toUpperCase()}'` |

```dart
var n = 5;
print('$n + 1 = ${n + 1}');    // 5 + 1 = 6
print('$n.toString()');         // 5.toString()    ← NOT evaluated, taken literally
print('${n.toString()}');       // 5               ← evaluated correctly
```

</p>
</details>

---

###### 34. Which of the following is the type of `nums`?

```dart
var nums = {1, 2, 3, 2, 1};
print(nums);
```

- A: `List<int>` — prints `[1, 2, 3, 2, 1]`
- B: `Map<int, int>` — prints `{1: 1, 2: 2, 3: 3}`
- C: `Set<int>` — prints `{1, 2, 3}`
- D: Compile error — duplicate keys

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's break it down:
- `{ ... }` with bare values (no `key: value`) creates a **Set**
- Sets remove duplicates automatically
- Order is preserved (since Dart 2.0 — `LinkedHashSet` by default)
- Output: `{1, 2, 3}` — the duplicates `2` and `1` are dropped

**Compare the three collection literals:**

```dart
var list = [1, 2, 3, 2, 1];     // List<int>      → [1, 2, 3, 2, 1]
var set  = {1, 2, 3, 2, 1};     // Set<int>       → {1, 2, 3}
var map  = {1: 'a', 2: 'b'};    // Map<int,String>→ {1: 'a', 2: 'b'}
```

**Key Rule:** Square brackets `[]` = List. Curly braces `{}` with bare values = Set. Curly braces `{}` with `key: value` = Map.

</p>
</details>

---

###### 35. Which is the correct way to read input and clear a `TextField`?

```dart
final _controller = TextEditingController();

TextField(controller: _controller);
```

To **read** the typed value and **clear** the field:

- A: Read `_controller.value`; clear `_controller.value = '';`
- B: Read `_controller.text`; clear `_controller.text = '';`
- C: Read `_controller.input`; clear `_controller.input = null;`
- D: Read `_controller.data`; clear `_controller.data.clear();`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Let's break it down:
- A `TextEditingController` exposes the typed string via its **`.text`** property
- To clear, set `.text` back to an empty string
- `.value` exists, but returns a `TextEditingValue` object (text + selection + composing), not the plain string
- `.input` and `.data` don't exist on the controller

```dart
final _controller = TextEditingController();

TextField(controller: _controller);

// later...
print(_controller.text);       // read what the user typed
_controller.text = '';         // clear the field
// or:
_controller.clear();           // also clears (method form)
```

**Why TextField is StatefulWidget:** because what's inside changes as the user types. The controller is the bridge between the UI and your logic.

</p>
</details>

---

###### 36. Spot the **invalid** widget composition:

- A: `Center(child: Text('Hello'))`
- B: `Column(children: [Text('A'), Text('B')])`
- C: `Center(children: [Text('A'), Text('B')])`
- D: `Container(child: Row(children: [Icon(Icons.star), Text('Rated')]))`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Let's analyze each option:

| Option | Code | Valid? |
|---|---|---|
| **A ✓** | `Center(child: Text('Hello'))` | Center takes one `child:` |
| **B ✓** | `Column(children: [Text('A'), Text('B')])` | Column takes `children:` list |
| **C ✗** | `Center(children: [...])` | **Center has no `children:`** — only `child:` |
| **D ✓** | `Container(child: Row(...))` | Container holds one widget, Row holds many — both valid |

**Key Rule — singular vs plural:**

| Widget | Singular `child:` | Plural `children:` |
|---|---|---|
| Center | ✓ | ✗ |
| Container | ✓ | ✗ |
| Padding | ✓ | ✗ |
| Buttons | ✓ | ✗ |
| Row | ✗ | ✓ |
| Column | ✗ | ✓ |
| ListView | ✗ | ✓ |
| Stack | ✗ | ✓ |

Mix them up and Flutter throws a compile error before the app runs.

</p>
</details>

---

## Concept Coverage

This 36-question set adapts the original MAD QUIZ PREP across all key concepts:

| Concept | Questions |
|---|---|
| Flutter vs Dart identity | 19, 27, 29 |
| Dart entry point | 2 |
| Variables (`final` must initialize) | 3 |
| Types (`int` vs `double`) | 4, 30 |
| Booleans | 5 |
| Strings & curly brace trap | 6 |
| Collections (List, Set, Map) | 7, 34 |
| Null safety (`??`) | 8 |
| String interpolation + parsing | 1, 33 |
| TextField + TextEditingController | 9, 10, 35 |
| `child` vs `children` | 11, 21, 22, 36 |
| `runApp()` | 12 |
| Stateless vs Stateful | 13, 20, 23, 24 |
| Common widgets (`home`, `appBar`) | 14, 15 |
| User input widget | 16 |
| Required button parameters | 17, 25, 26 |
| Function named parameters | 18, 31, 32 |
| Flutter cross-platform | 27 |
| DartPad capabilities | 28 |

---

## How to use this file

- Each question has a collapsible `<details>` answer — try answering first, then click to reveal
- Best viewed on GitHub or any markdown viewer that supports `<details>`
- Designed for self-study; for a closed-book mock exam, take the questions only (cover the answer sections)
