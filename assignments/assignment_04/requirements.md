# Assignment 4: Binary ↔ Decimal Converter

## Objective

Write a C++ program that allows the user to convert numbers between **binary and decimal**.

Your program will give the user a menu with three choices:

```text
1. Convert binary to decimal
2. Convert decimal to binary
3. Exit
```

The program should continue displaying the menu until the user chooses **3**.

## Requirements

### Option 1: Binary → Decimal

Ask the user to enter a binary number, such as:

```text
1101
```

While converting the number, **check that it is a valid binary number**. A valid binary number contains only the digits `0` and `1`.

For example:

```text
1101  → valid
10101 → valid
1201  → invalid
102   → invalid
```

If the number is invalid, display an appropriate error message and return to the menu.

#### How to convert binary to decimal

Binary is a base-2 number system. Each digit represents a power of 2, starting with \(2^0\) at the rightmost position.

For example, convert binary `1101` to decimal.

**Step 1: Identify the place values.**

Starting from the right, the place values are 1, 2, 4, and 8.

| Binary digit | 1 | 1 | 0 | 1 |
|---|---:|---:|---:|---:|
| Place value | 8 | 4 | 2 | 1 |
| Digit × place value | 8 | 4 | 0 | 1 |

**Step 2: Multiply each digit by its place value.**

- Rightmost digit: \(1 \times 1 = 1\)
- Next digit: \(0 \times 2 = 0\)
- Next digit: \(1 \times 4 = 4\)
- Leftmost digit: \(1 \times 8 = 8\)

**Step 3: Add the results.**

\(8 + 4 + 0 + 1 = 13\)

Therefore, binary `1101` equals decimal `13`.

#### How to do this in C++

You do not need to examine each digit manually. Use a loop to process the number one digit at a time.

1. Use `% 10` to obtain the rightmost digit.
2. Check whether the digit is `0` or `1`. If it is neither, the number is invalid.
3. Multiply the digit by the current place value and add the result to the decimal total.
4. Start with a place value of `1`. After each digit, multiply the place value by `2`.
5. Use `/= 10` to remove the rightmost digit.
6. Repeat until there are no digits left.

For example, processing `1101` from right to left:

| Current number | Rightmost digit | Place value | Contribution |
|---:|---:|---:|---:|
| 1101 | 1 | 1 | 1 |
| 110 | 0 | 2 | 0 |
| 11 | 1 | 4 | 4 |
| 1 | 1 | 8 | 8 |

The total is `13`.

**Important:** Make a copy of the original number before processing it. The loop changes the number as it removes digits, but you may need the original number to display an error message.

### Option 2: Decimal → Binary

Ask the user to enter a non-negative decimal number.

For example:

```text
13
```

Convert the decimal number to binary using arithmetic operations and a loop.

#### How to convert decimal to binary

To convert decimal `13` to binary, repeatedly divide the number by 2 and record each remainder.

**Step 1: Divide the decimal number by 2.**

| Calculation | Quotient | Remainder |
|---|---:|---:|
| 13 ÷ 2 | 6 | 1 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

In C++, integer division gives the quotient, and `% 2` gives the remainder.

**Step 2: Stop when the quotient becomes 0.**

The remainders are produced in this order:

```text
1, 0, 1, 1
```

**Step 3: Read the remainders in reverse order.**

```text
1101
```

Therefore, decimal `13` equals binary `1101`.

#### How to do this in C++

1. Use `% 2` to obtain the remainder.
2. Use `/= 2` to divide the number by 2.
3. Repeat until the number becomes 0.
4. Remember that the remainders must be displayed in reverse order.

**Hint:** If you are not using strings, arrays, or vectors, you can construct the binary result using a second place-value variable.

Start with `placeValue = 1`. Multiply each remainder by the current place value, add it to the result, and then multiply the place value by `10`.

For decimal `13`:

| Remainder | Place value | Contribution | Result so far |
|---:|---:|---:|---:|
| 1 | 1 | 1 | 1 |
| 0 | 10 | 0 | 1 |
| 1 | 100 | 100 | 101 |
| 1 | 1000 | 1000 | 1101 |

The final result is `1101`.

**Special case:** Decimal `0` converts to binary `0`. Handle this separately because a loop that runs while the number is greater than zero will not execute for zero.

### Option 3: Exit

When the user chooses `3`, display:

```text
Goodbye!
```

Then end the program.

## Example Run

```text
1. Convert binary to decimal
2. Convert decimal to binary
3. Exit

Enter your choice: 1

Enter a binary number: 1101
Decimal: 13

1. Convert binary to decimal
2. Convert decimal to binary
3. Exit

Enter your choice: 1

Enter a binary number: 1201
Error: 1201 is not a valid binary number.

1. Convert binary to decimal
2. Convert decimal to binary
3. Exit

Enter your choice: 2

Enter a decimal number: 13
Binary: 1101

1. Convert binary to decimal
2. Convert decimal to binary
3. Exit

Enter your choice: 3

Goodbye!
```

## Hints

### Useful arithmetic operators

| Operator | Purpose | Example |
|---|---|---|
| `%` | Obtain the remainder | `1101 % 10` gives `1` |
| `/` | Divide using integer division | `13 / 2` gives `6` |
| `/=` | Divide and store the result | `number /= 10` |
| `*=` | Multiply and store the result | `placeValue *= 2` |

### Additional requirements

- Use a loop to keep displaying the menu until the user chooses `3`.
- Use a loop to validate and convert the binary number.
- Use a loop to convert decimal to binary.
- Use `if`, `else if`, and `else` statements to handle menu choices and invalid input.
- Do not use strings, arrays, or vectors to perform either conversion.
- Assume the user enters non-negative whole numbers within the range your chosen integer type can represent, and that conversion results do not overflow.

### Before submitting

- [ ] Binary `1101` converts to decimal `13`.
- [ ] Binary `10101` converts to decimal `21`.
- [ ] Invalid binary input such as `1201` produces an error message.
- [ ] Decimal `13` converts to binary `1101`.
- [ ] Decimal `0` converts to binary `0`.
- [ ] The menu repeats until the user chooses `3`.
- [ ] Choosing `3` displays `Goodbye!` and ends the program.