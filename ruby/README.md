# About Ruby

Official website: https://www.ruby-lang.org/en/

Ruby is a programming language. It is purely Object-Oriented, meaning everything is an object.

Everything method in Ruby also returns something. If a method does not return anything explicitly, then `nil` is returned.

## Running Ruby code

To run a ruby file:

```bash
$ ruby ruby_file.rb
```

## Strings

Strings can be defined using single or double quotes. However, only the latter allow for string interpolation.

```ruby
# String interpolation
"My first name is #{first_name}"
```

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

## Objects

To get all the methods of an object, `methods` can be called directly on that same object. This will work with primitives as well, since they are objects (everything in Ruby is).

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
