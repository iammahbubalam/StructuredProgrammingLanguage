# C Programming Questions and Solutions

## Question 1: Trace Code Execution

### Part (a): Determine the output of the program a.c.

```c
#include <stdio.h>
int main()
{
    int a = 5 != 6? -1.2 : 0.3;
    int b = 1 + a--;
    if(!b--)
        printf("Inside First IF\n");
    printf("a = %d and b = %d\n", a, b);
    if(a * b > 0 && b - a > 0)
        printf("Inside Second IF\n");
    else if(a + b < 0)
        printf("Inside ELSE IF\n");
    else
        printf("Inside ELSE\n");
    return 0;
}
```

### Solution:

```c
// Tracing execution step by step:
// 1. a = 5 != 6 ? -1.2 : 0.3
//    Since 5 != 6 is true, a = -1.2, but since a is an int, a = -1
// 2. b = 1 + a-- = 1 + (-1) = 0, and a becomes -2 after the post-decrement
// 3. !b-- evaluates !0 which is 1 (true), and b becomes -1 after the post-decrement
// 4. "Inside First IF" is printed
// 5. "a = -2 and b = -1" is printed
// 6. a * b > 0 && b - a > 0
//    a * b = (-2) * (-1) = 2 > 0 (true)
//    b - a = (-1) - (-2) = 1 > 0 (true)
//    So the condition is true
// 7. "Inside Second IF" is printed

// Output:
// Inside First IF
// a = -2 and b = -1
// Inside Second IF
```

### Part (b): Rewrite the code segment b.c using if-else block without changing the logical meaning.

```c
switch(a * b)
{
case 0:
    a = b + 2;
    b = a--;
case 1:
    printf("a = %d and b = %d\n", a, b);
    break;
case 2:
    a = b + 2;
    b = a--;
case 3:
case 4:
    break;
    printf("a = %d and b = %d\n", a, b);
default:
    printf("Inside default\n");
}
```

### Solution:

```c
// Equivalent if-else block:
int product = a * b;

if (product == 0) {
    a = b + 2;
    b = a--;
    printf("a = %d and b = %d\n", a, b);
}
else if (product == 1) {
    printf("a = %d and b = %d\n", a, b);
}
else if (product == 2) {
    a = b + 2;
    b = a--;
    // Fall through to case 3 and 4, which only have a break
    // Note: The printf after the break is unreachable
}
else if (product == 3 || product == 4) {
    // Just a break, nothing happens
    // The printf after break is unreachable
}
else {
    printf("Inside default\n");
}
```

## Question 2: Determine the output of the program

```c
#include <stdio.h>
int main()
{
    int a = 8, b = 0, c = 0;
    do
    {
        if(a % 2 == 0) b++;
        else c++;
        printf("%d %d %d\n", a, b, c);
        if(a == 8) a = 3;
        else if(a == 3) a = 6;
        else if(a == 6) a = 9;
        else if(a == 9) a = 0;
    } while(a != 0);
    return 0;
}
```

### Solution:

```c
// Tracing execution step by step:
// Initial values: a = 8, b = 0, c = 0

// Iteration 1:
// a % 2 == 0 is true, so b++ (b becomes 1)
// print: 8 1 0
// a == 8 is true, so a = 3

// Iteration 2:
// a % 2 == 0 is false, so c++ (c becomes 1)
// print: 3 1 1
// a == 3 is true, so a = 6

// Iteration 3:
// a % 2 == 0 is true, so b++ (b becomes 2)
// print: 6 2 1
// a == 6 is true, so a = 9

// Iteration 4:
// a % 2 == 0 is false, so c++ (c becomes 2)
// print: 9 2 2
// a == 9 is true, so a = 0

// a == 0, so loop ends

// Output:
// 8 1 0
// 3 1 1
// 6 2 1
// 9 2 2
```

## Question 3: Determine the output of the program

```c
#include <stdio.h>
int main()
{
    int n = 9;
    int i = 1;
    int j;
    for(j = i * 7; i < n / 2 && i != j; j = j - 1 + i)
    {
        j = j - 2 + i;
        printf("i=%d, j=%d\n", i, j);
        do{
            j += 3, n--;
        } while(j % 2 != 0);
        if(i == 1) continue;
        i++;
    }
    return 0;
}
```

### Solution:

```c
// Tracing execution step by step:
// Initial values: n = 9, i = 1, j is uninitialized

// for loop initialization: j = i * 7 = 1 * 7 = 7
// i < n / 2: 1 < 9/2 = 1 < 4 (true)
// i != j: 1 != 7 (true)
// Loop body executes

// Iteration 1:
// j = j - 2 + i = 7 - 2 + 1 = 6
// print: i=1, j=6
// do-while: j += 3 = 9, n-- = 8
// j % 2 != 0: 9 % 2 != 0 (true), continue
// j += 3 = 12, n-- = 7
// j % 2 != 0: 12 % 2 != 0 (false), exit do-while
// i == 1 is true, so continue (skip i++)
// for loop update: j = j - 1 + i = 12 - 1 + 1 = 12
// i < n / 2: 1 < 7/2 = 1 < 3 (true)
// i != j: 1 != 12 (true)
// Loop body executes

// Iteration 2:
// j = j - 2 + i = 12 - 2 + 1 = 11
// print: i=1, j=11
// do-while: j += 3 = 14, n-- = 6
// j % 2 != 0: 14 % 2 != 0 (false), exit do-while
// i == 1 is true, so continue (skip i++)
// for loop update: j = j - 1 + i = 14 - 1 + 1 = 14
// i < n / 2: 1 < 6/2 = 1 < 3 (true)
// i != j: 1 != 14 (true)
// Loop body executes

// Iteration 3:
// j = j - 2 + i = 14 - 2 + 1 = 13
// print: i=1, j=13
// do-while: j += 3 = 16, n-- = 5
// j % 2 != 0: 16 % 2 != 0 (false), exit do-while
// i == 1 is true, so continue (skip i++)
// for loop update: j = j - 1 + i = 16 - 1 + 1 = 16
// i < n / 2: 1 < 5/2 = 1 < 2 (true)
// i != j: 1 != 16 (true)
// Loop body executes

// Iteration 4:
// j = j - 2 + i = 16 - 2 + 1 = 15
// print: i=1, j=15
// do-while: j += 3 = 18, n-- = 4
// j % 2 != 0: 18 % 2 != 0 (false), exit do-while
// i == 1 is true, so continue (skip i++)
// for loop update: j = j - 1 + i = 18 - 1 + 1 = 18
// i < n / 2: 1 < 4/2 = 1 < 2 (true)
// i != j: 1 != 18 (true)
// Loop body executes

// Iteration 5:
// j = j - 2 + i = 18 - 2 + 1 = 17
// print: i=1, j=17
// do-while: j += 3 = 20, n-- = 3
// j % 2 != 0: 20 % 2 != 0 (false), exit do-while
// i == 1 is true, so continue (skip i++)
// for loop update: j = j - 1 + i = 20 - 1 + 1 = 20
// i < n / 2: 1 < 3/2 = 1 < 1 (false)
// Loop ends

// Output:
// i=1, j=6
// i=1, j=11
// i=1, j=13
// i=1, j=15
// i=1, j=17
```

