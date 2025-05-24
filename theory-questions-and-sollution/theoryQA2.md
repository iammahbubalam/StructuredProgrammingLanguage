# Theory Questions and Solutions - Set 2

## Question 1

### (a) Program for Divisors and Perfect Squares

**Write a C program that satisfies the following requirements:**

i. Write a function `int count_divisors(int n)` that returns the total number of divisors of a given number n.
ii. Write a function `int is_perfect_square(int n)` that returns 1 if the given integer n is a perfect square, and 0 otherwise.
iii. In the main function, take two positive integers as input from the user. Then determine:
   - which number has more divisors.
   - whether each of the two numbers is a perfect square or not.

**Notes:**
- There are 4 divisors of 6: 1, 2, 3 and 6. So, `count_divisors(6)` should return 4.
- An integer n is a perfect square if there exists an integer m such that m × m = n.
- 4 is a perfect square because 4 = 2², but 5 is not a perfect square. So, `is_perfect_square(4)` should return 1 and `is_perfect_square(5)` should return 0.

**Solution:**

```c
#include <stdio.h>
#include <math.h>

// Function to count the divisors of a number
int count_divisors(int n) {
    int count = 0;
    
    // Optimization: only need to check up to sqrt(n)
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            // If divisors are equal, count only one
            if (n / i == i) {
                count++;
            } else { // Otherwise count both
                count += 2;
            }
        }
    }
    
    return count;
}

// Function to check if a number is a perfect square
int is_perfect_square(int n) {
    // Find the square root of n
    int sqrt_n = sqrt(n);
    
    // Check if square root multiplied by itself equals n
    if (sqrt_n * sqrt_n == n) {
        return 1;  // It's a perfect square
    } else {
        return 0;  // It's not a perfect square
    }
}

int main() {
    int num1, num2;
    
    // Input two numbers
    printf("Enter first positive integer: ");
    scanf("%d", &num1);
    
    printf("Enter second positive integer: ");
    scanf("%d", &num2);
    
    // Validate input
    if (num1 <= 0 || num2 <= 0) {
        printf("Error: Please enter positive integers only.\n");
        return 1;
    }
    
    // Count divisors for both numbers
    int div_count1 = count_divisors(num1);
    int div_count2 = count_divisors(num2);
    
    // Compare number of divisors
    printf("\nNumber of divisors:\n");
    printf("%d has %d divisors\n", num1, div_count1);
    printf("%d has %d divisors\n", num2, div_count2);
    
    if (div_count1 > div_count2) {
        printf("%d has more divisors than %d\n", num1, num2);
    } else if (div_count2 > div_count1) {
        printf("%d has more divisors than %d\n", num2, num1);
    } else {
        printf("Both numbers have the same number of divisors\n");
    }
    
    // Check if numbers are perfect squares
    printf("\nPerfect square check:\n");
    
    if (is_perfect_square(num1)) {
        printf("%d is a perfect square\n", num1);
    } else {
        printf("%d is not a perfect square\n", num1);
    }
    
    if (is_perfect_square(num2)) {
        printf("%d is a perfect square\n", num2);
    } else {
        printf("%d is not a perfect square\n", num2);
    }
    
    return 0;
}
```

### (b) Code Tracing with Local and Global Variables

**Determine the output of the following C code. Notice the use of local and global variables in different contexts.**

```c
#include <stdio.h>
int x = 10;
int y = 20;
int func(int a, int b) {
    int y = 5;
    x += 2;
    y += 3;
    a += y;
    b += x;
    printf("x = %d, y = %d, a = %d, b = %d.\n", x, y, a, b);
    return a * b + x - y;
}
int main() {
    int a = 4, b = 7;
    a = func(a, b);
    printf("a = %d, b = %d, x = %d.\n", a, b, x);
    return 0;
}
```

**Step-by-step Trace:**

