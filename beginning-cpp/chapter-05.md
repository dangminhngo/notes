# Chapter 05: Arrays and Loops

## Arrays

An _array_ is a variable that represents a sequence of memory locations, each
storing an item of data of the same data type. The data values are called
_elements_. The elements of an array are stored in one contiguous block of
memory.

The number of elements specified between the brackets is the _size_ of the array
that must always be specified using a _constant integer expression_.

You refer to an array element using an integer called an _index_.

```cpp
double temperatures[366]; // define an array of 366 double elements, just junk values
temparatures[3] = 99.0;

unsigned int heights[6] {26, 37, 12, 14, 52, 62};
```

## Understanding Loops

A _loop_ is a mechanism that enables you to execute a statement or block of
statements repeatedly until a particular condition is met. A single execution of
a loop's body is called an _iteration_.

## The `for` Loop

The `for` loop generally executes a statement or block of statements a
predetermined number of times.

```cpp
for (initialization; condition; iteration) {
    // loop statements
}
// next statement
```

## Avoiding Magic Numbers

A safer solution is to define a `const` variable for the array size and use that
instead of the explicit value.

```cpp
const size_t size{12};
double rainfall[size] {1.1, 1.2, 2.3, 1.8, 4.5, 2.1, 3.5, 4.8, 0.0, 0.3, 0.6, 0.7};
double copy[size] {};
for (size_t i {}; i < size; ++i) {
    copy[i] = rainfall[i];
}
```

## Defining the Array Size with the Braced Initializer

You can omit the size of the array when you supply one or more initial values in
its definition.

```cpp
int values[] {2, 3, 4};
```

## Determine the Size of an Array

You can use `std::size()` function provided by the `<array>` module of the STL.

```cpp
std::cout << std::size(values); // 3
```

## Controlling a `for` Loop with Floating-Point Values

You can use floating-point values to control the `for` loop but you need to be
careful when using a floating-point variable to control a `for` loop. Fractional
values may not be representable exactly as a binary floating-point number. This
can lead to some unwanted side effects.

```cpp
for (double radius{2.5}; radius <= 20.0; radius += 2.5) {
    std::cout << std::format("radius = {:4.1f}, area = {:7.2f}\n",
                             radius, std::numbers::pi * radius * radius);
}
```

No number that is a fraction with an odd denominator can be represented exactly
as a binary floating-point value.

The _comma_ operator combines two expressions into a single expression, where
the value of the operation is the value of its right operand.

## The Range-Based `for` Loop

The _range-based_ `for` loop iterates over all the values in a range of values.

```cpp
for (auto x : values) {
    total += x;
}
```

## The `while` Loop

The `while` loop uses a logical expression to control execution of the loop
body.

```cpp
initialization;
while (condition) {
    body
    iteration;
}
```

## The `do-while` Loop

The `do-while` loop is similar to the `while` loop, but the loop condition is
checked at the end of the loop. The loop statement is always executed at least
once.

```cpp
do {
    // loop statements
} while (condition);
```

## Nested Loops

You can place a loop inside another loop. You can nest loops within loops to
whatever depth you require to solve your problem.

## Skipping Loop Iterations

The `continue;` statement enables you to skip one loop iteration and press on
with the next.

## Breaking Out of a Loop

Executing a `break` statement within a loop ends the loop immediately, and
execution continues with the statement following the loop. The `break` statement
is often used with an _indefinite loop_. An _indefinite loop_ can potentially
run forever.

```cpp
for (;;) {
    // statements
}

while (true) {
    // statements
}
```

## Arrays of Characters

An array of elements of type `char` can have a dual personality. It can simply
be an array of characters, in which each element stores one character, or it can
represent a string. The _null character_ `\0` marks the end of the string.
