# Description

These are my notes on [Dan Abramov](https://twitter.com/dan_abramov)'s and [Maggie Appleton](https://twitter.com/Mappletons)'s course **Just Javascript**.

### Instructors brief bio

Dan Abramov works for Facebook as part of the React Core team. He also developed Redux along with Andrew Clark.

Maggie Appleton is an Art Director, Designer and Anthropologis at egghead.io.

# 01. Mental Models
*Purpose of the course - What is a mental model - How mental models may not correspond to reality - Reading code fast, and slow*

Given the following snippet, what are the values of `a` and `b`?

```javascript
let a = 10;
let b = a;
a = 0;
```

A Mental Model is composed of a "set of deep-rooted analogies", or "a combination of visual, spatial, and mechanical mental shortcuts", that allows us to be *really sure* of what the values of `a` and `b` are (`0` and `10`, respectively).

The parts that form our Mental Models are born out of many different places. They may be related to programming, or not. If they are, they may be borne out of a recent article we've read or of a tutorial we've completed early in our education. However they are formed and grown, our Mental Models influence how we read and interpret code.

Those Models may, also, be wrong. The **Just Javacript** course aims rebuild them.

An analogy is made with Daniel Kahneman's book ["Thinking, Fast and Slow"](https://www.amazon.com/Thinking-Fast-Slow-Daniel-Kahneman/dp/0374533555):

- "reading code fast" may lead to not detecting bugs, since our brain is relying on variable naming, comments and structure
- "reading code slow" forces us to get deep in the analysis of code, reading it line by line

It is when we're "reading code slowly" that Mental Models come into frame, as they're what will influence our interpretation of how the code will be run. As Mental Models may be incomplete, or wrong, so may our interpretation.

```javascript
function duplicateSpreadsheet(original) {
  if (original.hasPendingChanges) {
    throw new Error('You need to save the file before you can duplicate it.');
  }
  let copy = {
    created: Date.now(),
    author: original.author,
    cells: original.cells,
    metadata: original.metadata,
  };
  copy.metadata.title = 'Copy of ' + original.metadata.title;
  return copy;
}
```
In the `duplicateSpreadsheet` function above, we may not notice that the original file's name is being changed to "Copy of ${name}" when we read it "fast". Knowing that a bug - change of the original name - exists, switches our mode of reading to be "slow". It is then that our Mental Models will allow us to correctly (or incorrectly, or not at all, dependending on its accuracy) identify the source and cause of the bug.

# 02. The Javascript Universe
*The two kinds of values - The nine types of values - Checking the type of a value*

In Javascript, there are two **kinds** of values: **Primitive Values** and **Objects and Functions**.

The former - **primitive values** - include numbers and strings. **They can't be affected by anything in the code.**

The latter - **objects and functions** - include arrays, objects and functions. **Code can manipulate them.**

Adding to the **kinds** of values, Javascript also has **Expressions**. These are operations that result in a value, like `2 + 2` or `Hello ${name}!`.

The two **kinds** of values are distributed among nine fundamental **Types**:

- *Primitive Values*
  - **Undefined** - used for unintentionally missing values
  - **Null** - used for intentionally missing values
  - **Booleans** - used for logic operations
  - **Numbers** - used for math calculations
  - **Strings** - used for text
  - **Symbols** - used to hide implementation details
  - **BigInts** - used for math on big numbers
- *Objects and Functions*
  - **Objects** - used to group related data and code
  - **Functions** - used to refer to code

To check the type of a value, Javascript gives the `typeof` function. It can be invoked without parens, but, when done so, they may lead to ambiguity:

```javascript
console.log(x => x * 2)
// This will result in a "Uncaught SyntaxError: invalid arrow-function arguments"
// error being thrown.

console.log((x => x * 2))
// This will log 'function', as expected
```

Note that invoking `typeof(null)` will return "object" instead of the expected "null". That is due to an [old bug in Javascript](https://stackoverflow.com/questions/18808226/why-is-typeof-null-object).

There are no other fundamental value types, besides the nine listed above. Arrays are objects, as are dates and regular expressions, for instance.

A common misconception in Javascript is that *"everything is an object"*. But that is not true, although it may seem like it. When `"hi".toUpperCase()` is invoked, `"hi"` is not an object. Rather, javascript creates a wrapper object around it and then discards it.

# 03. Values and Variables
*Immutability of primitive values - Definition of Variable - Assignment of values to variables - Variables as expressions when invoking functions and assigning other variables*

As stated in lesson 02, Primitive Values can't be changed. They are immutable. Javascript will silently refuse, or error, the changing attempt.

Primitive values can't also have properties be set on them (*e.g.* `"h1".length = 3` will not work).

A new concept is introduced: the **Variable**. These are *declared* and, after that, can be *assigned* to values. After the initial assignment, variables can be assigned to other values.

```javascript
let x // variable "x" is declared
x = 10 // variable "x" is assigned to the value 10
x = 20 // variable "x" is re-assigned to the value 20
```

**An Assignment is, thus, a "relationship"**. On that relationship:
- the left side **must** be a variable
- the right side **must** be an expression. When the expression resolves to a primitive value, it is called a *Literal*.

When invoking a function, where the parameter is a variable (*i.e.* `console.log(x)`), it is not, in fact, the variable that is "passed in". *Functions are invoked with values*. When a variable is used, the function is **invoked with the current value assigned to the variable**. At this point, a variable also serves as an expression.

The example below demonstrates this:

```javascript
function double(x) {
  x = x * 2;
}

let money = 10;
double(money); // here, "double" will retrieve the value assigned to "money"
console.log(money); // will log 10, as "money" was not passed to "double"
```

As variables always point to values, `let y = x` means to assign to "y" the current value assigned "x" - and not to the variable "x".

# 04. Counting the Values (Part 1)
*The values of undefined - The values of null - The values of boolean - The values of number - Floating-point math and limited precision - Floating-point math special numbers*

Part 04 of this tutorial lists and describres the values that exist in each Value Type.

## Undefined

The Undefined type only has one possible value: `undefined`. Despite its name, **it is a value** and, as stated in Lesson 02, it conventionally represents *unintentionally missing values*.

However, the `undefined` value must be distinguished from a variable not yet defined - as what happens when accessing a value before its declaration. That will result in a `ReferenceError` as per example below:

```javascript
console.log(undefinedVar) // will log ReferenceError
let undefinedVar
console.log(undefinedVar.a) // will log TypeError
```

As observed in the example, properties cannot be read from `undefined` values.

## Null

Null type also only has one value: `null`. Also, like `undefined`, it will throw a `TypeError` if a property is attempted to be read from it. It represent an *intentionally missing value*, as per convention.

Also, as stated in Lesson 02, `console.log(typeof(null))` will log `object`. But this is a bug in Javascript, and `null` is its own Type.

## Boolean

The Boolean type has two possible values: `false` and `true`.

## Number

The Number type represent numerical values. However, when used by Javascript, they are somewhat different from the normal, human-usable, numbers. That is because Javascript applies *floating-point math* and it considers numbers to have *limited precision*.

When a number is written in the Javascript code, Javascript looks for the closest number that it knows about (from a pool of 18 quintillion numbers). *For most integers*, the number Javascript finds is exactly equal to the one that was written. However, as the written number distances itself from 0 - whether positive or negative - Javascript will find less exact values (losing precision).

The primitive wrapper object [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) provides a `MAX_SAFE_INTEGER` and a `MIN_SAFE_INTEGER`, representing the values that, between both, are exact in Javascript.

Floating points, however, *are not exact for Javascript*. Even 0.1 is not. The practical consequence of this is the fact that 0.1 + 0.2 !== 0.3, but rather 0.1 + 0.2 === 0.30000000000000004. This may be a source of bugs.

Floating-point math, however, works well (in the human sense) most of the time. As such, we rarely have to worry about it.

There are also some particular values resulting from adopting floating-point math:
- `Infinity`
- `-Infinity`
- `NaN`
- `-0`

They all have type of `number`. Of these [`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN) - standing for `Not-A-Number` is particulary curious as, despite its name, it is a number for Javascript. It represents *invalid numbers*.

# 05. Counting the Values (part 2)
*The values of BigInts - The values of Strings - How to declare Symbols - Creation an destruction of objects and functions - Functions as objects - Call Expression*

## BigInts

BigInts purpose is to represent very large numbers, as a regular `number` can't perform that task with accuracy. There is no maximum value for a BigInt, as it can represent any large number (at a speed and memory cost).

As this type is a fairly recent addition to Javascript, [it may not work in old browsers](https://caniuse.com/?search=bigint).


## Strings

Strings represent text and they may be written using double quotes (`""`), single quotes (`''`) or backticks (``).

Although Strings are not objects, they are provided with properties. These may, for example, get the length of the string (`.length`) or get the character at a given position (`[6]`). Since Strings are primitive, however, these properties can't be used to change its value (*e.g.* `"a string"[3] = "b"` will not change the string).

## Symbols

Symbols are a recent addition to Javascript, and they are declared by using `Symbol()`. They are skipped during this module.

## Objects

Objects include non-primitive values, like objects, arrays, RegExps and dates. As they are not primitive, objects are, by default, mutable. Their properties can be accessed via a dot ("dot notation") or brackets ("bracket notation").

For the purposes of the mental model, proposed for this course, objects are infinitely created upon their declaration (as opposed to primitive values which - again, for the purposes of this course - already exist). However, although they may be created, objects cannot be destroyed by running code.

Notwithstanding, Javascript is a garbage-collected language, and it will eventually destroy an object if there is no way in the code to reach it. When this happens, however, is not guaranteed.

## Functions

Functions are not primitives. As with objects, a new function is created every time it is declared, *even if in literal form*.

```javascript
for (let i = 1; i < 7; i++) {
  console.log(6) // here, the same value is used in every iteration
}

for (let i = 1; i < 7; i++) {
  console.log({}) // here, a new empty object is created in every iteration
}

for (let i = 1; i < 7; i++) {
  console.log(function () {}) // here, a new function is created in every iteration
}
```

Technically, Functions are Objects in Javascript but, crucially, they have unique capabilities. As objects, they can be re-assigned to a new variable (keeping the previous assignment still valid). However, as functions, they can be called, by invoking its name followed by parens. This is called a "call expression".

When a call expression is run, Javascript will, in turn, run the code of the function and retrieve the value returned from it.
