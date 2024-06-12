# Chapter 03: Working with Fundamental Data Types

## Operator Precedence and Associativity

A group of operators can be _left-associative_, which means operators execute
from left to right, or they can be _right-associative_, which means they execute
from right to left.

## Bitwise Operators

_Bitwise operators_ enable you to operate on an integer variable at the bit
level. Individual bits are often used as _flags_.

### The Bitwise Shift Operators

The bitwise _shift operators_ shift the contents of an integer variable by a
specified number of bits to the left or right. Bits that fall of either end of
the variable are lost.

```cpp
unsigned short number {16387};
auto result {static_cast<unsigned short>(number << 2)}; // shift left two bit positions
/*
    Original:       0100000000000011
    Shift left 2:   0000000000001100
    Shift right 2:  0001000000000000
*/
```

If you want to modify the original value of a variable using a shift operation.

```cpp
unsigned short number {16387};
number <<= 2; // equivalents to the upper
```

### Shifting Signed Integers

For negative numbers, right shift operators introduce `1` bits at the left to
fill vacated bit positions; for positive ones, `0` bits. This is known as _sign
extension_. The sign bit is propagated to maintain consistency between a right
shift and a divide operation.

```cpp
signed char positive {+104}; // 01101000
signed char negative {-104}; // 10011000
positive >>= 2; // 00011010 or +104 / 4
negative >>= 2; // 11100110 or -104 / 4
```

## Logical Operations on Bit Patterns

- `~`: The _bitwise complement operator_ is a unary operator that inverts the
  bits in its operand.
- `&`: The _bitwise AND operator_. If the corresponding bits are both 1, then
  the resulting bit is 1; otherwise, it's 0.
- `^`: The _bitwise exclusive OR operator_ (XOR). If the corresponding bits are
  different, then the result is 1. If the corresponding bits are the same, the
  result is 0.
- `|`: The _bitwise OR operator_. If either bit is 1, then the result is 1. If
  both bits are 0, then the result is 0.

The bitwise AND operator is used to select particular bits or groups of bits in
an integer value. For example, extract size and style of a font that is stored
in 2 bytes. Another use is to turn the bits off.

```cpp
unsigned short font {0b00000110'0'10'01100};
unsigned short size_mask {0x1F}; // 0b11111
auto size {static_cast<unsigned short>(font & size_mask)};
unsigned style_mask {0xFF00};
auto style {static_cast<unsigned short>(font & style_mask) >> 8};
```

The bitwise OR operator for setting one or more bits to 1.

```cpp
unsigned short font {0b00000110'0'10'01100};
auto italic {static_cast<unsigned short>(1u << 6)};
auto bold {static_cast<unsigned short>(1u << 5)};
font |= bold; // set bold to 1
font |= bold | italic; // set both to 1
```

The bitwise complement operator is used to flip each bit.

```cpp
auto bold {static_cast<unsigned short>(1u << 5)}; // 0000'0000'0010'0000
bold ~= bold; // 1111'1111'1101'1111
font &= ~bold; // set bold to 0
```

The bitwise XOR operator may be used to toggle or flip the state of individual
bits.

```cpp
font ^= bold; // toggle bold
```

## The Lifetime of a Variable

All variables have a finite _lifetime_. They come into existence from the point
at which you define them, and at some point they are destroyed. How long a
particular variable lasts is determined by its _storage duration_.

- Variables defined within a block that are not defined to be `static` have
  _automatic storage duration_. They exist from the point at which they are
  defined until the end of the block. They are referred to _automatic variables_
  or _local variables_. They are said to have _local scope_ or _block scope_.

- Variables defined using the `static` keyword have _static storage duration_.
  They are called _static variables_. They exist from the point that which they
  are defined and continue in existence until the program ends.

- Variables for which you allocate memory at runtime have _dynamic storage
  duration_. They exist from the point at which you create them until you
  release their memory to destroy theme.

- Variables declared with the `thread_local` keyword have _thread storage
  duration_. Thread local variables are an advanced topic.

The scope of a variable is the part of a program in which the variable name is
valid.

## Global Variables

Variables defined outside of all blocks and classes are called _globals_ and
have _global scope_. They have _static storage duration_ by default.

To access a global variable, qualify it with the _scope resolution operator_,
`::`.

## Enumerated Data Types

An _enumeration_ provides a limited set of possible values that can be usefully
referred to by name. The symbolic names between the braces are called
_enumerators_.

```cpp
enum class Day {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday};
Day today {Day::Monday}; // will have the value 0
```

You can specify the type of the enumerators like this:

```cpp
enum class Day : unsigned int {Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday};
enum class Punctuation : char {Comma = ',', Exclamation = '!', Question = '?'};
```

## Aliases for Data Types

The `using` keyword enables you to specify a _type alias_, which is your own
data type _name_ that serves as an alternative to an existing type name.

```cpp
using BigOnes = unsigned long long
BigOnes mynum{};

using PhoneBook = std::map<std::shared_ptr<Contact>, std::string>;
```
