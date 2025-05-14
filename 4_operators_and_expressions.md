# Operators and Expressions in C

## Introduction to Operators

Operators are special symbols that perform specific operations on one, two, or more operands, and then return a result. In C, operators are the foundation of any program because they allow us to manipulate data and control program flow.

## Arithmetic Operators

Arithmetic operators perform mathematical operations on numerical values.

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `5 / 3` | `1` (integer division) |
| | | `5.0 / 3.0` | `1.666667` (floating-point division) |
| `%` | Modulus (Remainder) | `5 % 3` | `2` |

### Examples

```c
#include <stdio.h>

int main() {
    int a = 10, b = 3;
    float x = 10.0, y = 3.0;
    
    printf("Integer arithmetic:\n");
    printf("%d + %d = %d\n", a, b, a + b);
    printf("%d - %d = %d\n", a, b, a - b);
    printf("%d * %d = %d\n", a, b, a * b);
    printf("%d / %d = %d\n", a, b, a / b);  // Integer division truncates
    printf("%d %% %d = %d\n", a, b, a % b);  // % needs to be escaped as %%
    
    printf("\nFloating-point arithmetic:\n");
    printf("%.1f + %.1f = %.1f\n", x, y, x + y);
    printf("%.1f - %.1f = %.1f\n", x, y, x - y);
    printf("%.1f * %.1f = %.1f\n", x, y, x * y);
    printf("%.1f / %.1f = %.1f\n", x, y, x / y);  // Floating-point division
    // No modulus operator for floating-point numbers
    
    return 0;
}
```

### Important Notes
- Integer division (`/`) truncates the result
- Modulus (`%`) only works with integer operands
- Be aware of type conversions in mixed-type operations

