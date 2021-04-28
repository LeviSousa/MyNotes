# About Ruby

Official website: https://www.ruby-lang.org/en/

Ruby is a programming language. It is purely Object-Oriented, meaning everything is an object. Manipulations on those same objects also return other objects.

Every method in Ruby also returns something. If a method does not return anything explicitly, then `nil` is returned.

## Running Ruby code

To run a ruby file:

```bash
$ ruby ruby_file.rb
```

## Strings

Strings can be defined using single or double quotes. However, only the latter allows for string interpolation.

```ruby
# String interpolation
"My first name is #{first_name}"
```

Single quoted strings are lighter, but also do less. Besides not being able to do string interpolation, single quoted strings can't also escape special characters (_e.g._ `/n`).

## Numbers

Integers have a `to_f` method, that can be invoked, returning a float representation. However, if the object cannot be converted to a float, it will return `0`. The same happens on `to_i` (converting to an integer).

Another useful method is the `.times`, which takes a block of code:

```ruby
20.times { print '-' }
```

## Variables

To declare a variable in Ruby, it is just required that the variable name and its value be written. Variables can, then, be overridden.

```ruby
count = 10 # this declares the variable "count"
count = 20 # this overrides the variable "count"
```

Variables' naming in Ruby has the following rules:
- Starting with lower case letter or underscore:
    - Local variables
    - Method parameters
    - Method names
- Starting with an @ sign:
    - Instance variables
- Starting with an upper case letter (and separating words with capitalization):
    - Class names
    - Module names
    - Constants (here `SCREAMING_SNAKE_CASE`)

## Symbols

`Symbols` are most often used when naming method parameters and looking up values in hashes. They are defined by a `:` next to its name. Example:

```ruby
# :action and :id are naming paramets, while [:id] is reading from an hash
redirect_to :action => 'edit', :id => params[:id]

# however, the most common form is:
redirect_to action: 'edit', product: product.id
```

## Arrays

`Arrays` are indexed collections, where the key is an integer, indicating the index on the array, starting with `0`.

Reading from an `Array` is more efficient than reading from an `Hash`. However, the former is less flexible to work with.

Appending an object to an `Array` can be done by using `<<`:

```ruby
an_array << appending_object
```

There are two ways to create an `Array` of strings:

```ruby
animals = ['ant', 'bee', 'cat', 'dog', 'elk']

# However, the most idiomatic way is:
animals = %w{ant bee cat dog elk}
```

## Hashes

As with `Arrays`, an `Hash` is an indexed collection. However, any object can be a key, even `Symbols`, which the most frequent choice.

```ruby
instrument_section = {
  :cello => 'string',
  :clarinet => 'woodwind'
}

# As seen in the Symbols section, this can be written as:
instrument_section = {
  cello: 'string',
  clarinet: 'woodwind
}
```

Reading a non-existing key from an `Hash` will return `nil`.
## Classes



## Methods

Methods are defined starting with the `def` keyword, and ending with the `end` keyword.

```ruby
def method_name(arg1, arg2)
    # method body
end
```

If a method does not have arguments, then it can be invoked without using empty parentheses `()`. This is also possible when method chaining:

```ruby
10.to_s.class
```

The last evaluated expression in a method will be implictly returned.

When invoking a method with an `Hash`, the curly braces - of the `Hash` - can be omitted only if the last parameter of the method is an `Hash`.

## Objects

To instantiate an object from a `Class`, the `.new` method is invoked from that `Class`.

To get all the methods of an object, `methods` can be called directly on that same object. This will work with primitives as well, since they are objects (everything in Ruby is).

## Equality

To test equality between objects, a lot of operations can be performed:

- `==` will return `true` if both objects are the same. It is typically overridden to provide class-specific meaning`
- `.equal?` works as the default `==`, but should never be overridden
- `.eql?` will return `true` if both objects' hashes are equal. So, if `eql?` is overriden in an object, so too should its `.hash`.

Official description can be found [here](https://ruby-doc.org/core-3.0.1/Object.html#method-i-eql-3F) and, for `===` specific, [here](https://ruby-doc.org/core-3.0.1/Object.html#method-i-3D-3D-3D).

## Input/Output

### Getting input from console

To get input from console:

```ruby
user_input = gets.chomp
```

`gets.chomp` will always return a string.

### Logging

Three possible ways to log a value to output (usually console) are `p`, `puts` and `print`. They are similar, but with some differences.

`puts` is short for "put string". It will log the value on its right and add a new line after it. It returns `nil`.

`print` will work like `puts`, except **it will not add a new line**.

`p` will output a more "raw" version of the provided object and is useful for debugging, as somethings that are "invisible" in the other two methods are visible when using `p` (like new lines). It will also return the provided value.

`pp` is another method used for logging. It works like `p`, but will log big hashes and arrays in a more readable way.

(More info can be found here: https://www.rubyguides.com/2018/10/puts-vs-print/)

## Miscellaneous notes

### Comments

Comments are written using `#`:

```ruby
# this is a comment
```
