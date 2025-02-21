# Getting JS to run
We can use the `<script></script>` tag to write Javascript within an HTML document.
We can use external scripts using `<script src="PATH"></script>`.  Scripts cannot both contain a source to another file and content within the script tag. If a source is provided, the content of the script tag is ignored. Multiple scripts can be added using multiple tags.

There are two types of PATHs that can be given. *Absolute* paths that provide the complete path to the file (e.g. `'/path/to/script.js'`) and *relative* paths that provide a path to a file in the same working directory (e.g. `./script.js` given that `script.js` is in the same directory as the HTML file). Full URLs can be given as PATHs too.

# Basic formatting
At the end of each line, a `;` semicolon is necessary. 
`//` - Single line comment
`/* */` - Multi-line comment (nested comments aren't supported.)

### Compatibility
Most modifications after 2009 are turned off by default, we need to enable `strict` mode to utilize them.

<mark style="background: #D2B3FFA6;">To make sure your JS script uses modern features, write</mark> `use strict;` <mark style="background: #D2B3FFA6;">at the top of the file </mark>(otherwise, the code above it won't be using strict mode). This can also be added to functions individually to make only that function use the modern features.

For browsers, put `use strict;` before any code you add in the developer console. `Shift Enter` lets you add a newline so you can work on your code.

## Variables
**Variables** are a 'named storage' for data.
We can create a variable using `let`.
```javascript
let words; //Creates a variable called words (no content inside).
```

We can assign values to variables using the = operator.
```javascript
let words = "Something"; //Creates variable words and assigns value "Something".
```

> Note: Once the variable is created, we don't need to use `let` to assign it a value. Repeated declarations create errors.

Now, we can access the value of the variable using it's name. <mark style="background: #ABF7F7A6;">Variables can be assigned any data type value at any time.</mark> Variables assigned with strings don't always have to be strings. 
```js
let words;
words = "Something"; //We can assign values to variables infinitely without using let
alert(words);
```

We can also declare multiple variables in the same line. This isn't ideal, better to declare each variable in separate lines.
```js
let words = "Something", things = "Nothing", hotel = "trivago";
```

### Naming limitations
1. The name must contain only letters, digits, or the symbols `$` and `_`. Just `$` and `_` can be used as variables too. 
2. The first character must not be a digit.

<mark style="background: #D2B3FFA6;">camelCase is the standard for JS naming</mark>. JavaScript is *case sensitive*. Certain words that are used for syntax are **reserved** and cannot be used.

<mark style="background: #D2B3FFA6;">All variables should have clear names that explain their purpose. Comments should be added with variables to provide extra information.</mark>

## Constants
Constants are variables that cannot be changed. They are defined using `const` instead of `let`.
```js
const VALUE = 5; //Can't be changed after being defined.
```

<mark style="background: #D2B3FFA6;">Naming convention states that all constants should be UPPERCASE.</mark>

# Data Types
We can use `typeof` to find the data type of a specific element/object/variable. We can also use `typeof()` to contain expressions and find their type. Note: `typeof` is not a function, it is an operator.
```js
typeof 22; // Number
typeof "Hi mom"; // String
typeof (200 + 3); // Number
```
## Number
Numbers represent both **integers** and **floating point numbers**. Both are the same datatype.
```js
let number = 22; // Number as a integer
number = 2.2; //Number as a floating point
```

### Operations
You can do multiplication `*`, division `/`, addition `+`, subtraction `-`.

### Special Types
There are, additionally, three special numbers in this datatype.
```js
alert(1/0); //Infinity
let negativeInfinity = -Infinity; // Negative infinity
let not_a_number = NaN; //Not a number

```

Infinity and negative infinity represent any case where there is an infinite number.<mark style="background: #ABF7F7A6;"> Can be written in terms of an operation that leads to infinity or directly the infinity keyword itself.</mark>

`NaN` is not a number, it is an error that is generated when there is an incorrect mathematical operation. For example, trying to divide a string by 2 (`string`/2). `NaN` is *sticky*, that means any future operations with this value only return `NaN`.

## BigInt
In JavaScript, the “number” type cannot safely represent integer values larger than $(2^{53}-1)$ (that’s $9007199254740991$), or less than $-(2^{53}-1)$ for negatives. After these values, there is a precision error. 

To avoid this error, we have a datatype that holds exceptionally large numbers. A `BigInt` value is created by appending `n` to the end of an integer.
```js
// n at the end means bigInt
let bigInt = 1234567890123456789012345678901234567890n;
```

## String
A **string** is a set of characters inside quotes. There are three types of quotes that can be used. *Single* and *double* are identical since they are simple quotes.
1. Single quotes: `'Hello'` 
2. Double quotes: `"Hello"`
3. Backtick quotes: `` `Hello` ``

<mark style="background: #ABF7F7A6;">Backtick quotes are used to extend functionality and allow embedding variables and expressions into a string using </mark>`${...}`. 

Strings, variables and even operations can be added and will automatically resolve and be added to the string.
```js
let name = Johnny;
alert(`I don't know your name, ${name} but the system does.`)
```

## Boolean
A datatype that can only have two values: `true` (yes/positive) or `false`(no, negative).

Booleans can also result from comparisons. The common comparison operators are: `>`, `<`
```js
let is_js_cool = True;
alert(5 > 7); // Returns False
```

## Null
A special datatype that represents (literally) nothing.
```js
let id = null;
```

In this case, id is 'unknown' or empty.

## Undefined
A special datatype only assigned to variables that have been created but not defined. Generally, don't assign this to any variables, instead use `null`.
```js
let something;
alert(something) //Returns undefined
```

## Objects
Objects are special datatypes because they can contain multiple values (which are of other datatypes). Other datatypes are called *primitive* because they can only store a single value, but objects are *complex* because they can store collections of data.
### Symbol
Used to create unique identifiers for objects.

# Type Conversions
### Converting to String
Certain methods like `alert()` automatically convert all text inside into strings.
To manually convert to strings, we use the `String(value)` operator. 
```js
let numberText = String(42); // numberText has value of type String "42"
```

### Converting to Number
We can convert to number using `Number(Value)`. Shorthand for `Number()` is `+`.
`Undefined` -> Becomes `NaN`
`Null` -> Becomes `0`
`true`/`false` -> Becomes `1`/`0`
`string` -> Becomes a number ONLY if there are numbers and whitespaces in the string. If any non-numerical characters are present, `NaN` is returned instead.

```js
let value1 = Number(Undefined); // Becomes NaN
let value2 = Number(Null); // Becomes 0
let value3 = Number(true); // Becomes 1
let value4 = Number("  40  "); // Becomes 40, all whitespace removed.
let value5 = +" 55 "; // Automatically converts to number 55.
```

### Converting to Boolean
We can convert values to booleans using `Boolean(Value)`.
- Values that are intuitively “empty”, like `0`, an empty string, `null`, `undefined`, and `NaN`, become `false`.
- Other values become `true`.
```js
let notTrue = Boolean(''); // Value is false
let totallyTrue = Boolean("sky"); // Value is true
```

# Basic Operators
### Basic terms
**operand** - What the operator is applied to. In `3 + 4`, `3` and `4` are operands, as they are the ones being added.
**operator** - The action being done to a/several operands.
- **unary** operators only have one operand. E.g. `-54` is a unary operator because it only has one operand, `54`.
- **binary** operators have two operands. E.g. `54 * 1` is a binary operator because it has two operands, `54` and `1`.

## Math Operators
- Addition `+`,
- Subtraction `-`,
- Multiplication `*`,
- Division `/`,
- Remainder `%` - The remaining value after doing a full integer division. `13 % 2` gives `1` as 1 is the remainder.
- Exponentiation `**` - Represents multiplying to the *power* of something. `2 ** 4` gives 16 as $2^4$ is 16.
## String Concatenation
You can add strings using the `+` operator. If any operand in the operation is a string, all operands are automatically converted into strings.
```js
let twoWords = 'Hello ' + 'world!'; // Returns "Hello world!"
let threeNumbers = '1' + 2 + 2; // Returns 122, not 14.  
```

Only `+` supports concatenation. All other operators automatically convert their operands into numbers.

## Operator Precedence
| Precedence | Name           | Operator |
| ---------- | -------------- | -------- |
| 14         | unary plus     | `+`      |
| 14         | unary negation | `-`      |
| 13         | exponentiation | `**`     |
| 12         | multiplication | `*`      |
| 12         | division       | `/`      |
| 11         | addition       | `+`      |
| 11         | subtraction    | `-`      |
| …          | …              | …        |
| 2          | assignment     | `=`      |
Higher precedence values go first. 

### Assignment Operator
Assignment operator is low priority, but it is an operator. It can be used within expressions. And, it can be chained.
```js
let number1 = 5;
let number2;
let number3 = 15 + (number2 = number1 + 3); // Returns 23. 15 + (number2 = 5 + 3)
// 15 + 8 = 23
number1 = number2 = number3 = 4;
```

It is strongly advised **not** to use either of these methods for readability. Keep everything on seperate lines.

We can also modify the current value using the `+=`, `*=`,`/=` and `-=` operators.
```js
let number1 = 5;
number1 += 3; // Value is 5 + 3 = 8
number1 *= 2; // Value is 8 * 2 = 16
```

### Increments and Decrements
To increase a value by 1, we use `++`. To decrease a value by 1, we use `--`.
```js
let numberT = 1;
numberT++; // numberT is now 2
numberT--; // numberT is now 1
```

We can add the `++` and `--` as a **prefix** or a **postfix**
A **prefix** will return the new value. 
```js
let numberA = 3;
let numberB = ++numberA; // Returns 4
```
A **postfix** will return the old value.
```js
let numberA = 3;
let numberB = ++numberA; // Returns 3
```
Note: In both cases, `numberA` is still being incremented. There is just a difference of the value returned in the location of the call.

## Bitwise Operators
- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )
Used very rarely, for meddling with bits directly.

## Comma
Comma is rarely used as an operator but can be useful sometimes. When multiple operands are joined by comma, all expressions are evaluated but only the last one is returned.
```js
let a = (5 + 3, 4 + 2); // In this case, a = 6 because only the last value is returned.
```
Note: Comma has very low precedence, even below the assignment operator so whenever it is being used, putting the expression in brackets is highly recommended.

# Comparisons
All comparison operators return a boolean value:

- `true` – means “yes”, “correct” or “the truth”.
- `false` – means “no”, “wrong” or “not the truth”.
### Comparison Operators
- Greater/less than: `a > b`, `a < b`.
- Greater/less than or equals: `a >= b`, `a <= b`.
- Equals: `a == b`, please note the double equality sign `==` means the equality test, while a single one `a = b` means an assignment.
- Not equals: In maths the notation is `≠`, but in JavaScript it’s written as `a != b`.
- Strict Equals: `a === b` checks equality without type conversion. 

## Comparing Strings
We can compare strings using comparison operators. This is what the comparison algorithm looks like for strings.
1. Compare the first character of both strings.
2. If the first character from the first string is greater (or less) than the other string’s, then the first string is greater (or less) than the second. We’re done.
3. Otherwise, if both strings’ first characters are the same, compare the second characters the same way.
4. Repeat until the end of either string.
5. If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.
```javascript
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```

## Comparing Different Types
When comparing different types, all operands are converted into numbers.
```javascript
alert( '2' > 1 ); // true, string '2' becomes a number 2
alert( '01' == 1 ); // true, string '01' becomes a number 1
```
For boolean values, `true` becomes `1` and `false` becomes `0`.
```javascript
alert( true == 1 ); // true
alert( false == 0 ); // true
```
# Conditional Branching (if statements)
The `if` statement evaluates a condition within paratheses and executes a block of code.
```js
if (condition) {
// If condition is true, block of code inside here is exectued
Block of Code
}
```

All expressions within `if` are converted into parantheses.
```js
if (1 ) {} // Will always run
if (0) {} // Will never run
if (variable) {} // We can also pass variables that are already true/false or have conditions within them.
```

## Else
If condition is true, then the `if` block runs. An optional block can be added called `else` that runs when condition is **not** true.
```js
if (condition) {
	Block of Code // Will run if true
} else {
	Block of Code // Will run if false
}
```

## Else-If
If we want to validate multiple conditions, we can use `else-if`.
```js
if (condition A) {
	Block of Code // Will run if Condition A is true
} else if (condition B) {
	Block of Code // Will run if Condition B is true AND condition A is false
} else {
	Block of Code // Will run if both Condition A and B are false
}
```

## ? Operator
We can use a shorthand method to evaluate a condition and return either value A or value B using the ? operator.
```js
let result = condition ? value1 : value2;
// If condition is true, value 1 is returned
// If condition is false, value 2 is returned
if (condition) { // Long form of this expression
	result = value1;
} else {
	result = value2;
}
```
An example is necessary.
```js
let result = (55 > 54) ? true: false; // This is the shorthand
if (55>54) {
	result = true;
} else {
	result = false;
}
```

Just like with `if-else`, we can use multiple ? mark operators to evaluate multiple conditions.
```js
let result = (condition) ? value1 :
	(condition) ? value2 :
	(condition) ? value3 :
	value4;
// If statement version
if (condition1) {
	result = value1; 
} else if (condition2) { 
	result = value2; 
} else if (condition3) { 
	result = value3; 
} else { 
	result = value4; 
}
```
An example is really necessary.
```js
let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';
```
1. The first question mark checks whether `age < 3`.
2. If true – it returns `'Hi, baby!'`. Otherwise, it continues to the expression after the colon “:”, checking `age < 18`.
3. If that’s true – it returns `'Hello!'`. Otherwise, it continues to the expression after the next colon “:”, checking `age < 100`.
4. If that’s true – it returns `'Greetings!'`. Otherwise, it continues to the expression after the last colon “:”, returning `'What an unusual age!'`.
```js
// If Else version
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

## Switch Statements
`switch` statements can replace multiple `else if` statements and make code more readable.
```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```
- The value of `x` is checked for a strict equality to the value from the first `case` (that is, `value1`) then to the second (`value2`) and so on.
- If the equality is found, `switch` starts to execute the code starting from the corresponding `case`, until the nearest `break` (or until the end of `switch`).
- If no case is matched then the `default` code is executed (if it exists).
Note: **Switch statements don't naturally break if a case is true. It is recommended to add breaks at the end of each code block to properly emulate an if statement.**

An example.
```javascript
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small' );
    break;
  case 4:
    alert( 'Exactly!' );
    break;
  case 5:
    alert( 'Too big' );
    break;
  default:
    alert( "I don't know such values" );
}
```

You can also group cases.
```javascript
let a = 3;

switch (a) {
  case 4:
    alert('Right!');
    break;

  case 3: // (*) grouped two cases
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;

  default:
    alert('The result is strange. Really.');
}
```
<mark style="background: #ABF7F7A6;">Note: The equality check for switch case statements is always strict. It only matches if the types are the same.</mark>
# Loops
## While Loop
The `while` loop allows for repeating a code block *while* a code block is true.
```javascript
while (condition) {
  // code
  // so-called "loop body"
}
```
A single execution of a loop is called a **iteration**. An example using increments to actually end the loop after a few iterations.
```javascript
while (i < 3) { // shows 0, then 1, then 2
  alert( i );
  i++;
}
```
## Do... While...
The condition check can be moved _below_ the loop body using the `do..while` syntax.

```javascript
do {
  // loop body
} while (condition);
```

The loop will first execute the body, then check the condition, and, while it’s truthy, execute it again and again.
## For Loop
```javascript
for (begin; condition; step) {
  // ... loop body ...
}
```
For example, you can begin by defining a variable and giving it increment until condition is satisfied.
```javascript
for (let i = 0; i < 3; i++) { // shows 0, then 1, then 2
  alert(i);
}
```
All parts of a `for` loop can be removed. Removing the step makes it, functionally, into a while loop. Removing the condition makes it infinite.
```js
for (;;) { // Creates a infinite loop
	Code
}
```

You can manually break a loop using `break`. You can break the current iteration and skip to the next one using `continue`.
```javascript
for (let i = 0; i < 10; i++) {
	
  // if true, skip the remaining part of the body
  if (i % 2 == 0) continue;

  alert(i); // 1, then 3, 5, 7, 9
}
```

Note: Break and continue don't work with `?`.
You can label loops using `Label:`.
```js
labelName: for (...) {
  ...
}
```
Labels can be used to break loops. Note: All breaks must be *inside* the for loop to work.
```javascript
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // if an empty string or canceled, then break out of both loops
    if (!input) break outer; // (*)

    // do something with the value...
  }
}
```

# Logical Operators
There are four logical operators in JavaScript: `||` (OR), `&&` (AND), `!` (NOT), `??` (Nullish Coalescing).
### || OR
OR `||` returns true if any of the conditions are true, or else returns false. 
```javascript
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```
Generally used in if statements.
```javascript
if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'The office is closed.' ); // it is the weekend
}
```
Given mutliple OR values...
```javascript
result = value1 || value2 || value3;
```
- Evaluates operands from left to right.
- For each operand, converts it to boolean. If the result is `true`, stops and returns the original value of that operand.
- If all operands have been evaluated (i.e. all were `false`), returns the last operand.
```javascript
alert( 1 || 0 ); // 1 (1 is truthy)

alert( null || 1 ); // 1 (1 is the first truthy value)
alert( null || 0 || 1 ); // 1 (the first truthy value)

alert( undefined || null || 0 ); // 0 (all falsy, returns the last value)
```

#### Special Uses of OR
**Getting the first truthy value from a list of variables or expressions.**
```javascript
let firstName = "";
let lastName = "";
let nickName = "SuperCoder";

alert( firstName || lastName || nickName || "Anonymous"); // SuperCoder
```
**Short Circuit Evaluation**
We can use OR to only carry out the code if all the previous conditions are false. 
```javascript
true || alert("not printed");
false || alert("printed");
```

### && AND
AND `&&` returns true if both operands are true, and talse otherwise.
```javascript
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```
Given multiple AND operators...
```javascript
result = value1 && value2 && value3;
```
- Evaluates operands from left to right.
- For each operand, converts it to a boolean. If the result is `false`, stops and returns the original value of that operand.
- If all operands have been evaluated (i.e. all were truthy), returns the last operand.
The rules above are similar to OR. The difference is that AND returns the first _falsy_ value while OR returns the first _truthy_ one.
<mark style="background: #ABF7F7A6;">The precedence of AND </mark>`&&` <mark style="background: #ABF7F7A6;">operator is higher than OR</mark> `||`.

### Not !
Not `!` operator accepts a single argument.
1. Converts the operand to boolean type: `true/false`.
2. Returns the inverse value.
```javascript
result = !value;
```
Some examples.
```javascript
alert( !true ); // false
alert( !0 ); // true
```
A double not `!!` can be used to convert booleans. The first `!` one converts it into a boolean and inverses it. The second one inverses it again, back to it's original value.
```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```
<mark style="background: #ABF7F7A6;">The precedence of NOT</mark> `!`<mark style="background: #ABF7F7A6;"> is the highest of all logical operators, so it always executes first, before</mark> `&&` <mark style="background: #ABF7F7A6;">or</mark> `||`.

## ?? Nullish Coalesing
Nullish Coalesing `??` has a result of:
- if `a` is defined, then `a`,
- if `a` isn’t defined, then `b`. `a` is not defined when it has the value of `null` or `undefined`.
```js
let nullish = a ?? b;
nullish = result = (a !== null && a !== undefined) ? a : b; // Expanded form, without using nullish coalesing.
```
A common use case is if a value isn't defined. 
```js
let a;
alert(a ?? "Something");
```
We can chain `??` to select the first value that isn't `null` or `undefined`.
```javascript
nickname = "Supercoder";
// shows the first defined value:
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // Supercoder
```
<mark style="background: #ABF7F7A6;">The precedence of the</mark> `??` <mark style="background: #ABF7F7A6;">operator is the same as</mark> `||`.<mark style="background: #ABF7F7A6;"> They both equal 3 in the MDN table.</mark>
That means that, just like `||`, the nullish coalescing operator `??` is evaluated before `=` and `?`, but after most other operations, such as `+`, `*`.

<mark style="background: #ABF7F7A6;">As a general rule, always put stuff in parantheses. </mark>

Note: Due to safety reasons, **JavaScript forbids using** `??` together with `&&` and `||` operators, unless the precedence is explicitly specified with parentheses.
# Interaction
### Alert 
Creates a **modal** window (a modal window is a window that the user has to deal with before interacting with anything else on the page; they can't click anything until they resolve the window).
```js
alert("Hello"); // Creates a modal window that the user needs to press 'OK' to resolve
```

### Prompt
Creates a **modal** window with a title message, input field and a OK/Cancel button. It accepts two arguments, the *title* that will be the text that goes in the title message and *[default]*, an **optional** parameter that provides default text for the text box. The square brackets aren't required.
```js
let variable = prompt(title, [default]) // Syntax
let age = prompt("Enter your age: ", 0) // Example
```

Note, it is standard to put the default value as a blank string `''` because some browsers (e.g. IE) will manually insert text like `undefined` when no *[default]* text is given.

### Confirm
Creates a **modal** window with a question and OK/Cancel options. OK results in `true` and Cancel results in `false`. 
```js
confirm(question);
let cupcakes_are_delicious = confirm("Are cupcakes delicious?"); // Returns either true or false
```

# Functions
Functions allow us to re-use the same code multiple times. 
A function contains a name, parameters (the 'input') and a block of code within it. Parameters allow you to take values from outside the function and put them inside and utilize them. We can call functions by referencing it's name and brackets `functionName()` and enter the parameters (comma separated) in the brackets.
```javascript
function name(parameter1, parameter2, ... parameterN) { // This is how we define a function
 // body
}
name() // This is how we call a function
```
A **local variable** is a variable that is defined within a function and can only be used within a function. It is said to have a *local* **scope**.
```javascript
function showMessage() {
  let message = "Hello, I'm JavaScript!"; // local variable

  alert( message );
}

showMessage(); // Hello, I'm JavaScript!

alert( message ); // <-- Error! The variable is local to the function
```
A function can use outer variables too and modify them inside the function. If there is a local variable with the same name, the local variable overshadows the outer variable and replaces it.
Outer variables are variables with a *global* scope. That means that they can be used across the entire document.
```javascript
let userName = 'John';

function showMessage() {
  userName = "Bob"; // (1) changed the outer variable

  let message = 'Hello, ' + userName;
  alert(message);
}

alert( userName ); // John before the function call

showMessage();

alert( userName ); // Bob, the value was modified by the function
```

## Parameters
```javascript
function showMessage(from, text) { // parameters: from, text
  alert(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```
- A **parameter** is the variable listed inside the parentheses in the function declaration (it’s a declaration time term).
- An **argument** is the value that is passed to the function when it is called (it’s a call time term).
We can provide *default* values for parameters in case a value isn't assigned. This is convention to ensure your functions don't break.
```javascript
function showMessage(from, text = "no text given") {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```
You can also use other functions as default values or function arguments.
```javascript
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // its result becomes the value of text
}
```
We could also define the default within the function, with the cleanest approach being using the nullish coalesing operator `??`.
```javascript
function showCount(count) {
  // if count is undefined or null, show "unknown"
  alert(count ?? "unknown");
}

showCount(0); // 0
showCount(null); // unknown
showCount(); // unknown
```

## Returning a value
The `return` directive returns a value from the function back to the place it was called.
```javascript
function sum(a, b) {
  return a + b;
}
let result = sum(1, 2);
alert( result ); // 3
```
Using `return` without a value causes the function to exit immediately. 
<mark style="background: #FFB86CA6;">Note: A function that doesn't return anything or has a empty return returns undefined.</mark>
<mark style="background: #FF5582A6;">Note: Never add a newline for a statement of return, it assumes semicolon and makes it an empty return.</mark>

## Function Standards
These prefixes are used to summarise a part of the purpose of a function. This is convention and camelCase is expected.
- `"get…"` – return a value,
- `"calc…"` – calculate something,
- `"create…"` – create something,
- `"check…"` – check something and return a boolean, etc.
We must follow the **one function, one purpose** rule. A function should *only* do what it name says, it should never cross beyond its scope. To fulfil multiple purposes, create multiple functions.
It is also expected to have detailed comments explaining the parameters of a function and the purpose of each line/step.

## Function Expressions
Function expressions are an alternative to regular function definitions and allow functions to be defined in the middle of any expression.
```javascript
let sayHi = function() {
  alert( "Hello" );
};
```
The `sayHi` variable is getting the value `function(){ alert("Hello"); }`. The code transalates to "create a function and put it into the variable `sayHi`".
The name of the function is not created as this is what enables to use it as an expression. 

These expressions can be made in the middle of any operation or other expression. This makes them a very powerful, shorthand way of writing functions.
### Expression vs Declaration
_Function Declaration:_ a function, declared as a separate statement, in the main code flow:

```javascript
// Function Declaration
function sum(a, b) {
  return a + b;
}
```
- _Function Expression:_ a function, created inside an expression or inside another syntax construct. Here, the function is created on the right side of the “assignment expression” `=`:
```javascript
// Function Expression
let sum = function(a, b) {
  return a + b;
};
```

**A Function Expression is created when the execution reaches it and is usable only from that moment.**

Once the execution flow passes to the right side of the assignment `let sum = function…` – here we go, the function is created and can be used (assigned, called, etc. ) from now on.

Function Declarations are different.

**A Function Declaration can be called earlier than it is defined.**

For example, a global Function Declaration is visible in the whole script, no matter where it is.

Another special feature of Function Declarations is their block scope.

In strict mode, when a Function Declaration is within a code block, it’s visible everywhere inside that block. But not outside of it.
```javascript
let age = prompt("What is your age?", 18);

// conditionally declare a function
if (age < 18) {

  function welcome() {
    alert("Hello!");
  }

} else {

  function welcome() {
    alert("Greetings!");
  }

}

// ...use it later
welcome(); // Error: welcome is not defined
```
But, if we use a function expression (and simplify it using the `?` operator) in order to make it work outside the scope of the `if` statement too.
```javascript
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

welcome(); // ok now
```

As a rule of thumb, when we need to declare a function, the first thing to consider is Function Declaration syntax. It gives more freedom in how to organize our code, because we can call such functions before they are declared.

That’s also better for readability, as it’s easier to look up `function f(…) {…}` in the code than `let f = function(…) {…};`. Function Declarations are more “eye-catching”.

…But if a Function Declaration does not suit us for some reason, or we need a conditional declaration (we’ve just seen an example), then Function Expression should be used.
## Functions are a value
Just to note, functions are a value; even when defined or used as an expression. 
Functions can be printed to show the value.
```javascript
function sayHi() {   // (1) create
  alert( "Hello" );
}

let func = sayHi;    // (2) copy

func(); // Hello     // (3) run the copy (it works)!
sayHi(); // Hello    //     this still works too (why wouldn't it)
```
1. The Function Declaration `(1)` creates the function and puts it into the variable named `sayHi`.
2. Line `(2)` copies it into the variable `func`. Please note again: there are no parentheses after `sayHi`. If there were, then `func = sayHi()` would write _the result of the call_ `sayHi()` into `func`, not _the function_ `sayHi` itself.
3. Now the function can be called as both `sayHi()` and `func()`.

We can also replicate the exact same with a function expression.
```javascript
let sayHi = function() { // (1) create
  alert( "Hello" );
};

let func = sayHi;
```

## Callback Functions
Functions can be called as parameters of other functions, these functions are called **callback** functions.
```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```
The idea is that we pass a function and expect it to be “called back” later if necessary. In our case, `showOk` becomes the callback for “yes” answer, and `showCancel` for “no” answer.

We can significantly shorten the code using function expressions.
```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```

Here, functions are declared right inside the `ask(...)` call. They have no name, and so are called _anonymous_. Such functions are not accessible outside of `ask` (because they are not assigned to variables), but that’s just what we want here.

## Arrow Functions
We can write **function expressions** in a better way using arrow functions.
```javascript
let func = (arg1, arg2, ..., argN) => expression; // Same structure as a function expression, just shorthand

// The same as...
let func = function(arg1, arg2, ..., argN) {
  return expression;
};
```
An example.
```javascript
let sum = (a, b) => a + b;

/* This arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```
We can also create functions with only one parameter where we can remove the brackets to make it shorter. 
```javascript
let double = n => n * 2;
// roughly the same as: let double = function(n) { return n * 2 }

alert( double(3) ); // 6
```
If there are no arguments, you still have to add the brackets.
```javascript
let sayHi = () => alert("Hello!");

sayHi();
```
They can be used as function expressions in if statements as well.
```javascript
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello!') :
  () => alert("Greetings!");

welcome();
```
Arrow functions with curly braces can have multiple statements but need to return something. 
```js
let lordName = (name) => {
name = "Sir " + name;
return name;
} // Multiple statements

let lordName = name => name = "Sir" + name; // Same functionality.
```

# Reference
`alert()` - Displays a message with an OK button
`let` - Define variable
`const` - Define constant

# Snippets