1. Program starts with global variables: `x = 10`, `y = 20`
2. In `main()`, local variables are initialized: `a = 4`, `b = 7`
3. Function `func(4, 7)` is called with arguments copied by value
   - Inside `func()`, a local variable `y = 5` is created (shadows global `y`)
   - `x += 2` changes global `x` to `12`
   - `y += 3` changes local `y` to `8` (not the global `y`)
   - `a += y` makes `a = 4 + 8 = 12`
   - `b += x` makes `b = 7 + 12 = 19`
   - First `printf` outputs: `x = 12, y = 8, a = 12, b = 19.`
   - Function returns `a * b + x - y = 12 * 19 + 12 - 8 = 228 + 4 = 232`
4. In `main()`, `a` gets the return value: `a = 232`, but `b` remains unchanged since it was passed by value
5. Second `printf` outputs: `a = 232, b = 7, x = 12.`

**Final Output:**
```
x = 12, y = 8, a = 12, b = 19.
a = 232, b = 7, x = 12.
```

## Question 2

### (a) String Manipulation Code Trace

**Manually trace the following code segment. Show the changes of all the variables. Then write down the output of the program.**

```c
int i, j;
char s1[20] = "ABCd", s2[20] = "EFGH789";
for (i = 0; s1[i] != 0; i++) {
    // do nothing
}
for (j = 0; s2[j] != 0; j++) {
    if (s2[j] >= '0' && s2[j] <= '9') {
        s1[i] = s2[j];
        i++;
    }
}
s1[i] = 0;
printf("S1 = %s", s1);
```

**Step-by-step Trace:**

| Step | Operation | i | j | s1 | s2 | Explanation |
|------|-----------|---|---|----|----|-------------|
| 1 | Initialize | - | - | "ABCd\0" | "EFGH789\0" | Initial state |
| 2 | First loop | 0 | - | "ABCd\0" | "EFGH789\0" | Check s1[0] != 0 (true) |
| 3 | First loop | 1 | - | "ABCd\0" | "EFGH789\0" | Check s1[1] != 0 (true) |
| 4 | First loop | 2 | - | "ABCd\0" | "EFGH789\0" | Check s1[2] != 0 (true) |
| 5 | First loop | 3 | - | "ABCd\0" | "EFGH789\0" | Check s1[3] != 0 (true) |
| 6 | First loop | 4 | - | "ABCd\0" | "EFGH789\0" | Check s1[4] != 0 (false, null terminator) |
| 7 | Second loop | 4 | 0 | "ABCd\0" | "EFGH789\0" | Check s2[0] != 0 (true) |
| 8 | If condition | 4 | 0 | "ABCd\0" | "EFGH789\0" | 'E' is not a digit, skip |
| 9 | Second loop | 4 | 1 | "ABCd\0" | "EFGH789\0" | Check s2[1] != 0 (true) |
| 10 | If condition | 4 | 1 | "ABCd\0" | "EFGH789\0" | 'F' is not a digit, skip |
| 11 | Second loop | 4 | 2 | "ABCd\0" | "EFGH789\0" | Check s2[2] != 0 (true) |
| 12 | If condition | 4 | 2 | "ABCd\0" | "EFGH789\0" | 'G' is not a digit, skip |
| 13 | Second loop | 4 | 3 | "ABCd\0" | "EFGH789\0" | Check s2[3] != 0 (true) |
| 14 | If condition | 4 | 3 | "ABCd\0" | "EFGH789\0" | 'H' is not a digit, skip |
| 15 | Second loop | 4 | 4 | "ABCd\0" | "EFGH789\0" | Check s2[4] != 0 (true) |
| 16 | If condition | 4 | 4 | "ABCd\0" | "EFGH789\0" | '7' is a digit, set s1[4]='7', i++ |
| 17 | Second loop | 5 | 5 | "ABCd7\0" | "EFGH789\0" | Check s2[5] != 0 (true) |
| 18 | If condition | 5 | 5 | "ABCd7\0" | "EFGH789\0" | '8' is a digit, set s1[5]='8', i++ |
| 19 | Second loop | 6 | 6 | "ABCd78\0" | "EFGH789\0" | Check s2[6] != 0 (true) |
| 20 | If condition | 6 | 6 | "ABCd78\0" | "EFGH789\0" | '9' is a digit, set s1[6]='9', i++ |
| 21 | Second loop | 7 | 7 | "ABCd789\0" | "EFGH789\0" | Check s2[7] != 0 (false, null terminator) |
| 22 | Set null | 7 | 7 | "ABCd789\0" | "EFGH789\0" | Set s1[7]=0 (null terminator) |