## Question 4: Flowchart for Rocket Launch Countdown System

```
// Flowchart for Rocket Launch Countdown System

 ┌─────────────┐
 │   START     │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │  Set timer  │
 │    to 10    │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │  Display    │
 │ countdown   │◄───┐
 │   number    │    │
 └──────┬──────┘    │
        │           │
 ┌──────▼──────┐    │
 │  Decrease   │    │
 │  timer by 1 │    │
 └──────┬──────┘    │
        │           │
 ┌──────▼──────┐    │
 │   Is timer  │    │
 │  equal to 0?│    │
 └──────┬──────┘    │
        │           │
 ┌──────▼──────┐    │
 │    NO       │    │
 └──────┬──────┘    │
        │           │
        └───────────┘
        │
 ┌──────▼──────┐
 │    YES      │
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │   Display   │
 │"Blasting Off!"│
 └──────┬──────┘
        │
 ┌──────▼──────┐
 │    END      │
 └─────────────┘
```

## Question 5: Triangular Pattern Program

Write a program that takes an odd integer n as input and displays a triangular pattern as demonstrated in the following table:

```
| Sample Input | Sample Output |
| ------------ | ------------- |
               |
3              |       0
               |      101
               |     21012
               |
5              |       0
               |      101
               |     21012
               |    3210123
               |   432101234
```

### Solution:

```c
#include <stdio.h>

int main() {
    int n, i, j, k;

    printf("Enter an odd integer: ");
    scanf("%d", &n);

    if (n % 2 == 0) {
        printf("Please enter an odd integer.\n");
        return 1;
    }

    // For each row
    for (i = 0; i < n; i++) {
        // Print leading spaces
        for (j = 0; j < n - 1 - i; j++) {
            printf(" ");
        }

        // Print decreasing sequence (i to 0)
        for (j = i; j >= 0; j--) {
            printf("%d", j);
        }

        // Print increasing sequence (1 to i) except for the first row
        if (i > 0) {
            for (j = 1; j <= i; j++) {
                printf("%d", j);
            }
        }

        printf("\n");
    }

    return 0;
}
```

## Question 6: Array Trace

### Part (a): Manually trace the following code segment for the array m[4]

```c
#include <stdio.h>
int main()
{
    int i, j, m[4];
    for(i = 0, j = 1; i < 4; i = i + 1, j = j + 2)
    {
        m[i] = i * i + j;
        printf("i = %d, j = %d, ", i, j);
        printf("m[%d] = %d\n", i, m[i]);
    }
    return 0;
}
```

### Solution:

```
// Tracing the execution of the array code:

// Initialization: i = 0, j = 1, m[] is uninitialized

// Iteration 1:
// i = 0, j = 1
// m[0] = 0*0 + 1 = 1
// Output: i = 0, j = 1, m[0] = 1
// i = i+1 = 1, j = j+2 = 3

// Iteration 2:
// i = 1, j = 3
// m[1] = 1*1 + 3 = 4
// Output: i = 1, j = 3, m[1] = 4
// i = i+1 = 2, j = j+2 = 5

// Iteration 3:
// i = 2, j = 5
// m[2] = 2*2 + 5 = 9
// Output: i = 2, j = 5, m[2] = 9
// i = i+1 = 3, j = j+2 = 7

// Iteration 4:
// i = 3, j = 7
// m[3] = 3*3 + 7 = 16
// Output: i = 3, j = 7, m[3] = 16
// i = i+1 = 4, j = j+2 = 9

// i = 4 is not < 4, so loop ends

// Final values:
// i = 4, j = 9
// m[0] = 1, m[1] = 4, m[2] = 9, m[3] = 16
```

## Question 7: Even/Odd Counter and Average Calculator

Write a C program that reads 20 integers into an array, determines how many numbers are even, how many are odd, and calculates the average of all 20 numbers.

### Solution:

```c
#include <stdio.h>

int main() {
    int numbers[20];
    int i, evenCount = 0, oddCount = 0;
    float sum = 0, average;

    // Input 20 integers
    printf("Enter 20 integers:\n");
    for (i = 0; i < 20; i++) {
        printf("Enter number %d: ", i + 1);
        scanf("%d", &numbers[i]);

        // Check if even or odd
        if (numbers[i] % 2 == 0) {
            evenCount++;
        } else {
            oddCount++;
        }

        // Add to sum for average calculation
        sum += numbers[i];
    }

    // Calculate average
    average = sum / 20;

    // Display results
    printf("\nResults:\n");
    printf("Number of even integers: %d\n", evenCount);
    printf("Number of odd integers: %d\n", oddCount);
    printf("Average of all numbers: %.2f\n", average);

    return 0;
}
```

## Question 8: Variable Validity, Value Computation, and Program Output

### Part (a): Determine which of the following variable names are invalid and explain why:

(i) first_name (ii) @home (iii) int\* (iv) 1st_name

### Solution:

