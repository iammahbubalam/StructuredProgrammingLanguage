# Variables and Data Types in C

## Introduction to Variables

A variable in C is a named storage location in the computer's memory that holds a value that can be modified during program execution. Think of it as a container that stores data which your program can manipulate.

### Key Characteristics of Variables
- Each variable has a specific **type** that determines what kind of data it can store
- Each variable has a **name** (identifier) used to refer to it
- Each variable uses a certain amount of **memory** based on its type
- Each variable has a **value** stored in that memory location

## Variable Declaration and Initialization

### Declaring Variables
In C, you must declare variables before using them. The basic syntax is:

```c
data_type variable_name;
```

Examples:
```c
int age;           // Declares an integer variable named 'age'
float temperature; // Declares a floating-point variable named 'temperature'
char grade;        // Declares a character variable named 'grade'
```

### Initializing Variables
You can assign an initial value to a variable at declaration time:

```c
data_type variable_name = initial_value;
```

Examples:
```c
int age = 25;           // Declares and initializes age to 25
float temperature = 98.6; // Declares and initializes temperature to 98.6
char grade = 'A';        // Declares and initializes grade to 'A'
```

### Multiple Declarations
You can declare multiple variables of the same type in one statement:

```c
int x, y, z;         // Declares three integer variables
int a = 5, b = 10;   // Declares and initializes two integers
```

## Rules for Naming Variables

1. **Valid Characters**: Letters (a-z, A-Z), digits (0-9), and underscore (_)
2. **First Character**: Must be a letter or underscore, not a digit
3. **Case Sensitivity**: `count` and `Count` are different variables
4. **Reserved Keywords**: Cannot use C keywords like `int`, `for`, `return`, etc.

**Good Variable Names:**
```c
int studentCount;
float average_score;
char first_initial;
```

**Bad Variable Names:**
```c
int 2ndValue;    // Cannot start with a digit
float my-score;  // Cannot contain hyphens
int for;         // Cannot use reserved keywords
```

## Primitive Data Types in C

### Overview of Primary Data Types

| Data Type | Size (typical) | Value Range | Format Specifier | Purpose |
|-----------|----------------|-------------|------------------|---------|
| `int` | 4 bytes | -2,147,483,648 to 2,147,483,647 | `%d` or `%i` | Whole numbers |
| `float` | 4 bytes | ~±3.4E-38 to ~±3.4E+38 (7 digits precision) | `%f` | Decimal numbers |
| `double` | 8 bytes | ~±1.7E-308 to ~±1.7E+308 (15 digits precision) | `%lf` | Higher precision decimals |
| `char` | 1 byte | -128 to 127 or 0 to 255 | `%c` | Single characters |

![C Data Types Hierarchy](https://placeholder-for-data-types-diagram.png)

### Integer Types

```c
// Basic integer
int count = 100;

// Type modifiers
short int small_number = 32767;     // 2 bytes typically
long int big_number = 2147483647L;  // 4 bytes (or 8 on some systems)
long long int huge_number = 9223372036854775807LL;  // 8 bytes

// Sign modifiers
unsigned int positive_only = 4294967295U;  // 0 to 4,294,967,295
signed int with_sign = -2147483648;       // -2,147,483,648 to 2,147,483,647
```

### Floating Point Types

```c
// Basic floating point types
float temperature = 98.6f;       // Single precision (~7 digits)
double precise_value = 3.14159265358979;  // Double precision (~15 digits)
long double extra_precise = 3.14159265358979323846L;  // Extended precision
```

### Character Type

```c
char grade = 'A';         // Character literal (note the single quotes)
char newline = '\n';      // Special character (escape sequence)
char null_char = '\0';    // Null character (important for strings)
```

### The `sizeof` Operator
The `sizeof` operator returns the memory size (in bytes) of a data type or variable:

```c
#include <stdio.h>

int main() {
    int x;
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of float: %zu bytes\n", sizeof(float));
    printf("Size of double: %zu bytes\n", sizeof(double));
    printf("Size of char: %zu bytes\n", sizeof(char));
    printf("Size of variable x: %zu bytes\n", sizeof(x));
    
    return 0;
}
```

## Format Specifiers and Printing Variables

Format specifiers are used with `printf()` and `scanf()` functions to specify the type of data being displayed or read.

### Common Format Specifiers

| Format Specifier | Description | Example |
|------------------|-------------|---------|
| `%d` or `%i` | Integer | `-123` |
| `%u` | Unsigned integer | `123` |
| `%f` | Float/Double | `123.456` |
| `%e` or `%E` | Scientific notation | `1.23e+2` |
| `%c` | Character | `'A'` |
| `%s` | String | `"Hello"` |
| `%x` or `%X` | Hexadecimal | `7B` or `7b` |
| `%o` | Octal | `173` |
| `%p` | Pointer address | `0x7ffee9d0a8d0` |
| `%%` | Percent sign | `%` |

### Printing Variables Example

```c
#include <stdio.h>

int main() {
    int age = 25;
    float height = 5.9;
    char grade = 'A';
    
    printf("Age: %d years\n", age);
    printf("Height: %.1f feet\n", height);  // .1 limits to 1 decimal place
    printf("Grade: %c\n", grade);
    
    // Multiple variables in one printf
    printf("I am %d years old, %.1f feet tall, and got an %c grade.\n", 
           age, height, grade);
    
    return 0;
}
```

### Format Specifier Modifiers

You can modify format specifiers for better control:

```c
int value = 123;
printf("%8d\n", value);    // Right-justified, width 8
printf("%-8d\n", value);   // Left-justified, width 8
printf("%08d\n", value);   // Pad with zeros to width 8

float pi = 3.14159;
printf("%.2f\n", pi);      // Two decimal places: 3.14
printf("%10.2f\n", pi);    // Width 10, two decimal places
```

## Type Conversion

### Implicit Conversion (Automatic)
C automatically converts one data type to another when assigning values:

```c
int x = 10;
double y = x;  // int converted to double (10.0)

double a = 9.7;
int b = a;     // double converted to int (9) - fractional part is truncated
```

### Explicit Conversion (Casting)
You can explicitly convert types using type casting:

```c
double price = 100.75;
int rounded_price = (int)price;  // Explicitly cast to int (100)

int numerator = 5;
int denominator = 2;
double result = (double)numerator / denominator;  // 2.5 instead of 2
```

## Constants

### Using `const` Keyword
```c
const float PI = 3.14159;
const int MAX_STUDENTS = 50;

// PI = 3.14;  // Error: cannot modify a constant
```

### Using `#define` Directive
```c
#define PI 3.14159
#define MAX_STUDENTS 50

// These are preprocessor directives, not variables
```

## Practice Exercises

1. Create variables for a student record (name, ID, GPA, grade) with appropriate data types
2. Write a program to calculate the area of a circle using PI as a constant
3. Write a program that converts temperature from Celsius to Fahrenheit
4. Create a program that correctly calculates the average of 5 integers

## Common Pitfalls and Best Practices

1. **Uninitialized Variables**: Always initialize variables before using them
2. **Data Type Overflow**: Be aware of the limits of each data type
3. **Implicit Conversions**: Be careful with automatic type conversions
4. **Meaningful Names**: Use descriptive variable names
5. **Consistent Style**: Follow a consistent naming convention
```

## Key Takeaways

- Variables allow us to store and manipulate data in our programs
- C requires all variables to be declared with a specific type
- Choose the appropriate data type based on the kind of data and range needed
- Format specifiers allow precise control over input and output
- Understanding type conversion helps prevent subtle bugs in calculations