**Final Output:**
```
S1 = ABCd789
```

**Explanation:** The first loop finds the length of s1 (which is 4 characters). The second loop examines each character in s2. When it finds a digit (7, 8, or 9), it appends that digit to s1 and increments i. The result is that the digits from s2 are appended to s1, giving "ABCd789".

### (b) String Reverse Function

**Write a function `void myStrRev(char src[], char dest [])` that stores the reverse of src into dest. You are not allowed to use <string.h>.**

**Solution:**

```c
void myStrRev(char src[], char dest[]) {
    int length = 0;
    
    // Calculate length of source string
    while (src[length] != '\0') {
        length++;
    }
    
    // Copy characters in reverse order
    for (int i = 0; i < length; i++) {
        dest[i] = src[length - 1 - i];
    }
    
    // Add null terminator to destination
    dest[length] = '\0';
}
```

**Explanation:**
1. First, we calculate the length of the source string by counting characters until we find the null terminator.
2. Then, we copy each character from the source to the destination in reverse order:
   - The first character in dest becomes the last character from src
   - The second character in dest becomes the second-to-last from src
   - And so on...
3. Finally, we add a null terminator to the end of the destination string to make it a valid C string.

**Example usage:**
```c
#include <stdio.h>

void myStrRev(char src[], char dest[]) {
    // Implementation as above
}

int main() {
    char source[] = "Hello World";
    char destination[20]; // Make sure dest has enough space
    
    myStrRev(source, destination);
    
    printf("Source: %s\n", source);
    printf("Reversed: %s\n", destination);
    
    return 0;
}
```

**Output:**
```
Source: Hello World
Reversed: dlroW olleH
```

## Question 3

### (a) String Pointer Manipulation

**Determine the output of the following C code segment for each of the given inputs.**

```c
char s[] = "computer club";
char *p, ch;
p = s;
scanf("%c", &ch);
while (*p != ch) {
    printf("%c", *p);
    p++;
}
```

**For input (i) u:**

| Step | p points to | *p | ch | Condition (*p != ch) | Output | Action |
|------|-------------|----|----|---------------------|--------|--------|
| 1 | s[0] = 'c' | 'c' | 'u' | true | c | p++ |
| 2 | s[1] = 'o' | 'o' | 'u' | true | o | p++ |
| 3 | s[2] = 'm' | 'm' | 'u' | true | m | p++ |
| 4 | s[3] = 'p' | 'p' | 'u' | true | p | p++ |
| 5 | s[4] = 'u' | 'u' | 'u' | false | - | Exit loop |

**Output:** `comp`

**For input (ii) c:**

| Step | p points to | *p | ch | Condition (*p != ch) | Output | Action |
|------|-------------|----|----|---------------------|--------|--------|
| 1 | s[0] = 'c' | 'c' | 'c' | false | - | Exit loop |

**Output:** ` ` (empty string)

**For input (iii) r:**

