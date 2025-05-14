# Functions in C

## Introduction to Functions

A function is a block of code that performs a specific task. Functions help in organizing code into modular, reusable components, which makes programs more maintainable, readable, and efficient.

### Why Use Functions?

1. **Code Reusability**: Write once, use many times
2. **Modularity**: Break complex problems into smaller, manageable parts
3. **Abstraction**: Hide implementation details
4. **Maintainability**: Easier to debug and modify
5. **Readability**: Cleaner code structure

### Function Types in C

1. **Standard Library Functions**: Pre-defined functions provided by C (e.g., `printf()`, `scanf()`, `strlen()`)
2. **User-defined Functions**: Functions created by the programmer

![Function Concept Diagram](https://placeholder-for-function-concept-diagram.png)

## Defining and Calling Functions

### Function Definition

The general syntax for defining a function in C is:

```c
return_type function_name(parameter_list) {
    // function body
    // statements
    return value;  // optional, based on return_type
}
```

Components:
- **return_type**: Data type of the value returned by the function
- **function_name**: Identifier used to call the function
- **parameter_list**: Input parameters (optional)
- **function body**: Code that executes when the function is called
- **return statement**: Value sent back to the caller (optional for `void` functions)

### Example Function Definition

```c
int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```

### Function Call

To use a function, you need to call it from somewhere in your code:

```c
#include <stdio.h>

// Function definition
int add(int a, int b) {
    int sum = a + b;
    return sum;
}

int main() {
    // Function call
    int result = add(5, 3);
    printf("The sum is: %d\n", result);
    
    // Another function call
    int anotherResult = add(10, 20);
    printf("The sum is: %d\n", anotherResult);
    
    return 0;
}
```

### Void Functions

Functions that don't return a value use the `void` return type:

```c
#include <stdio.h>

// Function that doesn't return a value
void greet(char name[]) {
    printf("Hello, %s!\n", name);
    // No return statement needed
}

int main() {
    greet("Alice");  // Output: Hello, Alice!
    greet("Bob");    // Output: Hello, Bob!
    return 0;
}
```

### Functions with No Parameters

Functions don't always need parameters:

```c
#include <stdio.h>
#include <time.h>

// Function with no parameters
void printCurrentTime() {
    time_t now = time(NULL);
    printf("Current time: %s", ctime(&now));
}

int main() {
    printCurrentTime();
    return 0;
}
```

## Function Prototypes

A function prototype is a declaration of a function that tells the compiler about the function's name, return type, and parameters without providing the function's body.

### Why Use Function Prototypes?

1. Allows calling functions before they are defined
2. Enables the compiler to perform type-checking
3. Helps detect errors at compile time rather than runtime

### Syntax of Function Prototype

```c
return_type function_name(parameter_types);
```

### Example with Function Prototype

```c
#include <stdio.h>

// Function prototype
int add(int, int);

int main() {
    int result = add(5, 3);  // Function is called before definition
    printf("The sum is: %d\n", result);
    return 0;
}

// Function definition
int add(int a, int b) {
    return a + b;
}
```

### Parameter Names in Prototypes

Parameter names in prototypes are optional but recommended for readability:

```c
// Both are valid prototypes
int calculate(int, float, char);
int calculate(int num, float factor, char operation);  // More readable
```

## Function Parameters and Arguments

### Parameters vs. Arguments

- **Parameters**: Variables in the function definition
- **Arguments**: Values passed to the function when it is called

```c
// a and b are parameters
int add(int a, int b) {
    return a + b;
}

int main() {
    // 5 and 3 are arguments
    int result = add(5, 3);
    return 0;
}
```

### Parameter Passing Mechanisms

#### Pass by Value

In C, all function parameters are passed by value by default. This means a copy of the argument is created and used inside the function.

```c
#include <stdio.h>

void modifyValue(int num) {
    num = num * 2;  // Modifies only the local copy
    printf("Inside function: %d\n", num);
}

int main() {
    int x = 10;
    printf("Before function call: %d\n", x);
    
    modifyValue(x);
    
    printf("After function call: %d\n", x);  // x remains unchanged
    return 0;
}
```

Output:
```
Before function call: 10
Inside function: 20
After function call: 10
```

#### Simulating Pass by Reference Using Pointers

To modify original variables, you can use pointers:

```c
#include <stdio.h>

void modifyValue(int *num) {
    *num = *num * 2;  // Modifies the original value
    printf("Inside function: %d\n", *num);
}

int main() {
    int x = 10;
    printf("Before function call: %d\n", x);
    
    modifyValue(&x);  // Pass the address of x
    
    printf("After function call: %d\n", x);  // x is modified
    return 0;
}
```

Output:
```
Before function call: 10
Inside function: 20
After function call: 20
```

### Array as Function Parameter

When passing an array to a function, you actually pass a pointer to the first element of the array:

```c
#include <stdio.h>

// Function that takes an array as parameter
void printArray(int arr[], int size) {
    printf("Array elements: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Function that modifies an array
void doubleArrayElements(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = arr[i] * 2;
    }
}

int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    
    printf("Original array:\n");
    printArray(numbers, 5);
    
    doubleArrayElements(numbers, 5);
    
    printf("Modified array:\n");
    printArray(numbers, 5);
    
    return 0;
}
```

Output:
```
Original array:
Array elements: 1 2 3 4 5
Modified array:
Array elements: 2 4 6 8 10
```

### Default Parameter Values

Unlike C++, C does not support default parameter values. You need to define multiple functions or use conditional logic within the function:

```c
#include <stdio.h>

// Approach 1: Multiple functions
void printMessage(char *message) {
    printf("%s\n", message);
}

void printMessageWithRepetition(char *message, int repeat) {
    for (int i = 0; i < repeat; i++) {
        printf("%s\n", message);
    }
}

// Approach 2: Function with conditional logic
void printMessageFlexible(char *message, int repeat) {
    if (repeat <= 0) repeat = 1;  // Default value
    
    for (int i = 0; i < repeat; i++) {
        printf("%s\n", message);
    }
}

int main() {
    printMessage("Hello");
    printf("----\n");
    printMessageWithRepetition("Hi", 3);
    printf("----\n");
    printMessageFlexible("Hey", 2);
    printf("----\n");
    printMessageFlexible("Default", -1);  // Will use default value
    
    return 0;
}
```

## Return Values from Functions

Functions can return at most one value in C. There are several approaches for handling different scenarios:

### Basic Return Value

```c
#include <stdio.h>

int square(int num) {
    return num * num;  // Returns a single value
}

int main() {
    int result = square(5);
    printf("5 squared is: %d\n", result);
    return 0;
}
```

### Returning Multiple Values Using Pointers

```c
#include <stdio.h>

void getStats(int arr[], int size, int *min, int *max, float *avg) {
    *min = arr[0];
    *max = arr[0];
    int sum = arr[0];
    
    for (int i = 1; i < size; i++) {
        if (arr[i] < *min) *min = arr[i];
        if (arr[i] > *max) *max = arr[i];
        sum += arr[i];
    }
    
    *avg = (float)sum / size;
}

int main() {
    int numbers[] = {5, 8, 2, 10, 7};
    int min, max;
    float avg;
    
    getStats(numbers, 5, &min, &max, &avg);
    
    printf("Minimum: %d\n", min);
    printf("Maximum: %d\n", max);
    printf("Average: %.2f\n", avg);
    
    return 0;
}
```

### Returning a Struct

```c
#include <stdio.h>

typedef struct {
    int min;
    int max;
    float avg;
} Stats;

Stats getStats(int arr[], int size) {
    Stats result;
    result.min = arr[0];
    result.max = arr[0];
    int sum = arr[0];
    
    for (int i = 1; i < size; i++) {
        if (arr[i] < result.min) result.min = arr[i];
        if (arr[i] > result.max) result.max = arr[i];
        sum += arr[i];
    }
    
    result.avg = (float)sum / size;
    return result;
}

int main() {
    int numbers[] = {5, 8, 2, 10, 7};
    Stats statistics = getStats(numbers, 5);
    
    printf("Minimum: %d\n", statistics.min);
    printf("Maximum: %d\n", statistics.max);
    printf("Average: %.2f\n", statistics.avg);
    
    return 0;
}
```

### Early Return

Functions can have multiple return statements:

```c
#include <stdio.h>

int findElement(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i;  // Early return when found
        }
    }
    return -1;  // Default return if not found
}

int main() {
    int numbers[] = {5, 8, 2, 10, 7};
    
    int index1 = findElement(numbers, 5, 8);
    int index2 = findElement(numbers, 5, 3);
    
    printf("Index of 8: %d\n", index1);
    printf("Index of 3: %d\n", index2);
    
    return 0;
}
```

## Scope and Lifetime of Variables

### Variable Scope

The scope of a variable determines where it can be accessed within a program:

#### Local Variables

Local variables are defined inside a function or block and can only be accessed within that function or block:

```c
#include <stdio.h>

void function1() {
    int localVar = 10;  // Local to function1
    printf("Inside function1, localVar = %d\n", localVar);
}

void function2() {
    // printf("localVar: %d\n", localVar);  // Error: localVar not in scope
    int localVar = 20;  // Different variable, also called localVar
    printf("Inside function2, localVar = %d\n", localVar);
}

int main() {
    function1();
    function2();
    // printf("localVar: %d\n", localVar);  // Error: localVar not in scope
    return 0;
}
```

#### Global Variables

Global variables are defined outside any function and can be accessed from any function:

```c
#include <stdio.h>

// Global variable
int globalVar = 100;

void function1() {
    printf("Inside function1, globalVar = %d\n", globalVar);
    globalVar = 200;  // Modifies the global variable
}

void function2() {
    printf("Inside function2, globalVar = %d\n", globalVar);
}

int main() {
    printf("Initially, globalVar = %d\n", globalVar);
    function1();
    function2();
    printf("Finally, globalVar = %d\n", globalVar);
    return 0;
}
```

#### Block Scope

Variables declared within a block (enclosed by curly braces) are only accessible within that block:

```c
#include <stdio.h>

int main() {
    // Outer block
    int x = 10;
    
    {
        // Inner block
        int y = 20;
        printf("Inside inner block: x = %d, y = %d\n", x, y);
    }
    
    printf("Outside inner block: x = %d\n", x);
    // printf("y = %d\n", y);  // Error: y is not in scope here
    
    return 0;
}
```

### Variable Lifetime

The lifetime of a variable determines how long it exists in memory:

#### Automatic Variables

Regular local variables have automatic lifetime; they are created when their block is entered and destroyed when the block is exited:

```c
#include <stdio.h>

void demoFunction() {
    int autoVar = 10;  // Created here
    printf("autoVar = %d\n", autoVar);
}  // autoVar is destroyed here

int main() {
    demoFunction();
    demoFunction();  // A new autoVar is created
    return 0;
}
```

#### Static Variables

Static local variables retain their values between function calls:

```c
#include <stdio.h>

void count() {
    static int counter = 0;  // Initialized only once
    counter++;
    printf("This function has been called %d time(s)\n", counter);
}

int main() {
    count();  // Output: 1
    count();  // Output: 2
    count();  // Output: 3
    return 0;
}
```

## Recursion

Recursion is a programming technique where a function calls itself to solve a problem. It consists of:

1. **Base Case**: The condition that terminates the recursion
2. **Recursive Case**: The condition where the function calls itself

### Simple Example: Factorial

```c
#include <stdio.h>

// Recursive function to calculate factorial
int factorial(int n) {
    // Base case
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive case
    else {
        return n * factorial(n - 1);
    }
}

int main() {
    int number = 5;
    printf("%d! = %d\n", number, factorial(number));
    return 0;
}
```

![Factorial Recursion Visualization](https://placeholder-for-factorial-recursion-diagram.png)

### Recursion vs Iteration

Let's compare recursive and iterative solutions for calculating factorial:

#### Recursive Solution

```c
int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}
```

#### Iterative Solution

```c
int factorial(int n) {
    int result = 1;
    for (int i = 1; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

### When to Use Recursion

Recursion is particularly useful for:

1. Problems that can be broken down into similar sub-problems
2. Tree or graph traversal
3. Divide-and-conquer algorithms
4. When the recursive solution is clearer than the iterative one

### Examples of Recursive Problems

#### Fibonacci Sequence

```c
#include <stdio.h>

int fibonacci(int n) {
    if (n <= 1) {
        return n;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}

int main() {
    printf("First 10 Fibonacci numbers:\n");
    for (int i = 0; i < 10; i++) {
        printf("%d ", fibonacci(i));
    }
    return 0;
}
```

#### Greatest Common Divisor (GCD)

```c
#include <stdio.h>

int gcd(int a, int b) {
    if (b == 0) {
        return a;
    } else {
        return gcd(b, a % b);
    }
}

int main() {
    int a = 48, b = 18;
    printf("GCD of %d and %d is %d\n", a, b, gcd(a, b));
    return 0;
}
```

#### Tower of Hanoi

```c
#include <stdio.h>

void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {
    if (n == 1) {
        printf("Move disk 1 from rod %c to rod %c\n", from_rod, to_rod);
        return;
    }
    
    towerOfHanoi(n-1, from_rod, aux_rod, to_rod);
    printf("Move disk %d from rod %c to rod %c\n", n, from_rod, to_rod);
    towerOfHanoi(n-1, aux_rod, to_rod, from_rod);
}

int main() {
    int n = 3;  // Number of disks
    towerOfHanoi(n, 'A', 'C', 'B');
    return 0;
}
```

### Risks of Recursion

1. **Stack Overflow**: Excessive recursive calls can exhaust the stack memory
2. **Performance Overhead**: Each function call has overhead
3. **Redundant Calculations**: Simple recursive implementations may recalculate the same values (e.g., in Fibonacci)

To address these issues, techniques like memoization (storing previously computed results) or tail recursion optimization can be used.

## Function Pointers

Function pointers allow functions to be passed as arguments to other functions, returned from functions, or stored in arrays.

### Declaring Function Pointers

```c
return_type (*pointer_name)(parameter_types);
```

### Example: Simple Function Pointer

```c
#include <stdio.h>

// Function to be pointed to
int add(int a, int b) {
    return a + b;
}

int main() {
    // Declare a function pointer
    int (*operation)(int, int);
    
    // Assign function address to pointer
    operation = add;
    
    // Call function through pointer
    int result = operation(5, 3);
    printf("Result: %d\n", result);
    
    return 0;
}
```

### Using Function Pointers for Callbacks

```c
#include <stdio.h>

// Different operation functions
int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }
int divide(int a, int b) { return b != 0 ? a / b : 0; }

// Function that takes an operation function as a parameter
int calculate(int a, int b, int (*operation)(int, int)) {
    return operation(a, b);
}

int main() {
    int a = 10, b = 5;
    
    printf("Addition: %d\n", calculate(a, b, add));
    printf("Subtraction: %d\n", calculate(a, b, subtract));
    printf("Multiplication: %d\n", calculate(a, b, multiply));
    printf("Division: %d\n", calculate(a, b, divide));
    
    return 0;
}
```

### Array of Function Pointers

```c
#include <stdio.h>

int add(int a, int b) { return a + b; }
int subtract(int a, int b) { return a - b; }
int multiply(int a, int b) { return a * b; }
int divide(int a, int b) { return b != 0 ? a / b : 0; }

int main() {
    // Array of function pointers
    int (*operations[4])(int, int) = {add, subtract, multiply, divide};
    char *opNames[4] = {"Addition", "Subtraction", "Multiplication", "Division"};
    
    int a = 10, b = 5;
    
    for (int i = 0; i < 4; i++) {
        printf("%s: %d\n", opNames[i], operations[i](a, b));
    }
    
    return 0;
}
```

## Inline Functions

C99 introduced the `inline` keyword, which suggests to the compiler that a function's code should be inserted at each call site, potentially improving performance by avoiding function call overhead.

```c
#include <stdio.h>

// Inline function definition
inline int max(int a, int b) {
    return (a > b) ? a : b;
}

int main() {
    int x = 10, y = 20;
    
    // The compiler may replace this call with the actual code
    int result = max(x, y);
    
    printf("Maximum: %d\n", result);
    return 0;
}
```

**Note**: The `inline` keyword is only a suggestion to the compiler, which may choose to ignore it. Also, inline functions should be simple and short.

## Best Practices for Functions

1. **Single Responsibility Principle**:
   Each function should do one thing and do it well.

2. **Meaningful Names**:
   Choose descriptive names that indicate what the function does.

3. **Keep Functions Short**:
   Aim for functions that can fit on one screen (20-30 lines).

4. **Limit the Number of Parameters**:
   Try to keep the parameter count low (ideally 4 or fewer).

5. **Use Function Prototypes**:
   Declare functions before using them to allow the compiler to perform type checking.

6. **Consistent Error Handling**:
   Use a consistent approach for error reporting (return codes, error messages, etc.).

7. **Document Your Functions**:
   Add comments explaining the purpose, parameters, return values, and any side effects.

8. **Avoid Side Effects**:
   Make it clear when a function modifies global state or parameters.

9. **Avoid Deep Nesting**:
   Refactor deeply nested code into separate functions.

10. **Test Your Functions**:
    Write tests to verify function behavior, especially edge cases.

## Common Pitfalls and How to Avoid Them

1. **Forgetting Return Statements**:
   Ensure all code paths in non-void functions return a value.

2. **Accessing Out-of-Scope Variables**:
   Be careful with local variable scope and lifetime.

3. **Stack Overflow in Recursion**:
   Always have a proper base case and avoid excessive recursion depth.

4. **Confusing Pass by Value and Pass by Reference**:
   Remember that C uses pass-by-value by default.

5. **Forgetting to Free Dynamic Memory**:
   Always free memory allocated within functions.

6. **Ignoring Function Return Values**:
   Check return values, especially for functions that can fail.

7. **Function Name Conflicts**:
   Avoid naming your functions the same as standard library functions.

## Practice Exercises

1. Write a function that finds the average of three integers.

2. Create a function that checks if a number is prime.

3. Implement a recursive function to calculate the power of a number (x^n).

4. Write a function that takes an array and its size, and returns the sum of its elements.

5. Create a function that uses function pointers to apply a specified mathematical operation on two numbers.

6. Write a recursive function that finds the nth number in the Fibonacci sequence using memoization for efficiency.

7. Implement a function that swaps the values of two variables using pointers.

8. Create a menu-driven calculator using function pointers for different operations.

## Key Takeaways

1. Functions are blocks of code that perform specific tasks and can be reused throughout a program.

2. Function prototypes declare functions before they're defined, enabling the compiler to perform type checking.

3. In C, parameters are passed by value by default; use pointers to simulate pass by reference.

4. Functions can return at most one value directly but can use pointers or structures to return multiple values.

5. Local variables exist only within their function or block, while global variables exist throughout the program.

6. Recursion is a powerful technique where a function calls itself to solve a problem.

7. Function pointers allow functions to be passed as arguments, creating flexible and modular code.

8. Following best practices for function design leads to more maintainable, readable, and efficient code.