```c
// (i) first_name - Valid: Contains only letters and underscore, doesn't start with a digit
// (ii) @home - Invalid: Contains special character '@', variable names can only contain letters, digits, and underscores
// (iii) int_ - Valid: Contains only letters and underscore, doesn't start with a digit
// (iv) 1st_name - Invalid: Starts with a digit, variable names must start with a letter or underscore
```

### Part (b): Compute the values of the variables a, b, c, and d. ASCII codes: 'A' = 65, 'a' = 97, '0' = 48.

(i) int a = 'B' - '7';
(ii) float b = (float)(2 % 5);
(iii) int n = 5, c = n-- + 3;
(iv) int d = (5 == 5) ? 1 : 0;

### Solution:

```c
// (i) int a = 'B' - '7';
// 'B' has ASCII value 66 (since 'A' is 65)
// '7' has ASCII value 55 (since '0' is 48)
// a = 66 - 55 = 11

// (ii) float b = (float)(2 % 5);
// 2 % 5 = 2 (remainder when 2 is divided by 5)
// b = 2.0 (converted to float)

// (iii) int n = 5, c = n-- + 3;
// c = 5 + 3 = 8 (n is used before decrementing)
// After this statement, n = 4 (due to post-decrement)

// (iv) int d = (5 == 5) ? 1 : 0;
// 5 == 5 is true
// d = 1
```

### Part (c): Determine the output of the following program for x = 6, y = 5:

```c
#include<stdio.h>
void main() {
    int x, y;
    scanf("%d%d", &x, &y);
    if ((x == y) || (x + y > 10)) {
        printf("Alpha\n");
        if (x % 2 == 0 && y % 2 == 0)
            printf("Both Even\n");
        else
            printf("Not Both Even\n");
    } else if (x > y) {
        printf("Beta\n");
        if (x - y > 5)
            printf("Difference > 5\n");
    } else {
        printf("Gamma\n");
        if (y % x == 0)
            printf("Divisible\n");
        else
            printf("Not Divisible\n");
    }
    if (x!=0 && y!=0)
        printf("End\n");
}
```

### Solution:

```
// For x = 6, y = 5:
// Check if (x == y) || (x + y > 10):
// (6 == 5) is false
// (6 + 5 > 10) is true (11 > 10)
// So the condition is true
// Print "Alpha"
// Check if x % 2 == 0 && y % 2 == 0:
// 6 % 2 == 0 is true
// 5 % 2 == 0 is false
// So the condition is false
// Print "Not Both Even"
// Check if (x!=0 && y!=0):
// Both are non-zero, so condition is true
// Print "End"

// Output:
// Alpha
// Not Both Even
// End
```

### Part (d): Implement the code segment using if-else statement without changing the logical meaning.

```c
switch(x-y){
    case 1: int d = x-y;
    printf("%d", d);
    case 2: break;
    case 5: d = i++;
    case 7:
    default:
    printf("%d", d);
}
```

### Solution:

```c
// Equivalent if-else block:
int diff = x - y;
if (diff == 1) {
    int d = diff;
    printf("%d", d);
    // Fall through to case 2
    if (diff == 2) {
        // Just break, nothing happens
    } else if (diff == 5) {
        d = i++;
        // Fall through to case 7 and default
        printf("%d", d);
    } else if (diff == 7) {
        // Fall through to default
        printf("%d", d);
    } else {
        // Default case
        printf("%d", d);
    }
} else if (diff == 2) {
    // Just break, nothing happens
} else if (diff == 5) {
    d = i++;
    // Fall through to case 7 and default
    printf("%d", d);
} else if (diff == 7) {
    // Fall through to default
    printf("%d", d);
} else {
    // Default case
    printf("%d", d);
}
```

## Question 9: Code Tracing

### Part (a): Manually trace the following code segment. Show the changes of all the variables.

```c
int start = 13, end = 16;
for (int current = start; current <= end; current++) {
    if (current % 2 == 1) {
        printf("%d %d\n", start++, end + 5);
    } else {
        start += 3;
        --end;
    }
}
```

### Solution:

```
// Initialization: start = 13, end = 16, current = 13

// Iteration 1:
// current = 13
// current % 2 == 1 is true (13 is odd)
// print: 13 21 (start = 13, end + 5 = 16 + 5 = 21)
// start++ makes start = 14
// current++ makes current = 14

// Iteration 2:
// current = 14
// current % 2 == 1 is false (14 is even)
// start += 3 makes start = 17
// --end makes end = 15
// current++ makes current = 15

// Iteration 3:
// current = 15
// current % 2 == 1 is true (15 is odd)
// print: 17 20 (start = 17, end + 5 = 15 + 5 = 20)
// start++ makes start = 18
// current++ makes current = 16

// Iteration 4:
// current = 16
// current % 2 == 1 is false (16 is even)
// start += 3 makes start = 21
// --end makes end = 14
// current++ makes current = 17

// current = 17 > end = 14, so loop ends

// Final values: start = 21, end = 14

// Output:
// 13 21
// 17 20
```

## Question 10: Loop Conversions and Flowcharts

### Part (a): Rewrite the code segment replacing for loops with while loops.

```c
for(int i=1,j=1;i<8;j+=2,i++){
    int n =i+j;
    for(n=n+2;n<12;){
        n++;
        printf("i=%d,j=%d and n=%d\n",i,j,n);
    }
}
```

### Solution:

```c
int i = 1, j = 1;
while (i < 8) {
    int n = i + j;
    n = n + 2;  // Initialize inner loop variable

    while (n < 12) {
        n++;
        printf("i=%d,j=%d and n=%d\n", i, j, n);
    }

    j += 2;
    i++;
}
```

### Part (b): Draw a flowchart based on the given code segment.

```c
int x,y,low,high;
scanf("%d%d",&x,&y);
if(x<y){
    low=x;
    high=y;
}else{
    low=y;
    high=x;
}
printf("Low=%d and high=%d\n",low,high);
int count = 0;
while(low<=high){
    low+=2;
    high-=2;
    printf("Iteration no:%d\n",count++);
}
```

### Solution:

