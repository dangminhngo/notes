# Chapter 2: Introducing Fundamental Types of Data

## Variables, Data, and Data Types

A variable is a named piece of memory that you define. Each variable stores data
only of a particular type.

### Defining Integer Variables

The variable will contain some arbitrary junk value if you don't specify an
initial value when you define the variable.

There are 3 types of initializing a variable. The braced initializer form is
slightly safer when it comes to so-called _narrowing conversions_.

```cpp
int apple_count{5}; // braced initializer
int lemon_count(4); // functional notation
int total_count = 12; // assignment notation
```

### Zero Initialization

You could omit the 0 in the braced initializer, the effect would be the same.

```cpp
int count {}; // count = 0
```

### Defining Variables with Fixed Values

The `const` keyword tells the compiler that the value of the variable must not
changed. It is a _constant_.

```cpp
const unsigned toe_count {10};
```

## Integer Literals

### Decimal Literals

You can write integer literals in a very straightforward way.

```cpp
unsigned long age {99UL};
unsigned short price {10u};
long long distance {15'000'000LL};
```

### Hexadecimal Literals

You prefix a hexadecimal literal with `0x` or `0X`.

```cpp
unsigned int color {0x0ff1ce};
int mask {0xFF00FF00};
unsigned long value {0xDEADlu};
```

### Octal Literals

You identify a number as octal by writing it with a leading zero. For example:
`0657`.

### Binary Literals

You write a binary integer literal as a sequence of binary digits (0 or 1)
prefixed by either `0b` or `0B`.

```cpp
int binary = 0b11110101;
int another_binary = 0B10101010;
```

## Calculations with Integers

An operation such as addition or multiplication is defined by an _operator_. The
values that an operator acts upon are called _operands_.

The computer will simply discard the fractional part in the following code.

```cpp
int numerator = 11;
int quotient = numerator / 4; // 2.75 -> 2
```

### Compound Arithmetic Expressions

Multiplication, division and modulus operations always execute before addition
and subtraction.

You can control the order in which more complicated expressions are executed
using parentheses.

## Assignment Operations

The value of a variable that is defined without the `const` qualifier can always
be overwritten with a new value. This is an _assignment statement_, and the = is
the _assignment operator_.

### The op= Assignment Operators

The op= _assignment operators_, or also _compound assignment operators_, are so
called because they're composed of an operator and an assignment operator =.

```cpp
feet %= feet_per_yard;
// <=> feet = feet % feet_per_yard
```

## The sizeof Operator

The sizeof operator is used to obtain the number of bytes occupied by a type, by
a variable, or by the result of an expression.

```cpp
sizeof(int); // 4

unsigned long height {12L};
sizeof(height); // 8
sizeof(height * height / 2); // 8
```

## Incrementing and Decrementing Integers

The prefix form of `++`/`--` increments/decrements the variable to which it
applies **when** its value is used in context.

The postfix form of `++`/`--` increments/decrements the variable to which it
applies **after** its value is used in context.

## Defining Floating-Point Variables

You can use the `unsigned` or `signed` modifiers with floating-point types; they
are always signed.

## Floating-Point Calculations

C++20 STL provide `<numbers>`, a module that defines several common mathematical
constants. For example: `std::numbers::e`, `std::numbers::pi`,
`std::numbers::sqrt2`, `std::numbers::phi`, ...

The `<cmath>` STL header defines a larger selection of trigonometric and
numerical functions that you can use in your programs. It also provides all
basic trigonometric functions (`cos()`, `sin()`, `tan()`). Angles are always
expressed in radians.

### Invalid Floating-Point Results

Floating-point operations in most computers are implemented according to the
IEEE 754 standard. So in practice, compilers generally behave quite similarly
when dividing floating-point numbers by zero.

Pitfalls:

- Many decimal values don't convert exactly to binary floating-point values.
- Taking the difference between two nearly identical values will lose precision.
- Working with values that differ by several orders of magnitude can lead to
  errors.

## Mix Expressions and Type Conversion

The compiler will arrange to convert one of the operand values to the same type
as the other. The operand to be converted will be the one with the lower rank.
These are called _implicit conversions_.

```cpp
1. long double
2. double
3. float
4. unsigned long long
5. long long
6. unsigned long
7. long
8. unsigned int
9. int
```

## Explicit Type Conversion

To explicitly convert the value of an expression to a given type, use
`static_cast<type_to_convert_to>(expression)`.

```cpp
int y {};
double z {5.0};
y = static_cast<int>(z);
```

## Formatting Strings

You can change the way an output stream formats data using _stream
manipulators_. You can tweak the number of decimal digits the stream uses to
format floating-point numbers with the `setprecision()` manipulator of the
`<iomanip>` module.

### std::format()

The first argument to `std::format()` is always the _format string_. This string
contains any number of _replacement fields_, each surrounded with a pair of
curly braces, `{}`. The format string is followed by zero or more additional
_arguments_, generally one per replacement field.

A format specifier is a seemingly cryptic sequence of numbers and characters,
introduced by a colon, telling `std::format()` how you would like the
corresponding data to be formatted. By default, this integer specifies the
_total number of significant digits_, counting digits **both before and after**
the decimal point.

```cpp
double pond_diameter {10.7654};
std::cout << std::format("Pond diameter is {:.2} feet.\n", pond_diameter ); // 11
```

You can instead make the precision specify the number of digits **after** the
decimal point by enabling so-called "fixed-point" formatting of floating-point
numbers.

```cpp
double pond_diameter {10.7654};
std::cout << std::format("Pond diameter is {:.2f} feet.\n", pond_diameter ); // 10.77
```

The general form of the format specifiers:
`[[fill]align][sign][#][0][width][.precision][type]`

- _fill_: the character will be filled in spaces if any.
- _align_: left `<`, right `>` and center `^`
- _sign_: a single character that determines what is printed in front of
  non-negative numbers.
- _\#_: toggles the so-called alternate form. For integer, the alternate form
  adds a _base prefix_: `0x, 0b, 0X, 0B, ...`
- _0_: adds 0 in front of value
- _width_: the width of formatting string (includes all specifiers)
- _.precision_: the number of significant digits
- _type_: specifies format type

An argument index can be added to the left of the colon of each replacement
field to match the argument position.

```cpp
std::cout << std::format("{1:.2f} feet is the diameter required for a pond with {0} fish.\n", fish_count, pond_diameter);
```

## Finding the Limits

The `<limits>` STL module makes the upper and lower limits for various types
available for all the fundamental data types.

```cpp
std::numeric_limits<double>::max();
std::numeric_limits<double>::min(); // min positive
std::numeric_limits<double>::lowest(); // min negative
```

You can retrieve many other items of information about various types.

```cpp
std::numeric_limits<type_name>::digits; // the number of binary digits, or bits
```

## Working with Character Variables

Variables of type `char` are used primarily to store a code for a single
character and occupy 1 byte.

You define wide-character literals in a similar way to literals of type `char`.
You can use types `char8_t`, `char16_t` or `char32_t` instead.

```cpp
wchar_t z {L'Z'};
wchar_t cc {L'\x00E7'};

char8_t yen {u8'\x00A5'}; // UTF-8
char16_t yen {u'\x0394'}; // UTF-16
char32_t yen {U'\x044f'}; // UTF-32
```

## The `auto` Keyword

You use the `auto` keyword to indicate that the compiler should deduce the type
of a variable.

```cpp
auto m {10}; // int
auto n {200UL}; // unsigned long
auto p {std::numbers::pi}; // double
```