| Step | p points to | *p | ch | Condition (*p != ch) | Output | Action |
|------|-------------|----|----|---------------------|--------|--------|
| 1 | s[0] = 'c' | 'c' | 'r' | true | c | p++ |
| 2 | s[1] = 'o' | 'o' | 'r' | true | o | p++ |
| 3 | s[2] = 'm' | 'm' | 'r' | true | m | p++ |
| 4 | s[3] = 'p' | 'p' | 'r' | true | p | p++ |
| 5 | s[4] = 'u' | 'u' | 'r' | true | u | p++ |
| 6 | s[5] = 't' | 't' | 'r' | true | t | p++ |
| 7 | s[6] = 'e' | 'e' | 'r' | true | e | p++ |
| 8 | s[7] = 'r' | 'r' | 'r' | false | - | Exit loop |

**Output:** `compute`

### (b) Pointer Operations

**Determine the output of the following C code segment.**

```c
int x, *y;
x = 10;
y = &x;
x = x + 1;
// address of x: 672454436
// address of y: 672454440
printf("%d\n", y);
printf("%d\n", *y);
printf("%d\n", x--);
printf("%d\n", *y);
```

**Step-by-step Trace:**

| Statement | x | y | *y | Output | Explanation |
|-----------|---|---|----|---------|-|
| `x = 10;` | 10 | undefined | - | - | Initialize x to 10 |
| `y = &x;` | 10 | 672454436 | 10 | - | y points to address of x |
| `x = x + 1;` | 11 | 672454436 | 11 | - | Increment x to 11 |
| `printf("%d\n", y);` | 11 | 672454436 | 11 | 672454436 | Print the address in y |
| `printf("%d\n", *y);` | 11 | 672454436 | 11 | 11 | Print the value at address in y |
| `printf("%d\n", x--);` | 10 | 672454436 | 10 | 11 | Print x (11), then decrement to 10 |
| `printf("%d\n", *y);` | 10 | 672454436 | 10 | 10 | Print the value at address in y |

**Output:**
```
672454436
11
11
10
```

### (c) Factorial using Call by Reference

**Write a program to calculate the factorial of a given number following the following steps:**
- Input the number in the main function.
- Pass this number to the factorial function.
- Calculate the factorial value in the factorial function.
- Print the factorial result in the main function. Use the concept of call by reference.

**Solution:**

```c
#include <stdio.h>

// Factorial function using call by reference
void factorial(int n, unsigned long long *result) {
    *result = 1;  // Initialize result to 1
    
    // Calculate factorial
    for (int i = 1; i <= n; i++) {
        *result = *result * i;
    }
}

int main() {
    int number;
    unsigned long long fact;
    
    // Input the number
    printf("Enter a non-negative integer to calculate factorial: ");
    scanf("%d", &number);
    
    // Check for negative numbers
    if (number < 0) {
        printf("Error: Factorial is not defined for negative numbers.\n");
        return 1;
    }
    
    // Calculate factorial using call by reference
    factorial(number, &fact);
    
    // Print the result
    printf("Factorial of %d is %llu\n", number, fact);
    
    return 0;
}
```

**Explanation:**
1. We define a function `factorial` that takes two parameters:
   - `n`: the number to calculate factorial for
   - `result`: a pointer to an unsigned long long variable where the result will be stored
2. Inside the function, we initialize `*result` to 1, then multiply it by each number from 1 to n.
3. Since we're using a pointer (`result`), any changes made to `*result` in the function are directly reflected in the variable `fact` in the main function.
4. This is an example of "call by reference" because we're passing the address (reference) of the variable to be modified.
5. We use `unsigned long long` to handle larger factorial values.

## Question 4

**Write a C program that satisfies the following requirements:**
i. Create a structure named Book to store details about a book like title, author, and price.
ii. Input the details of three books and store it in an array of structures.
iii. Display the information of the book with the highest price and the one with the lowest price.

**Solution:**