```
// Flowchart for the given code segment

┌─────────────┐
│   START     │
└──────┬──────┘
       │
┌──────▼──────┐
│  Read x, y  │
└──────┬──────┘
       │
┌──────▼──────┐
│  Is x < y?  │
└──────┬──────┘
       │
       ├────────────┐
       │yes         │no
┌──────▼──────┐    ┌▼────────────┐
│  low = x    │    │  low = y     │
│  high = y   │    │  high = x    │
└──────┬──────┘    └─────┬────────┘
       │                 │
       └────────┬────────┘
                │
┌───────────────▼─────────────────┐
│  Print "Low=low and high=high"  │
└───────────────┬─────────────────┘
                │
┌───────────────▼─────────────────┐
│            count = 0            │
└───────────────┬─────────────────┘
                │
┌───────────────▼─────────────────┐
│        Is low <= high?          │◄──────┐
└───────────────┬─────────────────┘       │
                │                         │
       ┌────────┴─────────┐               │
       │                  │               │
┌──────▼──────┐     ┌─────▼─────┐         │
│     YES     │     │    NO     │         │
└──────┬──────┘     └─────┬─────┘         │
       │                  │               │
┌──────▼──────┐     ┌─────▼─────┐         │
│  low += 2   │     │   END     │         │
└──────┬──────┘     └───────────┘         │
       │                                  │
┌──────▼──────────────────────┐           │
│ Print "Iteration no:count"  │           │
└──────┬──────────────────────┘           │
       │                                  │
┌──────▼──────┐                           │
│  count++    │                           │
└──────┬──────┘                           │
       │                                  │
       └──────────────────────────────────┘
```

### Part (c): Write a C program to print the pattern of an hourglass.

Take n as user input where n is odd.

```
n=5   * * * * *
        *   *
          *
        *   *
      * * * * *

n=7 * * * * * * *
      *       *
        *   *
          *
        *   *
      *       *
    * * * * * * *
```

### Solution:

```c
#include <stdio.h>

int main() {
    int n, i, j;

    printf("Enter an odd number: ");
    scanf("%d", &n);

    if (n % 2 == 0) {
        printf("Please enter an odd number.\n");
        return 1;
    }

    // Print the top row
    for (i = 0; i < n; i++) {
        printf("* ");
    }
    printf("\n");

    // Print the upper half of the hourglass
    for (i = 1; i < n/2; i++) {
        // Print leading spaces
        for (j = 0; j < i; j++) {
            printf("  ");
        }

        // Print first star
        printf("* ");

        // Print middle spaces
        for (j = 0; j < n - 2 - 2*i; j++) {
            printf("  ");
        }

        // Print last star
        printf("* \n");
    }

    // Print the middle point
    for (i = 0; i < n/2; i++) {
        printf("  ");
    }
    printf("* \n");

    // Print the lower half of the hourglass
    for (i = n/2 - 1; i > 0; i--) {
        // Print leading spaces
        for (j = 0; j < i; j++) {
            printf("  ");
        }

        // Print first star
        printf("* ");

        // Print middle spaces
        for (j = 0; j < n - 2 - 2*i; j++) {
            printf("  ");
        }

        // Print last star
        printf("* \n");
    }

    // Print the bottom row
    for (i = 0; i < n; i++) {
        printf("* ");
    }
    printf("\n");

    return 0;
}
```

## Question 11: Array Manipulations

### Part (a): Manually trace the following code segment for the array m[3]. Show the changes of all the variables.

```c
int i, j, m[3];
for (i=0, j = 5; i<3 ; i=i+1, j=j+2){
    m[i] = i*i + j;
    printf("\n i = %d, j = %d", i, j);
    printf("  m[%d] = %d ", i, m[i]);
}
```

### Solution:

```
// Initialization: i = 0, j = 5, m[] is uninitialized

// Iteration 1:
// i = 0, j = 5
// m[0] = 0*0 + 5 = 5
// Output: i = 0, j = 5  m[0] = 5
// i = i+1 = 1, j = j+2 = 7

// Iteration 2:
// i = 1, j = 7
// m[1] = 1*1 + 7 = 8
// Output: i = 1, j = 7  m[1] = 8
// i = i+1 = 2, j = j+2 = 9

// Iteration 3:
// i = 2, j = 9
// m[2] = 2*2 + 9 = 13
// Output: i = 2, j = 9  m[2] = 13
// i = i+1 = 3, j = j+2 = 11

// i = 3 is not < 3, so loop ends

// Final values:
// i = 3, j = 11
// m[0] = 5, m[1] = 8, m[2] = 13
```

### Part (b): Write a program to find out the 2nd largest number in an array of 10 integers.

### Solution:

```c
#include <stdio.h>

int main() {
    int arr[10];
    int i, largest, secondLargest;

    // Input 10 integers
    printf("Enter 10 integers:\n");
    for (i = 0; i < 10; i++) {
        printf("Enter number %d: ", i + 1);
        scanf("%d", &arr[i]);
    }

    // Initialize largest and second largest
    if (arr[0] > arr[1]) {
        largest = arr[0];
        secondLargest = arr[1];
    } else {
        largest = arr[1];
        secondLargest = arr[0];
    }

    // Find largest and second largest
    for (i = 2; i < 10; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        } else if (arr[i] > secondLargest && arr[i] != largest) {
            secondLargest = arr[i];
        }
    }

    printf("The second largest number is: %d\n", secondLargest);

    return 0;
}
```

### Part (c): Manually trace the following code segment for the 2D array m[2][3]. Show the changes of all the variables.

```c
int i, j, m[2][3];
for (i=0; i<2 ; i++){
    printf("\n");
    for (j=0; j<3; j++){
        m[i][j] = (i + 2*j)*10;
        printf(" (%d,%d):", i, j);
        printf("%d ", m[i][j]);
    }
}
```

### Solution:

```
// Initialization: i = 0, j = 0, m[][] is uninitialized

// Outer loop iteration 1 (i = 0):
// Print newline
// Inner loop iteration 1 (j = 0):
// m[0][0] = (0 + 2*0)*10 = 0
// Output: (0,0):0
// Inner loop iteration 2 (j = 1):
// m[0][1] = (0 + 2*1)*10 = 20
// Output: (0,1):20
// Inner loop iteration 3 (j = 2):
// m[0][2] = (0 + 2*2)*10 = 40
// Output: (0,2):40

// Outer loop iteration 2 (i = 1):
// Print newline
// Inner loop iteration 1 (j = 0):
// m[1][0] = (1 + 2*0)*10 = 10
// Output: (1,0):10
// Inner loop iteration 2 (j = 1):
// m[1][1] = (1 + 2*1)*10 = 30
// Output: (1,1):30
// Inner loop iteration 3 (j = 2):
// m[1][2] = (1 + 2*2)*10 = 50
// Output: (1,2):50

// Final values:
// m[0][0] = 0, m[0][1] = 20, m[0][2] = 40
// m[1][0] = 10, m[1][1] = 30, m[1][2] = 50

// Output:
//
// (0,0):0 (0,1):20 (0,2):40
// (1,0):10 (1,1):30 (1,2):50
```

## Question 12: Identify and Correct Errors, Find Output

### Part (a): Identify and correct errors in the following code segment:

```c
include <stdio>
Int main {
int Num, a;
   Num = 20%3;
a = Num+10
   printf("%d %f ", Num, a,);
return 0;
}
```

### Solution:

```c
// Errors identified and corrected:
// 1. Missing "#" before include
// 2. Incorrect capital "I" in "Int"
// 3. Missing parentheses after main
// 4. Missing semicolon after a = Num+10
// 5. Using %f for an integer variable a
// 6. Extra comma in printf arguments

#include <stdio.h>
int main() {
    int Num, a;
    Num = 20%3;
    a = Num+10;
    printf("%d %d ", Num, a);
    return 0;
}

// Output: 2 12
```

### Part (b): Find output of the following code segment:

```c
int a=3, b=4, c=-5, result;
int mod;
result = a * b % c + b;
printf("result = %d\n",result);
if (result >= 0 && result < 10) {
     printf("a =  %d\n", a);
}
else if (result >= 5) {
     printf("b =  %d\n", b);
}
else printf("a = %d\n", a);
```

### Solution:

```c
// Calculate the value of result:
// result = a * b % c + b
// result = 3 * 4 % (-5) + 4
// result = 12 % (-5) + 4
// result = 2 + 4 (modulo with negative divisor -5 gives 2)
// result = 6

// Check conditions:
// if (result >= 0 && result < 10) is true because 6 >= 0 and 6 < 10
// So we print: "a = 3"

// Output:
// result = 6
// a = 3
```

## Question 13: Code Conversion and Tracing

### Part (a): Rewrite the code segment using "if ... else" without changing the logical meaning:

```c
int num=5, sum=10, i=4, j=9;
switch(num) {
   case 1: sum *= 3;
   case 2:
   case 3: sum += --j * 2;
           i--; break;
   case 4: sum = ++i * j--;
           break;
   case 5: break;
      i += 10;
   default: sum *= i++ / j--;
           i=i % j; break;
}
```

### Solution:

```c
int num=5, sum=10, i=4, j=9;

if (num == 1) {
    sum *= 3;
    // Fall through to case 2 and 3
    sum += --j * 2;
    i--;
}
else if (num == 2 || num == 3) {
    sum += --j * 2;
    i--;
}
else if (num == 4) {
    sum = ++i * j--;
}
else if (num == 5) {
    // Note: The i += 10 statement is unreachable due to the break
    // before it in the original code
}
else {
    sum *= i++ / j--;
    i = i % j;
}

// For num = 5:
// The switch will hit case 5, then break,
// but the "i += 10" line is unreachable due to the break
// After this block, sum = 10, i = 4, j = 9
```

### Part (b): Manually trace the following code segment and show all the changes of the variables i, p, and x in each step:

```c
#include <stdio.h>
int main() {
  int p=1;
  int x = 490;
  for(int i=1;i<=p;){
    printf("%d %d %d\n",i,p,x);
    if(x % 29 == 0){
       printf("Not a great number!");
       break;
    }
    else {
       x -= 13;
       p += x % 10;
       i += 3;
    }
  }
  return 0;
}
```

### Solution:

```
// Initialization: p = 1, x = 490, i = 1

// for loop condition: i <= p is true (1 <= 1)
// Loop body executes:
// Output: "1 1 490"
// x % 29 = 490 % 29 = 26, which is not 0
// else block executes:
// x -= 13 = 490 - 13 = 477
// p += x % 10 = 1 + (477 % 10) = 1 + 7 = 8
// i += 3 = 1 + 3 = 4

// for loop condition check: i <= p is false (4 <= 8)
// Loop ends

// Final values: i = 4, p = 8, x = 477

// Output:
// 1 1 490
```

### Part (c): Draw a flow chart for the given code segment in Q.2(b)

```
// Flowchart for the code segment in Q.2(b)

┌─────────────┐
│   START     │
└──────┬──────┘
       │
┌──────▼──────┐
│  p = 1      │
│  x = 490    │
└──────┬──────┘
       │
┌──────▼──────┐
│  i = 1      │
└──────┬──────┘
       │
┌──────▼──────┐
│  i <= p?    │
└──────┬──────┘
       │
       ├────────────┐
       │yes         │no
┌──────▼──────┐    ┌▼────────────┐
│ Print i,p,x │    │   END       │
└──────┬──────┘    └─────────────┘
       │
┌──────▼──────┐
│ x % 29 == 0?│
└──────┬──────┘
       │
       ├────────────┐
       │yes         │no
┌──────▼──────┐    ┌▼────────────┐
│ Print "Not a│    │  x -= 13    │
│great number!│    └─────┬───────┘
└──────┬──────┘          │
       │               ┌─▼────────────┐
       │               │ p += x % 10  │
       │               └─────┬────────┘
       │                     │
       │               ┌─────▼────────┐
       │               │   i += 3     │
       │               └─────┬────────┘
       │                     │
┌──────▼──────┐              │
│   break     │◄─────────────┘
└──────┬──────┘
       │
       └──────────────────┐
                          │
                        ┌─▼─┐
                        │END│
                        └───┘
```

