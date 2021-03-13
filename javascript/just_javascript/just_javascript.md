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