```c
#include <stdio.h>
#include <string.h>

// Define the Book structure
struct Book {
    char title[100];
    char author[100];
    float price;
};

int main() {
    // Create an array of 3 Book structures
    struct Book books[3];
    int i;
    
    // Input details for each book
    for (i = 0; i < 3; i++) {
        printf("\nEnter details for Book %d:\n", i+1);
        
        printf("Title: ");
        // Use fgets to safely read strings with spaces
        fflush(stdin); // Clear input buffer
        fgets(books[i].title, sizeof(books[i].title), stdin);
        // Remove newline character if present
        books[i].title[strcspn(books[i].title, "\n")] = '\0';
        
        printf("Author: ");
        fgets(books[i].author, sizeof(books[i].author), stdin);
        books[i].author[strcspn(books[i].author, "\n")] = '\0';
        
        printf("Price: ");
        scanf("%f", &books[i].price);
        fflush(stdin); // Clear input buffer for next iteration
    }
    
    // Find book with highest price
    int highest_index = 0;
    for (i = 1; i < 3; i++) {
        if (books[i].price > books[highest_index].price) {
            highest_index = i;
        }
    }
    
    // Find book with lowest price
    int lowest_index = 0;
    for (i = 1; i < 3; i++) {
        if (books[i].price < books[lowest_index].price) {
            lowest_index = i;
        }
    }
    
    // Display the highest price book
    printf("\nBook with the highest price:\n");
    printf("Title: %s\n", books[highest_index].title);
    printf("Author: %s\n", books[highest_index].author);
    printf("Price: $%.2f\n", books[highest_index].price);
    
    // Display the lowest price book
    printf("\nBook with the lowest price:\n");
    printf("Title: %s\n", books[lowest_index].title);
    printf("Author: %s\n", books[lowest_index].author);
    printf("Price: $%.2f\n", books[lowest_index].price);
    
    return 0;
}
```

**Explanation:**
1. We define a structure `Book` with fields for title, author, and price.
2. We create an array to store information for 3 books.
3. We input details for each book, using safe string input methods:
   - `fgets` to read strings with spaces
   - `fflush(stdin)` to clear the input buffer
   - `strcspn` to remove newline characters from input
4. We find the indices of the books with the highest and lowest prices.
5. We display the details of those books with proper formatting.

## Question 5

**Write down a program that counts number of words in a text file named "A.txt". You can safely assume that it's in the same folder as the source code and it doesn't contain any trailing spaces.**

**Solution:**

```c
#include <stdio.h>

int main() {
    FILE *file;
    char ch, prevCh = ' ';
    int wordCount = 0;
    
    // Open file for reading
    file = fopen("A.txt", "r");
    
    // Check if file exists
    if (file == NULL) {
        printf("Error: Could not open file A.txt\n");
        return 1;
    }
    
    // Count words
    while ((ch = fgetc(file)) != EOF) {
        // If current character is a space/newline/tab and previous was not
        // then we've found the end of a word
        if ((ch == ' ' || ch == '\n' || ch == '\t') && 
            !(prevCh == ' ' || prevCh == '\n' || prevCh == '\t')) {
            wordCount++;
        }
        prevCh = ch;
    }
    
    // If the file doesn't end with space/newline/tab, count the last word
    if (!(prevCh == ' ' || prevCh == '\n' || prevCh == '\t') && prevCh != EOF) {
        wordCount++;
    }
    
    // Close the file
    fclose(file);
    
    // Display result
    printf("Number of words in the file: %d\n", wordCount);
    
    return 0;
}
```

**Explanation:**
1. We open the file "A.txt" for reading.
2. We read the file character by character:
   - `ch` holds the current character
   - `prevCh` holds the previous character
3. We count a word whenever we encounter a whitespace character (space, newline, tab) after a non-whitespace character.
4. Special case: If the file doesn't end with whitespace, we need to count the last word separately.
5. Finally, we display the total number of words found.

**Example:**
If A.txt contains: "Hello world! This is a test."
The program will count 6 words.

## Question 6

**Solve any one of the two following problems:**

### Problem (i): Fix the Recursive Function