![Arithmetic Operations Visualization](https://placeholder-for-arithmetic-diagram.png)

## Relational Operators

Relational operators compare two values and return either true (1) or false (0).

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `==` | Equal to | `5 == 5` | `1` (true) |
| | | `5 == 3` | `0` (false) |
| `!=` | Not equal to | `5 != 3` | `1` (true) |
| | | `5 != 5` | `0` (false) |
| `>` | Greater than | `5 > 3` | `1` (true) |
| | | `5 > 7` | `0` (false) |
| `<` | Less than | `3 < 5` | `1` (true) |
| | | `7 < 5` | `0` (false) |
| `>=` | Greater than or equal to | `5 >= 5` | `1` (true) |
| | | `5 >= 7` | `0` (false) |
| `<=` | Less than or equal to | `5 <= 5` | `1` (true) |
| | | `7 <= 5` | `0` (false) |

### Example

```c
#include <stdio.h>

int main() {
    int a = 5, b = 10, c = 5;
    
    printf("%d == %d is %d\n", a, b, a == b);  // 0 (false)
    printf("%d == %d is %d\n", a, c, a == c);  // 1 (true)
    printf("%d != %d is %d\n", a, b, a != b);  // 1 (true)
    printf("%d > %d is %d\n", a, b, a > b);    // 0 (false)
    printf("%d < %d is %d\n", a, b, a < b);    // 1 (true)
    printf("%d >= %d is %d\n", a, c, a >= c);  // 1 (true)
    printf("%d <= %d is %d\n", a, c, a <= c);  // 1 (true)
    
    return 0;
}
```

### Common Mistake
One of the most common mistakes in C programming is confusing the assignment operator (`=`) with the equality operator (`==`):

```c
// This ASSIGNS the value 5 to x
if (x = 5) {  // Always true because x becomes 5, which is non-zero
    printf("This will always execute!\n");
}

// This CHECKS if x equals 5
if (x == 5) {  // Only true if x is actually 5
    printf("This executes only if x is 5\n");
}
```

## Logical Operators

Logical operators work with boolean values (true/false) and are used to combine multiple conditions.

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&&` | Logical AND | `(5 > 3) && (10 > 5)` | `1` (true) |
| | | `(5 > 3) && (10 < 5)` | `0` (false) |
| `||` | Logical OR | `(5 > 3) || (10 < 5)` | `1` (true) |
| | | `(5 < 3) || (10 < 5)` | `0` (false) |
| `!` | Logical NOT | `!(5 > 3)` | `0` (false) |
| | | `!(5 < 3)` | `1` (true) |

### Truth Tables

#### Logical AND (`&&`)
| A | B | A && B |
|---|---|--------|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

#### Logical OR (`||`)
| A | B | A \|\| B |
|---|---|----------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

#### Logical NOT (`!`)
| A | !A |
|---|-----|
| 0 | 1 |
| 1 | 0 |

### Example

```c
#include <stdio.h>

int main() {
    int age = 25;
    int salary = 50000;
    
    // Checking multiple conditions
    if (age >= 18 && salary >= 30000) {
        printf("Eligible for loan\n");
    }
    
    int has_credit_card = 0;  // 0 means false
    int has_cash = 1;         // 1 means true
    
    // Either condition can be true
    if (has_credit_card || has_cash) {
        printf("Can make a purchase\n");
    }
    
    // Negating a condition
    if (!has_credit_card) {
        printf("Does not have a credit card\n");
    }
    
    // Complex condition
    if ((age > 20 && salary > 40000) || has_credit_card) {
        printf("Preferred customer\n");
    }
    
    return 0;
}
```

### Short-Circuit Evaluation
C uses short-circuit evaluation for logical operators:
- For `&&`: If the first operand is false, the second operand is not evaluated
- For `||`: If the first operand is true, the second operand is not evaluated

```c
// Example of short-circuit evaluation
int x = 5;
int y = 0;

// This won't cause division by zero because the first condition is false
if (y != 0 && x/y > 2) {
    printf("x/y is greater than 2\n");
}
```

## Assignment Operators

Assignment operators store values in variables.

| Operator | Description | Example | Equivalent to |
|----------|-------------|---------|---------------|
| `=` | Simple assignment | `x = 5` | `x = 5` |
| `+=` | Add and assign | `x += 3` | `x = x + 3` |
| `-=` | Subtract and assign | `x -= 3` | `x = x - 3` |
| `*=` | Multiply and assign | `x *= 3` | `x = x * 3` |
| `/=` | Divide and assign | `x /= 3` | `x = x / 3` |
| `%=` | Modulus and assign | `x %= 3` | `x = x % 3` |
| `<<=` | Left shift and assign | `x <<= 2` | `x = x << 2` |
| `>>=` | Right shift and assign | `x >>= 2` | `x = x >> 2` |
| `&=` | Bitwise AND and assign | `x &= 3` | `x = x & 3` |
| `|=` | Bitwise OR and assign | `x |= 3` | `x = x | 3` |
| `^=` | Bitwise XOR and assign | `x ^= 3` | `x = x ^ 3` |

### Example

```c
#include <stdio.h>

int main() {
    int a = 10;
    
    printf("Initial value: a = %d\n", a);
    
    a += 5;  // a = a + 5
    printf("After a += 5: a = %d\n", a);
    
    a -= 3;  // a = a - 3
    printf("After a -= 3: a = %d\n", a);
    
    a *= 2;  // a = a * 2
    printf("After a *= 2: a = %d\n", a);
    
    a /= 4;  // a = a / 4
    printf("After a /= 4: a = %d\n", a);
    
    a %= 3;  // a = a % 3
    printf("After a %= 3: a = %d\n", a);
    
    return 0;
}
```

## Increment and Decrement Operators

These unary operators increase or decrease a variable's value by 1.

| Operator | Description | Example |
|----------|-------------|---------|
| `++` | Increment | `++x` (pre-increment) |
| | | `x++` (post-increment) |
| `--` | Decrement | `--x` (pre-decrement) |
| | | `x--` (post-decrement) |

### Pre vs. Post Increment/Decrement

- **Pre-increment/decrement**: The operation is performed first, and then the value is used
- **Post-increment/decrement**: The value is used first, and then the operation is performed

```c
#include <stdio.h>

int main() {
    int a = 5, b = 5;
    int result1, result2;
    
    // Post-increment
    result1 = a++;  // result1 = 5, then a becomes 6
    
    // Pre-increment
    result2 = ++b;  // b becomes 6, then result2 = 6
    
    printf("a = %d, result1 = %d\n", a, result1);  // a = 6, result1 = 5
    printf("b = %d, result2 = %d\n", b, result2);  // b = 6, result2 = 6
    
    return 0;
}
```

![Increment Operations Visualization](https://placeholder-for-increment-diagram.png)

## Bitwise Operators

Bitwise operators perform operations on individual bits of integer values.

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&` | Bitwise AND | `5 & 3` | `1` |
| `|` | Bitwise OR | `5 | 3` | `7` |
| `^` | Bitwise XOR | `5 ^ 3` | `6` |
| `~` | Bitwise NOT | `~5` | `-6` (depends on int size) |
| `<<` | Left shift | `5 << 1` | `10` |
| `>>` | Right shift | `5 >> 1` | `2` |

### Example With Bit Manipulation

```c
#include <stdio.h>

int main() {
    unsigned int a = 5;  // 0101 in binary
    unsigned int b = 3;  // 0011 in binary
    
    printf("a = %u (binary: 0101)\n", a);
    printf("b = %u (binary: 0011)\n", b);
    
    // Bitwise AND: 0101 & 0011 = 0001
    printf("a & b = %u\n", a & b);
    
    // Bitwise OR: 0101 | 0011 = 0111
    printf("a | b = %u\n", a | b);
    
    // Bitwise XOR: 0101 ^ 0011 = 0110
    printf("a ^ b = %u\n", a ^ b);
    
    // Bitwise NOT (complement): ~0101 = 1010 (but with leading 1s)
    printf("~a = %u\n", ~a);
    
    // Left shift: 0101 << 1 = 1010
    printf("a << 1 = %u\n", a << 1);
    
    // Right shift: 0101 >> 1 = 0010
    printf("a >> 1 = %u\n", a >> 1);
    
    return 0;
}
```

### Bitwise Operation Visualizations

#### Bitwise AND (`&`)
```
    0101  (5)
  & 0011  (3)
  ------
    0001  (1)
```

#### Bitwise OR (`|`)
```
    0101  (5)
  | 0011  (3)
  ------
    0111  (7)
```

#### Bitwise XOR (`^`)
```
    0101  (5)
  ^ 0011  (3)
  ------
    0110  (6)
```

#### Left Shift (`<<`)
```
    0101  (5)
    <<1
  ------
    1010  (10)
```

#### Right Shift (`>>`)
```
    0101  (5)
    >>1
  ------
    0010  (2)
```

### Practical Applications of Bitwise Operators

1. **Setting a bit**: `x |= (1 << n)`
2. **Clearing a bit**: `x &= ~(1 << n)`
3. **Toggling a bit**: `x ^= (1 << n)`
4. **Checking if a bit is set**: `(x & (1 << n)) != 0`
5. **Power of 2 multiplication/division**: `x << 1` (multiply by 2), `x >> 1` (divide by 2)
6. **Creating bit masks for flags and permissions**

```c
#include <stdio.h>

int main() {
    unsigned char flags = 0;  // 00000000
    
    // Set bit 1 (second bit from right)
    flags |= (1 << 1);        // 00000010
    printf("After setting bit 1: %d\n", flags);
    
    // Set bit 3
    flags |= (1 << 3);        // 00001010
    printf("After setting bit 3: %d\n", flags);
    
    // Check if bit 3 is set
    if (flags & (1 << 3)) {
        printf("Bit 3 is set!\n");
    }
    
    // Clear bit 1
    flags &= ~(1 << 1);       // 00001000
    printf("After clearing bit 1: %d\n", flags);
    
    // Toggle bit 3
    flags ^= (1 << 3);        // 00000000
    printf("After toggling bit 3: %d\n", flags);
    
    return 0;
}
```

## Operator Precedence and Associativity

Operator precedence determines the order in which operators are evaluated in an expression. Operators with higher precedence are evaluated first.

### Precedence Table (from highest to lowest)

| Precedence | Operator | Description | Associativity |
|------------|----------|-------------|---------------|
| 1 | `()` `[]` `->` `.` | Parentheses, array subscript, structure member | Left to right |
| 2 | `++` `--` `!` `~` `+` `-` `*` `&` `sizeof` `(type)` | Unary operators, sizeof, type cast | Right to left |
| 3 | `*` `/` `%` | Multiplication, division, modulus | Left to right |
| 4 | `+` `-` | Addition, subtraction | Left to right |
| 5 | `<<` `>>` | Bitwise shift | Left to right |
| 6 | `<` `<=` `>` `>=` | Relational operators | Left to right |
| 7 | `==` `!=` | Equality operators | Left to right |
| 8 | `&` | Bitwise AND | Left to right |
| 9 | `^` | Bitwise XOR | Left to right |
| 10 | `\|` | Bitwise OR | Left to right |
| 11 | `&&` | Logical AND | Left to right |
| 12 | `\|\|` | Logical OR | Left to right |
| 13 | `? :` | Conditional operator | Right to left |
| 14 | `=` `+=` `-=` etc. | Assignment operators | Right to left |
| 15 | `,` | Comma operator | Left to right |

### Associativity
When operators have the same precedence, associativity determines the order of evaluation:
- **Left to right**: Most binary operators
- **Right to left**: Most unary operators and assignment operators

### Example

```c
#include <stdio.h>

int main() {
    int result;
    
    // Precedence example
    result = 5 + 3 * 2;       // Multiplication before addition
    printf("5 + 3 * 2 = %d\n", result);  // 11, not 16
    
    result = (5 + 3) * 2;     // Parentheses change precedence
    printf("(5 + 3) * 2 = %d\n", result);  // 16
    
    // Associativity example (left to right)
    result = 10 - 5 - 2;      // Evaluated as (10 - 5) - 2
    printf("10 - 5 - 2 = %d\n", result);  // 3, not 7
    
    // Associativity example (right to left)
    int a, b, c;
    a = b = c = 5;            // Evaluated as a = (b = (c = 5))
    printf("a = %d, b = %d, c = %d\n", a, b, c);  // All are 5
    
    return 0;
}
```

### Precedence Diagram
![Operator Precedence Chart](https://placeholder-for-precedence-diagram.png)

## The Conditional (Ternary) Operator

The conditional operator (`? :`) is the only ternary operator in C. It provides a shorthand way to write if-else statements.

Syntax:
```
condition ? expression_if_true : expression_if_false
```

### Example

```c
#include <stdio.h>

int main() {
    int age = 20;
    
    // Using if-else
    if (age >= 18) {
        printf("Adult\n");
    } else {
        printf("Minor\n");
    }
    
    // Using ternary operator
    printf("%s\n", age >= 18 ? "Adult" : "Minor");
    
    // Assigning a value based on a condition
    int ticket_price = age < 12 ? 5 : (age < 65 ? 10 : 7);
    printf("Ticket price: $%d\n", ticket_price);
    
    return 0;
}
```

## The sizeof Operator

The `sizeof` operator returns the size of a variable or data type in bytes.

```c
#include <stdio.h>

int main() {
    int x;
    int arr[10];
    
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of variable x: %zu bytes\n", sizeof(x));
    printf("Size of array arr: %zu bytes\n", sizeof(arr));
    printf("Number of elements in arr: %zu\n", sizeof(arr) / sizeof(arr[0]));
    
    return 0;
}
```

## Expressions in C

An expression is a combination of variables, constants, and operators that evaluates to a value. Expressions can be used wherever a value is expected.

### Types of Expressions

1. **Arithmetic Expressions**: Evaluate to a numeric value
   ```c
   int result = 5 + 3 * 2;
   ```

2. **Relational Expressions**: Evaluate to 0 (false) or 1 (true)
   ```c
   int is_valid = x > 0 && x < 100;
   ```

3. **Logical Expressions**: Evaluate to 0 (false) or 1 (true)
   ```c
   int result = (age > 18) && (score > 70);
   ```

4. **Assignment Expressions**: Assign and return a value
   ```c
   int x, y;
   x = (y = 10);  // y becomes 10, then x becomes 10
   ```

5. **Bitwise Expressions**: Perform bit manipulation
   ```c
   unsigned int flags = (1 << 3) | (1 << 5);
   ```

### Expression Statements
An expression followed by a semicolon becomes a statement:

```c
a = b + c;  // Assignment expression used as a statement
x++;        // Increment expression used as a statement
func();     // Function call expression used as a statement
```

## Practice Exercises

1. Write a program that uses all arithmetic operators on two numbers
2. Implement a simple calculator that performs basic operations based on user input
3. Write a program that uses bitwise operators to set and clear specific bits
4. Create a program that uses the ternary operator to determine the maximum of three numbers

## Common Pitfalls and Best Practices

1. **Operator Precedence**: Use parentheses to make complex expressions clear
2. **Assignment vs. Equality**: Don't confuse `=` with `==`
3. **Integer Division**: Be aware that integer division truncates the result
4. **Overflow**: Be careful with operations that might cause overflow
5. **Short-circuit Evaluation**: Rely on it to prevent errors like division by zero
6. **Side Effects**: Be careful with expressions that have side effects (like `++` or `--`)

## Key Takeaways

- Operators enable us to perform calculations and logic in our programs
- Understanding operator precedence is crucial for writing correct expressions
- Bitwise operators are powerful tools for low-level programming
- C provides a rich set of compound assignment operators for convenience
- Expressions form the building blocks of C statements and program logic