## Question 14: Pattern Printing and Loop Conversion

### Part (a): Write a C program to print the following pattern of digit '2'. Take n as user input where n is odd and n>=5.

```
Sample input n=5
Sample output
* * * * *
        *
* * * * *
*
* * * * *
```

### Solution:

```c
#include <stdio.h>

int main() {
    int n, i, j;

    printf("Enter an odd number (n>=5): ");
    scanf("%d", &n);

    if (n % 2 == 0 || n < 5) {
        printf("Please enter an odd number that is at least 5.\n");
        return 1;
    }

    // Print top horizontal line
    for (i = 0; i < n; i++) {
        printf("* ");
    }
    printf("\n");

    // Print top-right vertical line (n/2 - 1 rows)
    for (i = 0; i < n/2 - 1; i++) {
        for (j = 0; j < n-1; j++) {
            printf("  ");
        }
        printf("*\n");
    }

    // Print middle horizontal line
    for (i = 0; i < n; i++) {
        printf("* ");
    }
    printf("\n");

    // Print bottom-left vertical line (n/2 - 1 rows)
    for (i = 0; i < n/2 - 1; i++) {
        printf("*\n");
    }

    // Print bottom horizontal line
    for (i = 0; i < n; i++) {
        printf("* ");
    }
    printf("\n");

    return 0;
}
```

### Part (b): Replace the "outer" while loop with "for" and the "nested" for loop with "while" loop in the following code without changing the logical meaning of the program:

```c
int i=0, count = 0;
int n = 12345;
while (n != 0) {
   printf ("%d", n % 10);
   count++;
   for(; i<count; i++) {
        printf("%d", n/= 10);
   }
   printf ("\n");
}
```

### Solution:

```c
int i=0, count = 0;
int n = 12345;

// Replace outer while with for
for (; n != 0; ) {
   printf ("%d", n % 10);
   count++;

   // Replace inner for with while
   i = i; // Preserve the existing value of i
   while (i < count) {
        printf("%d", n/= 10);
        i++;
   }
   printf ("\n");
}
```

## Question 15: Array Manipulation

### Part (a): Manually trace the given code segment. Show the changes of all the variables i, hi, hlw and array arr elements in each step:

```c
int hi = 0, hlw = 10;
int arr[4] = {10, 20, 30, 40};
for(int i=4; i<=hlw; i++) {
    arr[hi] = arr[hi+1] - 5;
    hlw -= 2;
}
```

### Solution:

```
// Initialization: hi = 0, hlw = 10, arr = {10, 20, 30, 40}

// Iteration 1:
// i = 4
// i <= hlw is true (4 <= 10)
// arr[hi] = arr[hi+1] - 5 = arr[1] - 5 = 20 - 5 = 15
// arr = {15, 20, 30, 40}
// hlw -= 2 = 10 - 2 = 8
// i++ = 5

// Iteration 2:
// i = 5
// i <= hlw is true (5 <= 8)
// arr[hi] = arr[hi+1] - 5 = arr[1] - 5 = 20 - 5 = 15
// arr = {15, 20, 30, 40} (no change)
// hlw -= 2 = 8 - 2 = 6
// i++ = 6

// Iteration 3:
// i = 6
// i <= hlw is true (6 <= 6)
// arr[hi] = arr[hi+1] - 5 = arr[1] - 5 = 20 - 5 = 15
// arr = {15, 20, 30, 40} (no change)
// hlw -= 2 = 6 - 2 = 4
// i++ = 7

// Iteration 4:
// i = 7
// i <= hlw is false (7 <= 4)
// Loop ends

// Final values: i = 7, hi = 0, hlw = 4, arr = {15, 20, 30, 40}
```

### Part (b): Take an array as input of size N. Then take another number as input in K. Your task is to add this number to the even indexed elements, and subtract from the odd indexed elements:

```c
#include <stdio.h>

int main() {
    int N, K, i;

    // Input size of array
    printf("Enter the size of the array (N): ");
    scanf("%d", &N);

    int arr[N];

    // Input array elements
    printf("Enter the array elements:\n");
    for (i = 0; i < N; i++) {
        printf("Enter number %d: ", i + 1);
        scanf("%d", &arr[i]);
    }

    // Input K
    printf("Enter K: ");
    scanf("%d", &K);

    // Process array elements
    for (i = 0; i < N; i++) {
        if (i % 2 == 0) {
            // Even index, add K
            arr[i] += K;
        } else {
            // Odd index, subtract K
            arr[i] -= K;
        }
    }

    // Display result
    printf("Result: ");
    for (i = 0; i < N; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}
```

### Part (c): Write a program which will take input of N x N numbers in a 2D array A. Now swap all the elements in the first and last column within the array and finally print the array:

