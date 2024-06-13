# Chapter 04: Making Decisions

## Comparing Data Values

You can compare data values using two new sets of operators, namely _relational_
and _equality operators_.

In C++20, the _three-way comparison operator_ or _spaceship operator_, `<=>`,
was introduced in `<compare>` module.

```cpp
std::strong_ordering greater{2 <=> 0}; // std::strong_ordering::greater
std::strong_ordering less{-1 <=> 0}; // std::strong_ordering::less
std::strong_ordering equal{0 <=> 0}; // std::strong_ordering::equal
```

The `std::is_lt()`, `std::is_gt()` and `std::is_eq()` are so-called _named
comparison functions_, and are defined by the `<compare>` module.

## The `if` Statement

```cpp
if (condition) {
    // statement when condition is true
} else {
    // statement when condition is false
}
```

## Logical Operators

You use the AND operator, `&&`, when you have two conditions that must both be
`true` for a `true` result.

```cpp
if (letter >= 'A' && letter <= 'Z') {
    std::cout << "This is an uppercase letter." << std::endl;
}
```

You use the OR operator, `||`, when you want a `true` result when either or both
of the operands are `true`.

```cpp
if (income >= 100'000.00 || capital >= 1'000'000.00) {
    std::cout << "Of course, how much do you want to borrow?" << std::endl;
}
```

The negation operator, `!`, inverts the value of a single `bool` value.

```cpp
if (!false) {
    std::cout << "This line is ensured to print" << std::endl;
}
```

The XOR operator, `^`, return `true` if the both operands are different;
otherwise, return `false`.

```cpp
if ((age < 20) ^ (balance >= 1'000'000)) {}
if ((age < 20 || balance >= 1'000'000) && !(age < 20 && balance >= 1'000'000)) {}
```

## The Conditional Operator

The _conditional operator_ is sometimes called the _ternary operator_.

```cpp
condition ? expression1 : expressionb;
```

## The `switch` Statement

The `switch` statement enables you to select from multiple choices.

```cpp
switch (ticket_number) {
    case 147:
        std::cout << "You win first prize";
        break;
    case 387:
        std::cout << "You win second prize";
        break;
    case 29:
        std::cout << "You win third prize";
        break;
    default:
        std::cout << "Sorry, good luck for the next time.";
        break;
}
```

You can only `switch` on values of integral (`int`, `long`, `unsigned short`,
etc.), character (`char`, etc.) and enumeration types.

## Statement Blocks and Variable Scope

Any variable declared within a block ceases to exist at the end of the block, so
you cannot reference it outside the block.

Patterns where an extra scope (and indentation) is introduced to bind local
variables to `if` statements are relatively common. The additional
initialization _statement_ is executed prior to evaluating the `condition`
expression, the usual Boolean expression of the `if` statement.

```cpp
if (initialization; condition) {
    // the variable initialized exists in this block
}
```
