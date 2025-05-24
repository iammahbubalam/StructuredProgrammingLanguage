# Control Structures in C

## Introduction to Control Structures

Control structures are the programming constructs that allow us to control the flow of program execution. Instead of executing statements sequentially, control structures let us make decisions, repeat actions, and jump to different parts of code based on certain conditions.

In C programming, there are three main categories of control structures:

1. **Decision-making statements** (if, if-else, switch-case)
2. **Loops** (for, while, do-while)
3. **Jump statements** (break, continue, goto)

![Control Structures Overview](https://placeholder-for-control-structures-diagram.png)

## Decision-Making Statements

### if Statement

The `if` statement is used to execute a block of code only if a specified condition is true.

**Syntax:**
```c
if (condition) {
    // code to execute if condition is true
}
```

**Flowchart:**
![if Statement Flowchart](https://placeholder-for-if-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int age = 20;
    
    if (age >= 18) {
        printf("You are eligible to vote.\n");
    }
    
    return 0;
}
```

In this example, the message will be printed because age (20) is greater than or equal to 18.

### if-else Statement

The `if-else` statement executes one block of code if a condition is true and another block if the condition is false.

**Syntax:**
```c
if (condition) {
    // code to execute if condition is true
} else {
    // code to execute if condition is false
}
```

**Flowchart:**
![if-else Statement Flowchart](https://placeholder-for-if-else-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int number = 15;
    
    if (number % 2 == 0) {
        printf("%d is even.\n", number);
    } else {
        printf("%d is odd.\n", number);
    }
    
    return 0;
}
```

This program checks whether a number is even or odd and prints the appropriate message.

### Nested if-else Statement

You can place `if` statements inside other `if` or `else` blocks to create nested decision structures.

**Syntax:**
```c
if (condition1) {
    // code to execute if condition1 is true
    if (condition2) {
        // code to execute if both condition1 and condition2 are true
    }
} else {
    // code to execute if condition1 is false
}
```

**Example:**
```c
#include <stdio.h>

int main() {
    int score = 85;
    
    if (score >= 60) {
        printf("You passed the exam.\n");
        
        if (score >= 90) {
            printf("Excellent performance!\n");
        } else if (score >= 80) {
            printf("Good performance!\n");
        } else {
            printf("Average performance.\n");
        }
    } else {
        printf("You failed the exam.\n");
        
        if (score >= 50) {
            printf("You were close. Try again!\n");
        } else {
            printf("You need significant improvement.\n");
        }
    }
    
    return 0;
}
```

This program evaluates a student's exam performance using nested if-else statements.

### if-else if Ladder

When you need to check multiple conditions, you can use the if-else if ladder.

**Syntax:**
```c
if (condition1) {
    // code to execute if condition1 is true
} else if (condition2) {
    // code to execute if condition1 is false and condition2 is true
} else if (condition3) {
    // code to execute if condition1 and condition2 are false and condition3 is true
} else {
    // code to execute if all conditions are false
}
```

**Flowchart:**
![if-else if Ladder Flowchart](https://placeholder-for-if-else-if-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int score = 75;
    
    if (score >= 90) {
        printf("Grade: A\n");
    } else if (score >= 80) {
        printf("Grade: B\n");
    } else if (score >= 70) {
        printf("Grade: C\n");
    } else if (score >= 60) {
        printf("Grade: D\n");
    } else {
        printf("Grade: F\n");
    }
    
    return 0;
}
```

This program determines a student's grade based on their score.

### switch-case Statement

The `switch` statement is a multi-way decision statement that tests whether an expression matches one of several constant integer values and branches accordingly.

**Syntax:**
```c
switch (expression) {
    case constant1:
        // code to execute if expression == constant1
        break;
    case constant2:
        // code to execute if expression == constant2
        break;
    // more cases...
    default:
        // code to execute if expression doesn't match any case
}
```

**Flowchart:**
![switch Statement Flowchart](https://placeholder-for-switch-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int day = 3;
    
    switch (day) {
        case 1:
            printf("Monday\n");
            break;
        case 2:
            printf("Tuesday\n");
            break;
        case 3:
            printf("Wednesday\n");
            break;
        case 4:
            printf("Thursday\n");
            break;
        case 5:
            printf("Friday\n");
            break;
        case 6:
            printf("Saturday\n");
            break;
        case 7:
            printf("Sunday\n");
            break;
        default:
            printf("Invalid day\n");
    }
    
    return 0;
}
```

This program prints the name of the day based on a number from 1 to 7.

**Key Points About switch-case:**

1. The expression in `switch` must evaluate to an integer type (int, char, enum).
2. The `break` statement is used to exit the switch block. Without it, execution "falls through" to the next case.
3. The `default` case is executed when no case matches the expression (it's optional).
4. Multiple cases can execute the same code:

```c
switch (grade) {
    case 'A':
    case 'a':
        printf("Excellent!\n");
        break;
    case 'B':
    case 'b':
        printf("Good job!\n");
        break;
    // ... and so on
}
```

## Loops

Loops are used to execute a block of code repeatedly as long as a condition is true.

### for Loop

The `for` loop executes a block of code a specified number of times.

**Syntax:**
```c
for (initialization; condition; update) {
    // code to be executed repeatedly
}
```

**Flowchart:**
![for Loop Flowchart](https://placeholder-for-for-loop-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int i;
    
    // Print numbers from 1 to 5
    for (i = 1; i <= 5; i++) {
        printf("%d ", i);
    }
    printf("\n");
    
    return 0;
}
```

This program prints the numbers 1 to 5.

**Components of a for Loop:**

1. **Initialization**: Executed once before the loop starts (e.g., `i = 1`).
2. **Condition**: Evaluated before each iteration; loop continues if true (e.g., `i <= 5`).
3. **Update**: Executed after each iteration (e.g., `i++`).

**Variations of for Loop:**

1. **Multiple initializations and updates:**
```c
for (i = 0, j = 10; i < j; i++, j--) {
    printf("i = %d, j = %d\n", i, j);
}
```

2. **Omitting parts:**
```c
// Infinite loop
for (;;) {
    // This will run forever unless broken
    if (condition) break;
}
```

3. **Loop without body:**
```c
// Calculate sum of numbers 1 to 10
int sum = 0;
for (i = 1; i <= 10; sum += i, i++);
printf("Sum = %d\n", sum);
```

### while Loop

The `while` loop executes a block of code as long as a condition is true.

**Syntax:**
```c
while (condition) {
    // code to be executed repeatedly
}
```

**Flowchart:**
![while Loop Flowchart](https://placeholder-for-while-loop-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int i = 1;
    
    // Print numbers from 1 to 5
    while (i <= 5) {
        printf("%d ", i);
        i++;
    }
    printf("\n");
    
    return 0;
}
```

This program also prints the numbers 1 to 5 but using a `while` loop.

**Key Points About while Loop:**

1. The condition is evaluated before each iteration.
2. If the condition is initially false, the loop body won't execute at all.
3. It's suitable when the number of iterations isn't known in advance.

**Common Uses:**
```c
// Reading input until a sentinel value
int num;
printf("Enter numbers (enter -1 to stop):\n");

while (1) {
    scanf("%d", &num);
    if (num == -1) break;
    printf("You entered: %d\n", num);
}
```

### do-while Loop

The `do-while` loop is similar to the `while` loop, but it evaluates the condition after executing the loop body, ensuring the body executes at least once.

**Syntax:**
```c
do {
    // code to be executed repeatedly
} while (condition);
```

**Flowchart:**
![do-while Loop Flowchart](https://placeholder-for-do-while-flowchart.png)

**Example:**
```c
#include <stdio.h>

int main() {
    int i = 1;
    
    // Print numbers from 1 to 5
    do {
        printf("%d ", i);
        i++;
    } while (i <= 5);
    printf("\n");
    
    return 0;
}
```

This program also prints the numbers 1 to 5 using a `do-while` loop.

**Key Points About do-while Loop:**

1. The loop body always executes at least once, regardless of the condition.
2. The condition is evaluated after each iteration.
3. It's useful when you need to process input at least once.

**Common Uses:**
```c
// Menu-driven program
int choice;

do {
    printf("\nMenu:\n");
    printf("1. Add\n");
    printf("2. Subtract\n");
    printf("3. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);
    
    switch (choice) {
        case 1:
            printf("You selected Add\n");
            break;
        case 2:
            printf("You selected Subtract\n");
            break;
        case 3:
            printf("Exiting...\n");
            break;
        default:
            printf("Invalid choice, try again\n");
    }
} while (choice != 3);
```

## Break and Continue Statements

### break Statement

The `break` statement terminates the innermost enclosing loop or switch statement.

**Example in a Loop:**
```c
#include <stdio.h>

int main() {
    int i;
    
    // Print numbers from 1 to 10, but stop at 5
    for (i = 1; i <= 10; i++) {
        if (i > 5) {
            break;  // Exit the loop when i > 5
        }
        printf("%d ", i);
    }
    printf("\n");
    
    return 0;
}
```

Output: `1 2 3 4 5`

**Example in a Switch:**
```c
switch (choice) {
    case 1:
        printf("Option 1 selected\n");
        break;  // Exit the switch
    case 2:
        printf("Option 2 selected\n");
        break;  // Exit the switch
    // ...
}
```

### continue Statement

The `continue` statement skips the rest of the current loop iteration and proceeds to the next iteration.

**Example:**
```c
#include <stdio.h>

int main() {
    int i;
    
    // Print odd numbers from 1 to 10
    for (i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue;  // Skip even numbers
        }
        printf("%d ", i);
    }
    printf("\n");
    
    return 0;
}
```

Output: `1 3 5 7 9`

**Differences Between break and continue:**

- `break` terminates the entire loop
- `continue` skips the current iteration but continues the loop

![Break vs Continue](https://placeholder-for-break-continue-diagram.png)

## Nested Loops

A nested loop is a loop within a loop. The inner loop executes completely for each iteration of the outer loop.

**Example: Multiplication Table**
```c
#include <stdio.h>

int main() {
    int i, j;
    
    // Print multiplication table (1-5)
    for (i = 1; i <= 5; i++) {
        for (j = 1; j <= 5; j++) {
            printf("%d*%d=%-3d ", i, j, i*j);
        }
        printf("\n");
    }
    
    return 0;
}
```

Output:
```
1*1=1   1*2=2   1*3=3   1*4=4   1*5=5   
2*1=2   2*2=4   2*3=6   2*4=8   2*5=10  
3*1=3   3*2=6   3*3=9   3*4=12  3*5=15  
4*1=4   4*2=8   4*3=12  4*4=16  4*5=20  
5*1=5   5*2=10  5*3=15  5*4=20  5*5=25  
```

**Example: Pattern Printing**
```c
#include <stdio.h>

int main() {
    int i, j;
    
    // Print a right-angled triangle pattern
    for (i = 1; i <= 5; i++) {
        for (j = 1; j <= i; j++) {
            printf("* ");
        }
        printf("\n");
    }
    
    return 0;
}
```

Output:
```
* 
* * 
* * * 
* * * * 
* * * * * 
```

**Key Points About Nested Loops:**

1. For each iteration of the outer loop, the inner loop completes all its iterations.
2. The total number of iterations is the product of the iterations of each loop.
3. You can have more than two levels of nested loops, but be careful about performance.

## The goto Statement

The `goto` statement allows an unconditional jump to a labeled statement within the same function.

**Syntax:**
```c
goto label;
// ...
label: statement;
```

**Example:**
```c
#include <stdio.h>

int main() {
    int i = 0;
    
start:
    printf("%d ", i);
    i++;
    
    if (i < 5) {
        goto start;
    }
    printf("\n");
    
    return 0;
}
```

Output: `0 1 2 3 4`

**Important Notes About goto:**

1. `goto` is generally discouraged in modern programming due to its potential to create spaghetti code.
2. It makes programs harder to understand, debug, and maintain.
3. Almost every use of `goto` can be replaced with structured control statements (if, while, for).
4. Some legitimate uses of `goto` in C include breaking out of nested loops or error handling with cleanup.

**Breaking Out of Nested Loops:**
```c
#include <stdio.h>

int main() {
    int i, j;
    
    for (i = 0; i < 5; i++) {
        for (j = 0; j < 5; j++) {
            if (i == 2 && j == 3) {
                goto out;  // Break out of both loops
            }
            printf("(%d,%d) ", i, j);
        }
        printf("\n");
    }
    
out:
    printf("\nBroke out at i=2, j=3\n");
    
    return 0;
}
```

## Choosing the Right Control Structure

1. **if-else vs. switch:**
   - Use `if-else` for ranges or non-integer values
   - Use `switch` for multiple options with discrete, integer values

2. **for vs. while vs. do-while:**
   - Use `for` when the number of iterations is known
   - Use `while` when the loop depends on a condition that might never be true
   - Use `do-while` when the body must execute at least once

3. **Nested Loops:**
   - Use for processing multi-dimensional data (matrices, tables)
   - Be careful with performance when nesting many loops

4. **break and continue:**
   - Use `break` to exit a loop early
   - Use `continue` to skip specific iterations

## Practice Exercises

1. Write a program that determines if a year is a leap year.
2. Create a calculator program that performs basic arithmetic operations using a switch statement.
3. Print the Fibonacci sequence up to n terms using a loop.
4. Use nested loops to create patterns like these:
   ```
   1
   1 2
   1 2 3
   1 2 3 4
   1 2 3 4 5
   ```
5. Write a program that finds the prime numbers between 1 and 100.

## Common Pitfalls and Best Practices

1. **Infinite Loops**: Always ensure that loop conditions eventually become false.
   ```c
   // Infinite loop example
   while (1) {
       // Must have a break condition inside
       if (condition) break;
   }
   ```

2. **Off-by-One Errors**: Be careful with loop boundaries.
   ```c
   // Correct way to loop through array of size n
   for (i = 0; i < n; i++) {  // Not i <= n
       // Process array[i]
   }
   ```

3. **Confusing = and ==**: Using the assignment operator instead of equality operator in conditions.
   ```c
   // Wrong (assigns 5 to x)
   if (x = 5) { ... }
   
   // Correct (checks if x equals 5)
   if (x == 5) { ... }
   ```

4. **Missing Break in Switch**: Without break, execution falls through to the next case.
   ```c
   switch (x) {
       case 1:
           printf("One\n");
           // Missing break - execution falls through to case 2
       case 2:
           printf("Two\n");
           break;
   }
   ```

5. **Complex Nested Structures**: Avoid deeply nested control structures that make code hard to read.

## Key Takeaways

1. Control structures modify the flow of program execution from the default sequential flow.
2. Decision-making statements allow the program to choose different paths based on conditions.
3. Loops allow repeated execution of code blocks.
4. The `break` statement terminates a loop or switch, while `continue` skips the current iteration.
5. Nested loops are powerful but should be used carefully.
6. The `goto` statement should be avoided in favor of structured programming constructs.

## Real-World Applications

1. **Form Validation**: Using if-else to validate user input
2. **Menu-Driven Programs**: Using switch-case for options
3. **Data Processing**: Using loops to process arrays or collections
4. **Pattern Recognition**: Using nested loops to analyze patterns in data
5. **Game Development**: Using control structures to manage game states and logic