```c
#include <stdio.h>

int main() {
    int N, i, j, temp;

    // Input size of the square matrix
    printf("Enter the size of the square matrix (N): ");
    scanf("%d", &N);

    int A[N][N];

    // Input matrix elements
    printf("Enter the matrix elements:\n");
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++) {
            scanf("%d", &A[i][j]);
        }
    }

    // Swap first and last column
    for (i = 0; i < N; i++) {
        temp = A[i][0];        // Store first column element
        A[i][0] = A[i][N-1];   // Replace first with last
        A[i][N-1] = temp;      // Replace last with stored first
    }

    // Display the modified matrix
    printf("Modified matrix:\n");
    for (i = 0; i < N; i++) {
        for (j = 0; j < N; j++) {
            printf("%d ", A[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

## Question 16

### Part (a): Variable Name Validity

Analyze which variable names are valid or invalid:

| Variable | Validity | Reason |
|----------|----------|---------|
| `int_a` | **Valid** | Contains letters and underscore, follows C naming rules |
| `_num` | **Valid** | Starts with underscore followed by letters (though reserved for system) |
| `99p` | **Invalid** | Cannot start with digits in C |
| `"my_val"` | **Invalid** | Double quotes not allowed in identifiers |

### Part (b): Variable Value Computation

Given ASCII codes: A=65, a=97, 0=48

**Expression Analysis:**

**(i) `float a = 101/7;`**
```
101/7 = 14 (integer division)
Result: a = 14.0
```

**(ii) `float b = (float)(3%5);`**
```
3%5 = 3 (since 3 < 5)
Cast to float: b = 3.0
```

**(iii) `float c = 21>43 || 6!=6;`**
```
21 > 43 → false (0)
6 != 6 → false (0)  
false || false → false (0)
Result: c = 0.0
```

**(iv) `double result = 12 + (1 * '3');`**
```
ASCII of '3' = 51
1 * 51 = 51
12 + 51 = 63
Result: result = 63.0
```

### Part (c): Code Output Analysis

**Given Code:**
```c
int num; 
scanf("%d", &num); 
if (num % 2 != 0) { 
    printf("Mashrafe\n"); 
} 
if (num < 100) { 
    printf("Shakib\n"); 
} else if (num >= 100) { 
    printf("Mahmudullah\n"); 
} 
if (num >= 0 && num < 5) { 
    printf("Imrul\n"); 
} else if (num >= 0 && num <= 49) { 
    printf("Tamim\n"); 
} else { 
    printf("Rubel\n"); 
} 
```

**Case (i): Input = 2.3**
- `scanf("%d", &num)` reads integer part: `num = 2`
- `2 % 2 != 0` → false, no "Mashrafe"
- `2 < 100` → true, prints "Shakib"
- `2 >= 0 && 2 < 5` → true, prints "Imrul"

**Output:** `Shakib\nImrul\n`

**Case (ii): Input = 127**
- `num = 127`
- `127 % 2 != 0` → true, prints "Mashrafe"
- `127 < 100` → false, `127 >= 100` → true, prints "Mahmudullah"
- `127 >= 0 && 127 < 5` → false
- `127 >= 0 && 127 <= 49` → false
- Else condition: prints "Rubel"

**Output:** `Mashrafe\nMahmudullah\nRubel\n`

---

## Question 17: Switch Statement Analysis

### Part (a): Code Trace

**Given Code:**
```c
int a,b,c; 
scanf("%d%d%d",&a,&b,&c); 
int result=a--/b++; 
switch(a+b){ 
case 1:  
    result+=a/c*2; 
    b++; 
case 2:  
case 3: 
    result=a*c/b; 
    a++; 
case 4: break; 
    a=2; 
default: result=5;                
} 
printf("%d %d %d %d", a,b,c,result); 
```

**Example with input: a=5, b=2, c=3**

**Step-by-step execution:**
1. `result = a--/b++` → `result = 5/2 = 2`, then `a=4, b=3`
2. `switch(a+b)` → `switch(4+3=7)`
3. No case matches 7, goes to `default`
4. `result = 5`

**Final values:** `a=4, b=3, c=3, result=5`
**Output:** `4 3 3 5`

---

## Question 18

### Part (a): Switch to If-Else Conversion

**Converted Code:**
```c
int a,b,c; 
scanf("%d%d%d",&a,&b,&c); 
int result=a--/b++; 
int switchValue = a+b;

if(switchValue == 1) {
    result += a/c*2; 
    b++; 
    // Fall through to case 2/3
    result = a*c/b; 
    a++; 
} else if(switchValue == 2 || switchValue == 3) {
    result = a*c/b; 
    a++; 
} else if(switchValue == 4) {
    // Do nothing (break equivalent)
} else {
    result = 5; 
}
printf("%d %d %d %d", a,b,c,result); 
```

### Part (b): Loop Trace

**Original Code (with corrections):**
```c
int start=105, end=112, count=0; 
for(int i=end; i>=start; i--){ 
    if(end%2 != 0){ 
        count++; 
        start++; 
        end += 2;  // Corrected from end+2
    } else { 
        end--; 
        start += 1;  // Corrected from start+1
    } 
} 
```

**Trace Table:**

| Iteration | i | start | end | count | Condition | Action |
|-----------|---|-------|-----|-------|-----------|---------|
| 1 | 112 | 105 | 112 | 0 | 112%2==0 | end--, start++ → end=111, start=106 |
| 2 | 111 | 106 | 111 | 0 | 111%2!=0 | count++, start++, end+=2 → count=1, start=107, end=113 |
| 3 | 110 | 107 | 113 | 1 | 113%2!=0 | count++, start++, end+=2 → count=2, start=108, end=115 |
| ... | ... | ... | ... | ... | ... | ... |

---

## Question 19

### Part (a): 'M' Pattern Program

**Algorithm:**
- Print '*' at first and last columns
- Print '*' on main diagonal (upper half)
- Print '*' on anti-diagonal (upper half)

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter n: ");
    scanf("%d", &n);
    
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            if(j == 0 || j == n-1 || 
               (i == j && i <= n/2) || 
               (i + j == n-1 && i <= n/2)) {
                printf("*");
            } else {
                printf(" ");
            }
        }
        printf("\n");
    }
    return 0;
}
```

### Part (b): Loop Replacement

**Original:**
```c
int a=10, b=20, count=0; 
for(int i=b; i>=a; i--){ 
    for(int j=a; j<=b; j++){ 
        printf("%d ", j); 
    } 
    if(b%2 != 0){           
        printf("%d \n", a); 
    } else { 
        printf("%d \n", b); 
    } 
} 
```

**Converted (while + do-while):**
```c
int a=10, b=20, count=0; 
int i = b;
while(i >= a) {
    int j = a;
    do {
        printf("%d ", j);
        j++;
    } while(j <= b);
    
    if(b % 2 != 0) {
        printf("%d \n", a);
    } else {
        printf("%d \n", b);
    }
    i--;
}
```

---

## Question 20

### Part (a): Flowchart for Factorial Code

```mermaid
flowchart TD
    A[START] --> B[Input n]
    B --> C{n <= 0?}
    C -->|YES| D[Print "Enter a +ve integer"]
    C -->|NO| E[fact = 1, i = 1]
    D --> F[END]
    E --> G[fact *= i]
    G --> H[i++]
    H --> I{i <= n?}
    I -->|YES| G
    I -->|NO| J[Print factorial]
    J --> F
```