**Find the bug in the recursive function and rewrite it. The fixed function should work correctly for any positive value of n.**

```c
int addDigits(int n) {
    return (n % 10) + addDigits(n / 10);
}

void main() {
    int k;
    k = addDigits(4531);
    printf("k = %d", k);
}
```

**Expected Output:**
```
k = 13
```

**Bug and Fixed Solution:**

The bug is that the recursive function doesn't have a base case, so it will keep calling itself indefinitely even when n becomes 0, causing a stack overflow.

**Fixed Version:**

```c
#include <stdio.h>

int addDigits(int n) {
    // Base case: when n is 0, return 0
    if (n == 0) {
        return 0;
    }
    // Return last digit + sum of remaining digits
    return (n % 10) + addDigits(n / 10);
}

int main() {
    int k;
    k = addDigits(4531);
    printf("k = %d", k);
    return 0;
}
```

**Explanation:**
1. The bug is that the recursive function doesn't have a base case to stop recursion.
2. In recursion, a base case is essential to prevent infinite recursion.
3. The fixed version adds a base case: when n is 0, return 0.
4. For the input 4531, the function calculates:
   - 1 + addDigits(453)
   - 1 + (3 + addDigits(45))
   - 1 + (3 + (5 + addDigits(4)))
   - 1 + (3 + (5 + (4 + addDigits(0))))
   - 1 + (3 + (5 + (4 + 0)))
   - 1 + 3 + 5 + 4 = 13

### Problem (ii): File I/O for Even/Odd Sums

**The file "input.txt" contains 5 integers. Write a program that reads the 5 integers and prints the sum of all even numbers and the sum of all odd numbers in another file "output.txt".**

**Solution:**

```c
#include <stdio.h>

int main() {
    FILE *inputFile, *outputFile;
    int num;
    int evenSum = 0, oddSum = 0;
    int count = 0;
    
    // Open input file for reading
    inputFile = fopen("input.txt", "r");
    
    // Check if input file exists
    if (inputFile == NULL) {
        printf("Error: Could not open input file!\n");
        return 1;
    }
    
    // Read 5 integers from input file
    while (count < 5 && fscanf(inputFile, "%d", &num) == 1) {
        // Add to appropriate sum
        if (num % 2 == 0) {
            // Even number
            evenSum += num;
        } else {
            // Odd number
            oddSum += num;
        }
        count++;
    }
    
    // Verify we read exactly 5 numbers
    if (count < 5) {
        printf("Warning: Input file contains fewer than 5 integers.\n");
    }
    
    // Close input file
    fclose(inputFile);
    
    // Open output file for writing
    outputFile = fopen("output.txt", "w");
    
    // Check if output file was created successfully
    if (outputFile == NULL) {
        printf("Error: Could not create output file!\n");
        return 1;
    }
    
    // Write results to output file
    fprintf(outputFile, "%d %d", evenSum, oddSum);
    
    // Close output file
    fclose(outputFile);
    
    printf("Success: Sums have been written to output.txt\n");
    
    return 0;
}
```

**Explanation:**
1. We open "input.txt" for reading.
2. We read integers from the file one by one:
   - We use `fscanf` with a return value check to ensure valid input
   - We keep track of how many integers we've read
3. For each integer, we check if it's even or odd, and add it to the appropriate sum.
4. We verify that we read exactly 5 integers.
5. We open "output.txt" for writing.
6. We write the sums of even and odd numbers to the output file.

**Examples:**
- If "input.txt" contains: `1 2 3 4 5`
  - Even numbers: 2, 4 (sum = 6)
  - Odd numbers: 1, 3, 5 (sum = 9)
  - "output.txt" will contain: `6 9`

- If "input.txt" contains: `10 15 20 25 30`
  - Even numbers: 10, 20, 30 (sum = 60)
  - Odd numbers: 15, 25 (sum = 40)
  - "output.txt" will contain: `60 40`
