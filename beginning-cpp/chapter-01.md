# Chapter 01: Basic Ideas

## Modern C++

Created in the early 1980s by Danish computer scientist Bjarne Stroustrup. Every
three years, a new version of the standard is published. C++20 will again change
the way we program in C++ forever since C++11.

## Standard Libraries

The _Standard Library_ is a huge collection of routines and definitions that
provide functionality that is required by many programs.

## C++ Program Concepts

The names of source files usually have the extension `.cpp`, although other
extensions such as `.cc`, `.cxx`, or `.c++` are sometimes used to identify a C++
source file.

A C++ program consists of one or more functions, one of which is called
`main()`. Execution always starts with `main()`.

- _Functions_: A function is a named block of code that carries out a
  well-defined operation.Functions is reusable, easier to develop and test.

```cpp
int main() {}
```

- _Statements_: A statement is a basic unit in a C++ program. A statement always
  ends with a semicolon. You can enclose several statements between `{}`, which
  referred to as a _statement block_ or _compound statement_. Blocks can be
  placed inside other blocks - this concept is called _nesting_.

```cpp
int answer{42};
```

- _Namespaces_: A namespace is a sort of family name that prefixes all the names
  declared within the namespace, for example, `std`. `::` is called _the scoped
  resolution operator_.

```cpp
namespace my_space {
    // All names declared here
}
```

- _Names and Keywords_: A name can be any sequence letters A-Z, a-z, 0-9 and the
  underscore `_`. Keywords are reserved words that have a specific meaning in
  C++, such as `class`, `int`, `namespace`, ...

- _Classes and Objects_: A class is a block of code that defines a data type. An
  item of data of a class type is referred to as an object.

- _Templates_: A template is a recipe that you create to be used by the compiler
  to generate code automatically for a function or class customized for a
  particular type or types. The compiler use a _function template_ to generate
  one or more of a family of functions. It uses a _class template_ to generate
  classes.

## Procedural and Object-Oriented Programming

- Procedural programming: Focus on the process that your program must implement
  to solve the problem.

- Object-oriented programming: Determine what types of objects the problem is
  concerned with. It's easier to understand and maintain.

## Representing Numbers

### Decimal Numbers

Use `decimal notation` to represent numbers using base 10.

### Binary Numbers

Representing numbers using base 2 is called the _binary system_ of counting.

If you have n bits available, you can represent 2^n integers, with positive
values from 0 to 2^n - 1.

### Hexadecimal Numbers

Use `hexadecimal notation` to represent numbers using base 16.

A byte is 8 bits, which is exactly two hexadecimal digits.

### Negative Binary Numbers

Each number consists of a sign bit that is 0 for positive values and 1 for
negative values, plus a given number of other bits that specify the _magnitude_
or absolute value of the number (the value without the sign, in other words).
This is called a _signed magnitude_.

Virtually all modern computers use the so-called _two's complement
representation_ of negative binary numbers.

1. You start with +8 in binary: `00001000`.
2. You then "flip" each binary digit: `11110111`.
3. If you now add 1 to this, you get the two's complement form of -8:
   `11111000`.

### Octal values

Octal integers are numbers expressed with base 8. Digits in an octal value can
only be from 0 to 7. `076` is an octal value that corresponds to 62 in decimal.

> Never write decimal integers in your source code with leading zero.

### Big-Endian & Little-Endian System

The most significant eight bits of the value are stored in the byte with the
highest address, and the least significant eight bits are stored in the byte
with the lowest address, which is the leftmost byte. This arrangement is
described as _little-endian_.

The bytes are in reverse sequence. This arrangement is described as
_big-endian_.

### Floating-Point Numbers

A so-called normalized number consists of two parts: a _mantissa_ or _fraction_
and an _exponent_. Both can be either positive or negative. For example,
`3.650000E02 = 3.650000 x 10^2`.

Floating-point numbers in general are only approximate representations of the
exact number.

Take care when adding or subtracting numbers of significant different magnitudes
like `3.650000E+06 + 1.230000E-04 = 3.650000E+06`.

Take care when the numbers are nearly equal. Most numbers may cancel each other
out, and you may end up with a result that has only one or two digits of
precision. This is referred to as _catastrophic cancellation_.

Left to right, each floating-point number then consists of a single sign bit,
followed by a fixed number of bits for the exponent, and finally another series
of bits that encode the mantissa. The most common floating-point numbers
representations are the so-called _single precision_ (1 sign bit, 8 bits for the
exponent, and 23 bits for the mantissa, 32 bits in total) and \_double precision
(1 + 11 + 52, 64 bits) floating-point numbers.

## Representing Characters

Each character is assigned an unique integer value called its _code_ or _code
point_.

### ASCII Codes

It is a 7-bit code, so there are 128 different code values.

### UCS and Unicode

UCS defines a mapping between characters and integer code values, called _code
points_. An encoding specifies a way of representing a given code point as a
series of bytes or words.

Unicode is a standard that defines a set of characters and their code points
identical to those in UCS. The range of code points is more than enough to
accommodate the character sets for all the languages in the world, as well as
many different sets of graphical characters such as mathematical symbols, or
even emoticons and emojis. The most commonly used encodings are referred to as
UTF-8, UTF-16 and UTF-32.