### Part (b): Bank Balance Filter Program

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number of clients: ");
    scanf("%d", &n);
    
    double balances[100];  // Fixed size array
    
    // Input all balances
    printf("Enter balances:\n");
    for(int i = 0; i < n; i++) {
        printf("Client %d: ", i+1);
        scanf("%lf", &balances[i]);
    }
    
    // Display only valid balances (>= 500.00)
    printf("\nValid balances (>= 500.00 taka):\n");
    int count = 0;
    for(int i = 0; i < n; i++) {
        if(balances[i] >= 500.00) {
            printf("Client %d: %.2lf taka\n", i+1, balances[i]);
            count++;
        }
    }
    
    if(count == 0) {
        printf("No valid balances found.\n");
    }
    
    return 0;
}
```

---

## Question 21

### Part (a): Manual Trace of Array Code

**Given Code:**
```c
int ara[5] = {8, 6, 2, 4, 7};  
for(int i = 1; i < 5; i += 2){ 
   ara[i] = 3 * ara[i - 1];  
} 
for(int i = 1; i < 5; i++){ 
   if(i % 2 == 0){ 
      ara[i] = i * 4 + ara[i-1]; 
   } 
} 
```

**Initial State:**
```
ara[0] = 8, ara[1] = 6, ara[2] = 2, ara[3] = 4, ara[4] = 7
```

**First Loop Trace (i += 2):**

| Step | i | Condition | ara[i-1] | Calculation | New ara[i] | Array State |
|------|---|-----------|----------|-------------|------------|-------------|
| Initial | - | - | - | - | - | {8, 6, 2, 4, 7} |
| 1 | 1 | i < 5 ✓ | ara[0] = 8 | 3 × 8 = 24 | ara[1] = 24 | {8, 24, 2, 4, 7} |
| 2 | 3 | i < 5 ✓ | ara[2] = 2 | 3 × 2 = 6 | ara[3] = 6 | {8, 24, 2, 6, 7} |
| 3 | 5 | i < 5 ✗ | - | Loop ends | - | {8, 24, 2, 6, 7} |

**Second Loop Trace (i++):**

| Step | i | Condition | i % 2 == 0? | ara[i-1] | Calculation | New ara[i] | Array State |
|------|---|-----------|-------------|----------|-------------|------------|-------------|
| Start | - | - | - | - | - | - | {8, 24, 2, 6, 7} |
| 1 | 1 | i < 5 ✓ | 1 % 2 = 1 ✗ | - | Skip | - | {8, 24, 2, 6, 7} |
| 2 | 2 | i < 5 ✓ | 2 % 2 = 0 ✓ | ara[1] = 24 | 2×4 + 24 = 32 | ara[2] = 32 | {8, 24, 32, 6, 7} |
| 3 | 3 | i < 5 ✓ | 3 % 2 = 1 ✗ | - | Skip | - | {8, 24, 32, 6, 7} |
| 4 | 4 | i < 5 ✓ | 4 % 2 = 0 ✓ | ara[3] = 6 | 4×4 + 6 = 22 | ara[4] = 22 | {8, 24, 32, 6, 22} |
| 5 | 5 | i < 5 ✗ | - | Loop ends | - | - | {8, 24, 32, 6, 22} |

**Final Result:** `ara = {8, 24, 32, 6, 22}`

### Part (b): Manual Trace of 2D Array Sum Code

**Given Code:**
```c
int row, col, sum = 0; 
int A[][3] = {{1,2,3}, {11,5,6}, {12,7,9}, {8,13,4}}; 
for(row=0; row<4; row++){ 
   for(col=0; col<3; col++){ 
      if(col > row) { 
          sum += A[row][col]; 
      } 
   } 
} 
```

**Matrix A Visualization:**
```
     col: 0   1   2
row 0:    1   2   3
row 1:   11   5   6  
row 2:   12   7   9
row 3:    8  13   4
```

**Complete Execution Trace:**

| Step | row | col | col > row? | A[row][col] | Action | sum | Comment |
|------|-----|-----|------------|-------------|---------|-----|---------|
| Initial | - | - | - | - | - | 0 | Starting value |
| 1 | 0 | 0 | 0 > 0 ✗ | A[0][0] = 1 | Skip | 0 | - |
| 2 | 0 | 1 | 1 > 0 ✓ | A[0][1] = 2 | sum += 2 | 2 | Add upper triangle element |
| 3 | 0 | 2 | 2 > 0 ✓ | A[0][2] = 3 | sum += 3 | 5 | Add upper triangle element |
| 4 | 1 | 0 | 0 > 1 ✗ | A[1][0] = 11 | Skip | 5 | - |
| 5 | 1 | 1 | 1 > 1 ✗ | A[1][1] = 5 | Skip | 5 | - |
| 6 | 1 | 2 | 2 > 1 ✓ | A[1][2] = 6 | sum += 6 | 11 | Add upper triangle element |
| 7 | 2 | 0 | 0 > 2 ✗ | A[2][0] = 12 | Skip | 11 | - |
| 8 | 2 | 1 | 1 > 2 ✗ | A[2][1] = 7 | Skip | 11 | - |
| 9 | 2 | 2 | 2 > 2 ✗ | A[2][2] = 9 | Skip | 11 | - |
| 10 | 3 | 0 | 0 > 3 ✗ | A[3][0] = 8 | Skip | 11 | - |
| 11 | 3 | 1 | 1 > 3 ✗ | A[3][1] = 13 | Skip | 11 | - |
| 12 | 3 | 2 | 2 > 3 ✗ | A[3][2] = 4 | Skip | 11 | - |

**Upper Triangle Elements Added:**
- A[0][1] = 2
- A[0][2] = 3  
- A[1][2] = 6

**Final Result:** `sum = 11`

**Pattern Analysis:** The code sums all elements in the upper triangle of the matrix (where column index > row index).

---

## Summary

This test covers fundamental C programming concepts including:
- Variable naming conventions
- Data type operations and type casting
- Control structures (if-else, switch, loops)
- Array manipulation (1D and 2D)
- Code tracing and debugging
- Pattern programming
- Flow control conversion between different structures
