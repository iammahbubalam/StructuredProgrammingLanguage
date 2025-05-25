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


# Theory Questions and Solutions - Set 3

## Question 1

### (a) Implementing getSumMean Function

**Requirements:**
- Implement `getSumMean(float marks[], int N, int type)` function to compute sum or mean of marks of N students from an input array.
- Initialize an array in main() to store marks of 100 students with user input.
- Take number of elements and value type as input from user.
- If type is 1, return sum; if type is 2, return mean.
- Discuss the argument passing method used in the function call.

**Solution:**

```c
#include <stdio.h>

// Function to calculate sum or mean of marks
float getSumMean(float marks[], int N, int type) {
    float sum = 0.0;
    
    // Calculate sum of N elements
    for (int i = 0; i < N; i++) {
        sum += marks[i];
    }
    
    // Return sum or mean based on type
    if (type == 1) {
        return sum;  // Return sum
    } else if (type == 2) {
        return sum / N;  // Return mean
    } else {
        printf("Invalid type! Returning 0.\n");
        return 0.0;
    }
}

int main() {
    float studentMarks[100];  // Array to store marks of 100 students
    int n, type;
    
    // Input marks for students
    printf("Enter marks for students (up to 100):\n");
    for (int i = 0; i < 100; i++) {
        printf("Student %d: ", i+1);
        scanf("%f", &studentMarks[i]);
        
        // Ask if user wants to continue or stop
        if (i < 99) {
            char choice;
            printf("Enter more marks? (y/n): ");
            scanf(" %c", &choice);
            if (choice == 'n' || choice == 'N') {
                break;
            }
        }
    }
    
    // Input number of elements to process
    printf("\nEnter number of students to process: ");
    scanf("%d", &n);
    
    // Validate n
    if (n <= 0 || n > 100) {
        printf("Invalid number of students! Please enter a value between 1 and 100.\n");
        return 1;
    }
    
    // Input type (1 for sum, 2 for mean)
    printf("Enter type (1 for sum, 2 for mean): ");
    scanf("%d", &type);
    
    // Call getSumMean function and display result
    float result = getSumMean(studentMarks, n, type);
    
    if (type == 1) {
        printf("Sum of marks for %d students: %.2f\n", n, result);
    } else if (type == 2) {
        printf("Mean of marks for %d students: %.2f\n", n, result);
    } else {
        printf("Invalid type! Please enter 1 for sum or 2 for mean.\n");
    }
    
    return 0;
}
```

**Argument Passing Method Analysis:**

In the function call `getSumMean(studentMarks, n, type)`, the following argument passing methods are used:

1. `studentMarks` (array parameter): This is **call-by-reference**. When arrays are passed to functions in C, only the address of the first element is passed, not the entire array. This means the function receives a pointer to the array, allowing it to directly access and modify the original array elements if needed.

2. `n` and `type` (integer parameters): These are passed by **call-by-value**. Copies of these values are created and passed to the function. Any changes made to these parameters inside the function do not affect the original values in the calling function.

Justification: Although the function doesn't modify the array, it still has the capability to do so because it receives the memory address of the original array. This is why array passing in C is considered call-by-reference, while the scalar values like integers are passed by value.

### (b) Finding Output of Program with Local and Global Contexts

**Given Code:**
```c
int x = 6, y = 8; 
int func(int a, int b) {     
   a *= 2;     
   printf("a = %d, b = %d.\n", a, b); 
   return (--a) * (b--);  
}  
int sub(int a, int b) {     
   b /= 6;     
   printf("a = %d, b = %d.\n", a, b);     
   return (--a) * (--b);  
} 
int main() {         
   y = func(x, y);     
   printf("x = %d, y = %d.\n", x, y); 
   x = sub(x, y);     
   printf("x = %d, y = %d.\n", x, y); 
   return 0;  
} 
```

**Step-by-step Trace:**

1. Initialize global variables: `x = 6, y = 8`
2. Call `func(x, y)` with `a = 6, b = 8`
   - `a *= 2` → `a = 12`
   - Print: `a = 12, b = 8.`
   - Return `(--a) * (b--)` → `11 * 8 = 88` (a becomes 11, b becomes 7 after evaluation)
3. Assign return value to y: `y = 88`
4. Print: `x = 6, y = 88.`
5. Call `sub(x, y)` with `a = 6, b = 88`
   - `b /= 6` → `b = 14` (integer division: 88/6 = 14)
   - Print: `a = 6, b = 14.`
   - Return `(--a) * (--b)` → `5 * 13 = 65` (a becomes 5, b becomes 13 after evaluation)
6. Assign return value to x: `x = 65`
7. Print: `x = 65, y = 88.`

**Final Output:**
```
a = 12, b = 8.
x = 6, y = 88.
a = 6, b = 14.
x = 65, y = 88.
```

## Question 2

### (a) Manual Tracing of String Manipulation Program

**Given Code:**
```c
#include <stdio.h> 
#include <string.h> 
 
int main() { 
    char A[50] = "Structured"; 
    char B[50] = "Coding"; 
    int len = strlen(A); 
    for (int i=0; i<strlen(B); i++) 
      A[len-i-1] = B[i]; 
     
    strncat(A, B, 2); 
     
    for (int j=0; j<4; j++) 
      A[j] = B[strlen(B)-j-1]; 
    printf("A: %s\n", A); 
    printf("B: %s\n", B); 
    return 0; 
} 
```

**Manual Tracing:**

| Step | Operation | A | B | len | i/j | Explanation |
|------|-----------|---|---|----|-----|-------------|
| 1 | Initialize | "Structured\0" | "Coding\0" | - | - | Initial values |
| 2 | `len = strlen(A)` | "Structured\0" | "Coding\0" | 10 | - | Length of A is 10 |
| 3 | Loop starts | "Structured\0" | "Coding\0" | 10 | i=0 | First iteration |
| 4 | `A[len-i-1] = B[i]` | "StructureC\0" | "Coding\0" | 10 | i=0 | A[9] = B[0] = 'C' |
| 5 | Loop continues | "StructurCd\0" | "Coding\0" | 10 | i=1 | A[8] = B[1] = 'o' |
| 6 | Loop continues | "StructCod\0" | "Coding\0" | 10 | i=2 | A[7] = B[2] = 'd' |
| 7 | Loop continues | "StruCodi\0" | "Coding\0" | 10 | i=3 | A[6] = B[3] = 'i' |
| 8 | Loop continues | "StrCodin\0" | "Coding\0" | 10 | i=4 | A[5] = B[4] = 'n' |
| 9 | Loop continues | "StCoding\0" | "Coding\0" | 10 | i=5 | A[4] = B[5] = 'g' |
| 10 | Loop ends | "StCoding\0" | "Coding\0" | 10 | - | A now contains "StCoding" |
| 11 | `strncat(A, B, 2)` | "StCodingCo\0" | "Coding\0" | 10 | - | Append first 2 chars of B to A |
| 12 | Second loop starts | "StCodingCo\0" | "Coding\0" | 10 | j=0 | Second loop first iteration |
| 13 | `A[j] = B[strlen(B)-j-1]` | "gCodingCo\0" | "Coding\0" | 10 | j=0 | A[0] = B[5] = 'g' |
| 14 | Loop continues | "gnodingCo\0" | "Coding\0" | 10 | j=1 | A[1] = B[4] = 'n' |
| 15 | Loop continues | "gniingCo\0" | "Coding\0" | 10 | j=2 | A[2] = B[3] = 'i' |
| 16 | Loop continues | "gnidngCo\0" | "Coding\0" | 10 | j=3 | A[3] = B[2] = 'd' |
| 17 | Loop ends | "gnidngCo\0" | "Coding\0" | 10 | - | Final state |

**Final values:**
- A: "gnidngCo"
- B: "Coding"

**Output:**
```
A: gnidngCo
B: Coding
```

### (b) Replace Every Nth Character with 'Z'

**Write a C program to replace every nth character of a string with the letter 'Z'. You cannot use any library functions.**

```c
#include <stdio.h>

// Function to find string length without library functions
int stringLength(char str[]) {
    int length = 0;
    
    // Count characters until null terminator
    while (str[length] != '\0') {
        length++;
    }
    
    return length;
}

int main() {
    char string[100];
    int n;
    
    // Input string
    printf("Enter a string: ");
    scanf("%s", string);
    
    // Input value of n
    printf("Enter value of n (every nth character will be replaced): ");
    scanf("%d", &n);
    
    // Validate n
    if (n <= 0) {
        printf("Error: n must be a positive integer.\n");
        return 1;
    }
    
    // Find string length
    int length = stringLength(string);
    
    // Replace every nth character with 'Z'
    for (int i = n-1; i < length; i += n) {
        string[i] = 'Z';
    }
    
    // Display result
    printf("Modified string: %s\n", string);
    
    return 0;
}
```

**Explanation:**
1. We define a custom `stringLength` function to find the length of a string without using library functions.
2. We input the string and the value n from the user.
3. We replace every nth character with 'Z' by starting at index (n-1) and incrementing by n.
4. Finally, we display the modified string.

**Example 1:**
- Input string: "HelloWorld"
- n = 3
- Positions to replace (0-indexed): 2, 5, 8
- Result: "HeZloZorZd"

**Example 2:**
- Input string: "Programming"
- n = 2
- Positions to replace (0-indexed): 1, 3, 5, 7, 9
- Result: "PZoZrZmZiZg"

## Question 3

### (a) Identify and Correct Errors in Structure Code

**Given Code with Errors:**
```c
struct Gadget { 
   int serialNo, 
   char category[], 
   float price; 
} 
int main() { 
   struct g1; 
   serialNo = 123; 
   category = "Tab"; 
   price = 5500.00; 
   scanf("%c",g1.category); 
   scanf("%s",&G1.price); 
}
```

**Corrected Code:**
```c
#include <stdio.h>

struct Gadget { 
   int serialNo;  // Missing semicolon, added
   char category[20];  // Array size not specified, added size
   float price;  // No change needed
};  // Missing semicolon, added

int main() { 
   struct Gadget g1;  // Incorrect declaration, corrected
   g1.serialNo = 123;  // Missing struct variable name, added g1.
   strcpy(g1.category, "Tab");  // Can't assign string directly, use strcpy
   g1.price = 5500.00;  // Missing struct variable name, added g1.
   
   printf("Enter category: ");
   scanf("%s", g1.category);  // Incorrect format specifier and missing &, corrected
   
   printf("Enter price: ");
   scanf("%f", &g1.price);  // Incorrect variable name (G1 vs g1), corrected
   
   return 0;  // Missing return statement, added
}
```

**Errors Identified and Corrected:**
1. Missing semicolons after each field in the structure definition
2. Missing size specification for the character array `category`
3. Missing semicolon after the structure definition
4. Incorrect structure variable declaration (`struct g1` should be `struct Gadget g1`)
5. Direct access to structure members without specifying structure variable (`g1.`)
6. Direct string assignment to array (used `strcpy()` instead)
7. Incorrect format specifier in first `scanf` (used `%s` instead of `%c`)
8. Missing `&` in first `scanf` for character array
9. Capitalization error in second `scanf` (`G1` vs `g1`)
10. Missing return statement in main function

### (b) UIU Sports Club Player Management Program

**Create a C program for the UIU Sports Club to store and manage players' performance for the VC Cup football Season 3.**

```c
#include <stdio.h>
#include <string.h>

// Player structure definition
struct player {
    char name[50];
    int id;
    int matchesPlayed;
    int goals[50];  // Array to store goals in each match
};

// Function to calculate total goals scored by a player
int goalsScored(struct player p, int matches) {
    int totalGoals = 0;
    
    // Sum up goals from all matches
    for (int i = 0; i < matches; i++) {
        totalGoals += p.goals[i];
    }
    
    return totalGoals;
}

// Function to find player with highest goals
int selectBestScorer(struct player b[], int total_players) {
    int maxGoals = -1;
    int bestPlayerIndex = -1;
    
    // Compare goals of all players
    for (int i = 0; i < total_players; i++) {
        int playerGoals = goalsScored(b[i], b[i].matchesPlayed);
        
        // If current player has more goals than previous best
        if (playerGoals > maxGoals) {
            maxGoals = playerGoals;
            bestPlayerIndex = i;
        }
    }
    
    return bestPlayerIndex;
}

int main() {
    struct player players[120];  // Array to store 120 players
    int numPlayers;
    
    // Input number of players (for testing purposes, using a smaller number)
    printf("Enter number of players to register (up to 120): ");
    scanf("%d", &numPlayers);
    
    if (numPlayers <= 0 || numPlayers > 120) {
        printf("Invalid number of players. Please enter between 1 and 120.\n");
        return 1;
    }
    
    // Input data for each player
    for (int i = 0; i < numPlayers; i++) {
        printf("\nEnter details for Player %d:\n", i+1);
        
        printf("Name: ");
        scanf(" %[^\n]s", players[i].name);
        
        printf("ID: ");
        scanf("%d", &players[i].id);
        
        printf("Number of matches played: ");
        scanf("%d", &players[i].matchesPlayed);
        
        if (players[i].matchesPlayed <= 0 || players[i].matchesPlayed > 50) {
            printf("Invalid number of matches. Please enter between 1 and 50.\n");
            i--;  // Retry this player
            continue;
        }
        
        // Input goals for each match
        printf("Enter goals scored in each match:\n");
        for (int j = 0; j < players[i].matchesPlayed; j++) {
            printf("Match %d: ", j+1);
            scanf("%d", &players[i].goals[j]);
            
            if (players[i].goals[j] < 0) {
                printf("Invalid goal count. Goals cannot be negative.\n");
                j--;  // Retry this match
                continue;
            }
        }
    }
    
    // Find best goal scorer
    int bestScorer = selectBestScorer(players, numPlayers);
    
    // Display result
    if (bestScorer != -1) {
        int totalGoals = goalsScored(players[bestScorer], players[bestScorer].matchesPlayed);
        
        printf("\nBest Goal Scorer:\n");
        printf("Name: %s\n", players[bestScorer].name);
        printf("ID: %d\n", players[bestScorer].id);
        printf("Matches Played: %d\n", players[bestScorer].matchesPlayed);
        printf("Total Goals: %d\n", totalGoals);
    } else {
        printf("\nNo players found.\n");
    }
    
    return 0;
}
```

## Question 4

### (a) Function Call Analysis

**Given Code:**
```c
void f(char *s1, char *s2, int n, int *a) {     
    int i;      
    for(i=0; i<n; i++) {          
        if(s1[i] > s2[i]) *a = *a+1;            
        else if(s1[i]<s2[i]) *(s1+i)=*(s2+i); 
        else if(s1[i] == s2[i]) *a = *a-1; 
    }  
}  
void main() {      
    int a, b;      
    char s1[] = "worldcupBangladesh";      
    char s2[] = "BanglaWash";      
    a = 0;      
    f(s1,s2,13,&a);        
    printf("%d\n s1=%s , s2=%s\n",a,s1,s2);  
} 
```

**Step-by-step Trace:**

We need to trace through the function execution comparing characters at each position:

Initial values:
- s1 = "worldcupBangladesh"
- s2 = "BanglaWash"
- a = 0
- n = 13 (comparing first 13 characters)

Execution:
1. i=0: s1[0]='w', s2[0]='B'
   - 'w' > 'B'? No ('w' = 119, 'B' = 66 in ASCII)
   - 'w' < 'B'? No
   - 'w' == 'B'? No
   - No condition matches
   
2. i=1: s1[1]='o', s2[1]='a'
   - 'o' > 'a'? Yes ('o' = 111, 'a' = 97 in ASCII)
   - *a = *a + 1 = 0 + 1 = 1
   
3. i=2: s1[2]='r', s2[2]='n'
   - 'r' > 'n'? Yes ('r' = 114, 'n' = 110 in ASCII)
   - *a = *a + 1 = 1 + 1 = 2
   
4. i=3: s1[3]='l', s2[3]='g'
   - 'l' > 'g'? Yes ('l' = 108, 'g' = 103 in ASCII)
   - *a = *a + 1 = 2 + 1 = 3
   
5. i=4: s1[4]='d', s2[4]='l'
   - 'd' > 'l'? No ('d' = 100, 'l' = 108 in ASCII)
   - 'd' < 'l'? Yes
   - s1[4] = s2[4] => s1[4] = 'l'
   - s1 becomes "worllcupBangladesh"
   
6. i=5: s1[5]='c', s2[5]='a'
   - 'c' > 'a'? Yes ('c' = 99, 'a' = 97 in ASCII)
   - *a = *a + 1 = 3 + 1 = 4
   
7. i=6: s1[6]='u', s2[6]='W'
   - 'u' > 'W'? Yes ('u' = 117, 'W' = 87 in ASCII)
   - *a = *a + 1 = 4 + 1 = 5
   
8. i=7: s1[7]='p', s2[7]='a'
   - 'p' > 'a'? Yes ('p' = 112, 'a' = 97 in ASCII)
   - *a = *a + 1 = 5 + 1 = 6
   
9. i=8: s1[8]='B', s2[8]='s'
   - 'B' > 's'? No ('B' = 66, 's' = 115 in ASCII)
   - 'B' < 's'? Yes
   - s1[8] = s2[8] => s1[8] = 's'
   - s1 becomes "worllcups*angladesh" (* represents the modified part)
   
10. i=9: s1[9]='a', s2[9]='h'
    - 'a' > 'h'? No ('a' = 97, 'h' = 104 in ASCII)
    - 'a' < 'h'? Yes
    - s1[9] = s2[9] => s1[9] = 'h'
    - s1 becomes "worllcupsh*ngladesh"
    
11. i=10: s1[10]='n', s2[10]='\0' (end of string)
    - We're comparing with the null terminator, which has ASCII value 0
    - 'n' > '\0'? Yes
    - *a = *a + 1 = 6 + 1 = 7
    
12. i=11: s1[11]='g', s2[11]=undefined (past end of string)
    - Unpredictable behavior, but following the pattern, likely:
    - 'g' > undefined? Implementation-dependent
    - Let's assume *a = *a + 1 = 7 + 1 = 8
    
13. i=12: s1[12]='l', s2[12]=undefined (past end of string)
    - Unpredictable behavior
    - Let's assume *a = *a + 1 = 8 + 1 = 9

**Output (approximate due to undefined behavior):**
```
9
s1=worllcupshngladesh, s2=BanglaWash
```

**Argument Passing Analysis:**

In the function call `f(s1, s2, 13, &a)`, two different argument passing methods are used:

1. `s1` and `s2` (string parameters): This is **call-by-reference**. Arrays in C are passed as pointers to their first elements, allowing the function to modify the original array contents.

2. `n` (integer parameter): This is **call-by-value**. A copy of the value is created and passed to the function. Any changes to this parameter inside the function don't affect the original.

3. `&a` (integer pointer parameter): This is **call-by-reference**. The address of variable `a` is passed, allowing the function to modify the original variable.

Evidence: The function modifies both the original string `s1` and the original integer `a`, proving they are passed by reference.

### (b) Output of Function with Pointers

**Given Code:**
```c
int fun(int *a, int *b){
    if (*a > 1)  
        return *a + *b;
    else  
        return *b - *a;
}

int main(void) {
    int x = -10;  
    int y = 20;  
    printf("The result is %d", fun(&x, &y));
}
```

**Analysis:**

1. `x = -10`, `y = 20`
2. Call `fun(&x, &y)` with pointers to x and y
3. Inside `fun`, `*a = -10` and `*b = 20`
4. Check `if (*a > 1)`, which is false since -10 is not greater than 1
5. Execute `else` branch: `return *b - *a` = 20 - (-10) = 30

**Output:**
```
The result is 30
```

## Question 5

### (a) Array Manipulation with Pointers

**Write a C program that does the following:**
- Declare an array A with size 20, a pointer variable aPtr, and assign array A to aPtr
- Scan elements of array A using pointer aPtr with offset
- Write a swap function to swap any 2 values using pointers
- Call swap function to swap A[5] and A[11]

```c
#include <stdio.h>

// Function to swap two values using pointers
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int A[20];  // Declare array with size 20
    int *aPtr;  // Declare pointer variable
    
    aPtr = A;   // Assign array A to pointer aPtr
    
    // Scan elements of array using pointer with offset
    printf("Enter 20 integers:\n");
    for (int i = 0; i < 20; i++) {
        printf("Element %d: ", i);
        scanf("%d", aPtr + i);  // Using pointer offset
    }
    
    // Display original array
    printf("\nOriginal array:\n");
    for (int i = 0; i < 20; i++) {
        printf("%d ", *(aPtr + i));
    }
    
    // Swap elements A[5] and A[11]
    swap(aPtr + 5, aPtr + 11);
    
    // Display array after swapping
    printf("\n\nArray after swapping A[5] and A[11]:\n");
    for (int i = 0; i < 20; i++) {
        printf("%d ", *(aPtr + i));
    }
    
    return 0;
}
```

### (b) File Handling Questions

**Questions about the file "students.dat" containing student names and CGPAs:**

#### i. Difference between read, write, and append modes

**Read Mode ("r"):**
- Opens a file for reading only
- Requires the file to exist; returns NULL if file doesn't exist
- File pointer positioned at the beginning of the file
- Cannot modify or write to the file

**Write Mode ("w"):**
- Opens a file for writing only
- Creates a new file if it doesn't exist; truncates file to zero length if it exists
- File pointer positioned at the beginning of the file
- Overwrites any existing content

**Append Mode ("a"):**
- Opens a file for writing only
- Creates a new file if it doesn't exist; preserves content if it exists
- File pointer positioned at the end of the file
- Adds new content to the end of the file, preserving existing content

#### ii. Which mode to open the file and what happens if it doesn't exist

To add new student information to an existing file that already has 5 students, you should use **Append Mode ("a")** to preserve the existing content and add new records at the end.

If the file doesn't exist when opened in append mode, the C library will create a new file. This is different from read mode, which would return a NULL pointer if the file doesn't exist.

#### iii. C program to open, modify, and close the file

```c
#include <stdio.h>

int main() {
    FILE *file;
    char name[50];
    float cgpa;
    
    // Open file in append mode
    file = fopen("students.dat", "a");
    
    // Check if file opened successfully
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    
    // Ask how many students to add
    int numStudents;
    printf("Enter number of students to add: ");
    scanf("%d", &numStudents);
    
    // Add new student information
    for (int i = 0; i < numStudents; i++) {
        printf("\nEnter details for Student %d:\n", i+1);
        
        printf("Name: ");
        scanf(" %[^\n]s", name);
        
        printf("CGPA: ");
        scanf("%f", &cgpa);
        
        // Write to file
        fprintf(file, "%s %.2f\n", name, cgpa);
    }
    
    // Close the file
    fclose(file);
    
    // Reopen to read and display all students
    file = fopen("students.dat", "r");
    
    if (file == NULL) {
        printf("Error opening file for reading!\n");
        return 1;
    }
    
    // Display all student information
    printf("\nAll Students in the file:\n");
    printf("------------------------------------------\n");
    printf("%-30s %s\n", "Name", "CGPA");
    printf("------------------------------------------\n");
    
    while (fscanf(file, "%[^0-9] %f\n", name, &cgpa) == 2) {
        printf("%-30s %.2f\n", name, cgpa);
    }
    
    // Close the file again
    fclose(file);
    
    printf("Operation completed successfully.\n");
    
    return 0;
}
```

**Explanation:**
1. We open the file "students.dat" in append mode to add new records without affecting existing ones
2. We check if the file opened successfully
3. We input the number of students to add
4. For each new student, we input name and CGPA, then write them to the file
5. We close the file to ensure all data is saved
6. We reopen the file in read mode to display all student information
7. We read and display all students from the file
8. Finally, we close the file again


# Theory Questions and Solutions - Set 4

## Question 1

### (a) Factorial and Sum Functions

**Write a C program according to the following requirements:**

i. Write a function `int factorial(int n)` that will return the factorial of a given number. Factorial of a number can be calculated by multiplying the numbers from 1 to n consecutively. For example, factorial of 4 = 1×2×3×4 = 24. Assume n will not be greater than 10.
ii. Write a function `int sum(int a, int b)` that will return the sum of two given numbers.
iii. In the main function, take three integers as inputs and calculate the sum of the factorial of those integers using the above functions factorial() and sum().

**Solution:**

```c
#include <stdio.h>

// Function to calculate factorial of a number
int factorial(int n) {
    int result = 1;
    
    // Multiply numbers from 1 to n
    for (int i = 1; i <= n; i++) {
        result *= i;
    }
    
    return result;
}

// Function to calculate sum of two numbers
int sum(int a, int b) {
    return a + b;
}

int main() {
    int num1, num2, num3;
    
    // Input three integers
    printf("Enter three integers (0-10): ");
    scanf("%d %d %d", &num1, &num2, &num3);
    
    // Validate input values
    if (num1 < 0 || num1 > 10 || num2 < 0 || num2 > 10 || num3 < 0 || num3 > 10) {
        printf("Please enter values between 0 and 10.\n");
        return 1;
    }
    
    // Calculate factorial of each number
    int fact1 = factorial(num1);
    int fact2 = factorial(num2);
    int fact3 = factorial(num3);
    
    // Calculate sum of the factorials
    // We need to use sum() function twice since it only takes two arguments
    int result = sum(sum(fact1, fact2), fact3);
    
    // Display results
    printf("Factorial of %d = %d\n", num1, fact1);
    printf("Factorial of %d = %d\n", num2, fact2);
    printf("Factorial of %d = %d\n", num3, fact3);
    printf("Sum of factorials = %d\n", result);
    
    return 0;
}
```

**Explanation:**
1. We implement the `factorial()` function to calculate n! by multiplying numbers from 1 to n.
2. We implement the `sum()` function to return the sum of two numbers.
3. In the main function, we take three integers as input and calculate their factorials.
4. We calculate the sum of the factorials using the `sum()` function, applying it twice since it only takes two arguments at a time.
5. Finally, we display the factorials and their sum.

### (b) Code Tracing with Global Variables

**Find the output of the following program:**

```c
#include<stdio.h> 
int x = 2, y = 3; 
int fun1(int n){ 
    return n%11; 
} 
void fun2(int arr[], int n){ 
    for(int i = 0; i<n; i++){ 
        x = fun1(x) + fun1(y); 
        arr[i] = arr[i] + x; 
        y = fun1(y) + fun1(x); 
    } 
} 
int main(){ 
    int a[] = {2, 3, 5, 7, 11}; 
    fun2(a, 5); 
    for(int i = 0; i<5; i++) 
        printf("%d ", a[i]); 
} 
```

**Step-by-step Trace:**

Initial values:
- Global variables: `x = 2, y = 3`
- Array: `a = {2, 3, 5, 7, 11}`

Let's trace the execution of `fun2(a, 5)`:

**Iteration 1 (i = 0):**
- `fun1(x) = fun1(2) = 2%11 = 2`
- `fun1(y) = fun1(3) = 3%11 = 3`
- `x = 2 + 3 = 5`
- `arr[0] = a[0] + x = 2 + 5 = 7`
- `fun1(y) = fun1(3) = 3%11 = 3`
- `fun1(x) = fun1(5) = 5%11 = 5`
- `y = 3 + 5 = 8`

**Iteration 2 (i = 1):**
- `fun1(x) = fun1(5) = 5%11 = 5`
- `fun1(y) = fun1(8) = 8%11 = 8`
- `x = 5 + 8 = 13`
- `arr[1] = a[1] + x = 3 + 13 = 16`
- `fun1(y) = fun1(8) = 8%11 = 8`
- `fun1(x) = fun1(13) = 13%11 = 2`
- `y = 8 + 2 = 10`

**Iteration 3 (i = 2):**
- `fun1(x) = fun1(13) = 13%11 = 2`
- `fun1(y) = fun1(10) = 10%11 = 10`
- `x = 2 + 10 = 12`
- `arr[2] = a[2] + x = 5 + 12 = 17`
- `fun1(y) = fun1(10) = 10%11 = 10`
- `fun1(x) = fun1(12) = 12%11 = 1`
- `y = 10 + 1 = 11`

**Iteration 4 (i = 3):**
- `fun1(x) = fun1(12) = 12%11 = 1`
- `fun1(y) = fun1(11) = 11%11 = 0`
- `x = 1 + 0 = 1`
- `arr[3] = a[3] + x = 7 + 1 = 8`
- `fun1(y) = fun1(11) = 11%11 = 0`
- `fun1(x) = fun1(1) = 1%11 = 1`
- `y = 0 + 1 = 1`

**Iteration 5 (i = 4):**
- `fun1(x) = fun1(1) = 1%11 = 1`
- `fun1(y) = fun1(1) = 1%11 = 1`
- `x = 1 + 1 = 2`
- `arr[4] = a[4] + x = 11 + 2 = 13`
- `fun1(y) = fun1(1) = 1%11 = 1`
- `fun1(x) = fun1(2) = 2%11 = 2`
- `y = 1 + 2 = 3`

Final array values:
- `a = {7, 16, 17, 8, 13}`

**Output:**
```
7 16 17 8 13
```

## Question 2

### (a) String Manipulation Tracing

**Show manual tracing of the following program:**

```c
#include <stdio.h> 
#include <string.h> 
 
int main() { 
     char A[101] = {'\0'}; 
     char B[101] = "string"; 
      
     strncpy(A, B, 4); 
     strncat(A, "kernel", 3); 
      
     for(int i=0; B[i]!='\0'; i++) { 
         if(B[i]=='i') { 
             B[i] = '\0'; 
         } 
     } 
     printf("%s - %s\n", A, B); 
     return 0; 
} 
```

**Manual Tracing:**

| Step | Operation | A | B | i | Explanation |
|------|-----------|---|---|----|-------------|
| 1 | Initialize | "\0" (empty) | "string" | - | Initial values |
| 2 | `strncpy(A, B, 4)` | "stri" | "string" | - | Copy first 4 chars from B to A |
| 3 | `strncat(A, "kernel", 3)` | "striker" | "string" | - | Append first 3 chars of "kernel" to A |
| 4 | Loop starts | "striker" | "string" | 0 | Start loop to check each char in B |
| 5 | Check B[0]='s'=='i'? | "striker" | "string" | 0 | False, continue |
| 6 | Check B[1]='t'=='i'? | "striker" | "string" | 1 | False, continue |
| 7 | Check B[2]='r'=='i'? | "striker" | "string" | 2 | False, continue |
| 8 | Check B[3]='i'=='i'? | "striker" | "str\0ng" | 3 | True, set B[3]='\0' |
| 9 | Loop ends | "striker" | "str" | - | B is now truncated at position 3 |

**Final values:**
- A: "striker"
- B: "str"

**Output:**
```
striker - str
```

### (b) String Search and Replace

**Consider the following string declaration:**
```c
char str[55]="I love spl. Uiu has some good labs for spl.";
```

**Write a C program that will replace each occurrence of the word "spl" with "dsa" and print out the resulting text. You cannot use any library functions.**

```c
#include <stdio.h>

// Function to calculate length of a string
int myStrlen(char s[]) {
    int length = 0;
    while (s[length] != '\0') {
        length++;
    }
    return length;
}

// Function to check if substring at position matches the target
int isMatch(char str[], int pos, char target[]) {
    int i = 0;
    while (target[i] != '\0') {
        if (str[pos + i] != target[i]) {
            return 0;  // Not a match
        }
        i++;
    }
    return 1;  // Match found
}

// Function to replace a substring with another
void replaceSubstring(char str[], char find[], char replace[]) {
    int strLen = myStrlen(str);
    int findLen = myStrlen(find);
    int replaceLen = myStrlen(replace);
    
    // If lengths are different, we need to shift characters
    int lenDiff = replaceLen - findLen;
    
    for (int i = 0; i < strLen; i++) {
        // Check if we found the substring
        if (isMatch(str, i, find)) {
            // If replacement is longer than original
            if (lenDiff > 0) {
                // Shift characters to the right to make space
                for (int j = strLen; j >= i + findLen; j--) {
                    str[j + lenDiff] = str[j];
                }
            }
            // If replacement is shorter than original
            else if (lenDiff < 0) {
                // Shift characters to the left to close gap
                for (int j = i + findLen; j <= strLen; j++) {
                    str[j + lenDiff] = str[j];
                }
            }
            
            // Copy the replacement string
            for (int j = 0; j < replaceLen; j++) {
                str[i + j] = replace[j];
            }
            
            // Update string length and current position
            strLen += lenDiff;
            i += replaceLen - 1;  // -1 because the loop will increment i
        }
    }
}

int main() {
    char str[55] = "I love spl. Uiu has some good labs for spl.";
    char find[] = "spl";
    char replace[] = "dsa";
    
    printf("Original: %s\n", str);
    
    replaceSubstring(str, find, replace);
    
    printf("Modified: %s\n", str);
    
    return 0;
}
```

**Output:**
```
Original: I love spl. Uiu has some good labs for spl.
Modified: I love dsa. Uiu has some good labs for dsa.
```

## Question 3

### (a) Structure Code Error Correction

**Identify and correct the errors in the following code:**

```c
struct student{ 
   char name[]; 
   int ID; 
} 
int main() { 
   student s1,s2; 
   s1.name="Rahim"; 
   s1.ID=101;     
   struct student* s_ptr = s2; 
   scanf("%s",&s_ptr.name); 
   scanf("%d",&s_ptr.ID); 
}
```

**Corrected Code:**

```c
#include <stdio.h>
#include <string.h>  // For strcpy

struct student{ 
   char name[50];   // Missing array size, added 50
   int ID; 
};  // Missing semicolon, added

int main() { 
   struct student s1, s2;  // Missing 'struct' keyword, added
   
   // Cannot assign string literal directly to array
   strcpy(s1.name, "Rahim");  // Used strcpy
   
   s1.ID = 101;     
   
   struct student* s_ptr = &s2;  // Missing & operator, added
   
   printf("Enter name: ");
   scanf("%s", s_ptr->name);  // Changed . to -> for pointer and removed & from array name
   
   printf("Enter ID: ");
   scanf("%d", &s_ptr->ID);  // Changed . to -> for pointer
   
   // Added print to verify
   printf("Student 1: %s, ID: %d\n", s1.name, s1.ID);
   printf("Student 2: %s, ID: %d\n", s2.name, s2.ID);
   
   return 0;  // Added return statement
}
```

**Errors Identified and Corrected:**
1. Missing array size for `name[]` (should specify size like `name[50]`)
2. Missing semicolon after structure definition
3. Missing `struct` keyword when declaring variables of type `student`
4. Direct string assignment to array (replaced with `strcpy()`)
5. Missing address operator (`&`) for the pointer assignment (`s_ptr = &s2`)
6. Incorrect pointer notation (used `s_ptr->name` instead of `s_ptr.name`)
7. Incorrect usage of `&` with `s_ptr.name` (arrays already decay to pointers)
8. Missing return statement

### (b) Patient Information Management

**Write a C program to store patient information and perform the following operations:**

i. Create a structure named Patient with members: name, age, height, weight, and BMI.
ii. Declare an array of size 100 of type Patient structures.
iii. Take inputs and calculate the BMI using the formula: weight / (height).
iv. Find and display all the information of the youngest patient with lowest age.

```c
#include <stdio.h>
#include <string.h>

// Structure definition for Patient
struct Patient {
    char name[50];
    int age;
    float height;
    float weight;
    float BMI;
};

int main() {
    // Declare array of 100 Patient structures
    struct Patient patients[100];
    int numPatients;
    
    // Input number of patients
    printf("Enter number of patients (max 100): ");
    scanf("%d", &numPatients);
    
    if (numPatients <= 0 || numPatients > 100) {
        printf("Invalid number of patients. Please enter between 1 and 100.\n");
        return 1;
    }
    
    // Input patient information
    for (int i = 0; i < numPatients; i++) {
        printf("\nEnter details for Patient %d:\n", i+1);
        
        printf("Name: ");
        scanf(" %[^\n]s", patients[i].name);
        
        printf("Age: ");
        scanf("%d", &patients[i].age);
        
        printf("Height (in meters): ");
        scanf("%f", &patients[i].height);
        
        printf("Weight (in kg): ");
        scanf("%f", &patients[i].weight);
        
        // Calculate BMI
        patients[i].BMI = patients[i].weight / (patients[i].height * patients[i].height);
    }
    
    // Find youngest patient
    int youngestIndex = 0;
    for (int i = 1; i < numPatients; i++) {
        if (patients[i].age < patients[youngestIndex].age) {
            youngestIndex = i;
        }
    }
    
    // Display information of youngest patient
    printf("\nYoungest Patient Information:\n");
    printf("Name: %s\n", patients[youngestIndex].name);
    printf("Age: %d\n", patients[youngestIndex].age);
    printf("Height: %.2f meters\n", patients[youngestIndex].height);
    printf("Weight: %.2f kg\n", patients[youngestIndex].weight);
    printf("BMI: %.2f\n", patients[youngestIndex].BMI);
    
    return 0;
}
```

**Note:** In the problem statement, the BMI formula is given as weight / (height), but the standard BMI formula is weight / (height * height). I've used the standard formula in the solution.

## Question 4

### (a) Pointer Array Operations

**Write a C program that does the following:**
- Declare an integer array arr with array size 100
- Declare a pointer variable arrPtr and assign the array arr to it
- Scan the elements of the array arr using the pointer arrPtr with offset
- Find and print the largest element of arr using the pointer arrPtr

```c
#include <stdio.h>

int main() {
    int arr[100];  // Declare array with size 100
    int *arrPtr;   // Declare pointer variable
    int n;         // Number of elements
    
    arrPtr = arr;  // Assign array to pointer
    
    // Input number of elements
    printf("Enter number of elements (max 100): ");
    scanf("%d", &n);
    
    if (n <= 0 || n > 100) {
        printf("Invalid number of elements. Please enter between 1 and 100.\n");
        return 1;
    }
    
    // Input array elements using pointer with offset
    printf("Enter %d integers:\n", n);
    for (int i = 0; i < n; i++) {
        printf("Element %d: ", i+1);
        scanf("%d", arrPtr + i);  // Using pointer arithmetic
    }
    
    // Find largest element using pointer
    int largest = *arrPtr;  // Initialize with first element
    
    for (int i = 1; i < n; i++) {
        if (*(arrPtr + i) > largest) {
            largest = *(arrPtr + i);
        }
    }
    
    // Display array elements
    printf("\nArray elements: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", *(arrPtr + i));
    }
    
    // Display largest element
    printf("\nLargest element: %d\n", largest);
    
    return 0;
}
```

### (b) Pointer Function Tracing

**Find the output of the following code:**

```c
#include <stdio.h> 
void inc(int *ap, int dummy){ 
    for(int i=0; i<dummy; i++){ 
        *ap = *ap + 1; 
        ap = ap + 2; 
    } 
    dummy = 100; 
} 
int main() { 
    int a[] = {1,2,3,4,5,6,7,8}; 
    int dummy = 3; 
    inc(&a[2], dummy); 
    for(int i=0; i<8; i++)   
        printf("%d ",a[i]); 
    printf("\nDummy=%d\n", dummy); 
    return 0; 
} 
```

**Step-by-step Trace:**

1. In `main()`, we have array `a = {1,2,3,4,5,6,7,8}` and `dummy = 3`
2. We call `inc(&a[2], dummy)`, passing the address of `a[2]` (which is 3) and value of `dummy`
3. Inside `inc()`, we loop `dummy` times (3 iterations)

**Iteration 1:**
- `*ap = *ap + 1`: Increments the value at `a[2]` from 3 to 4
- `ap = ap + 2`: Moves pointer to `a[4]`

**Iteration 2:**
- `*ap = *ap + 1`: Increments the value at `a[4]` from 5 to 6
- `ap = ap + 2`: Moves pointer to `a[6]`

**Iteration 3:**
- `*ap = *ap + 1`: Increments the value at `a[6]` from 7 to 8
- `ap = ap + 2`: Moves pointer to `a[8]` (out of bounds)

4. `dummy = 100`: This change is local to the function and doesn't affect the value in `main()`
5. Return to `main()` and print array values: `1 2 4 4 6 6 8 8`
6. Print value of `dummy` in `main()`, which is still 3

**Output:**
```
1 2 4 4 6 6 8 8 
Dummy=3
```

## Question 5

### (a) Recursive Function Tracing

**Write the output of the following program:**

```c
#include <stdio.h> 
int power_of_2(int n) { 
    printf("Inside power_of_2(%d)\n", n); 
    if(n == 1) return 1; 
    if(n % 2 != 0) return 0; 
    return power_of_2(n / 2); 
} 
int main(void){ 
    int num = 16; 
    power_of_2(num); 
    return 0; 
} 
```

**Step-by-step Trace:**

1. Call `power_of_2(16)`
   - Print: `Inside power_of_2(16)`
   - `16 == 1`? No
   - `16 % 2 != 0`? No
   - Call `power_of_2(16 / 2)` = `power_of_2(8)`

2. Call `power_of_2(8)`
   - Print: `Inside power_of_2(8)`
   - `8 == 1`? No
   - `8 % 2 != 0`? No
   - Call `power_of_2(8 / 2)` = `power_of_2(4)`

3. Call `power_of_2(4)`
   - Print: `Inside power_of_2(4)`
   - `4 == 1`? No
   - `4 % 2 != 0`? No
   - Call `power_of_2(4 / 2)` = `power_of_2(2)`

4. Call `power_of_2(2)`
   - Print: `Inside power_of_2(2)`
   - `2 == 1`? No
   - `2 % 2 != 0`? No
   - Call `power_of_2(2 / 2)` = `power_of_2(1)`

5. Call `power_of_2(1)`
   - Print: `Inside power_of_2(1)`
   - `1 == 1`? Yes
   - Return 1

6. The returned value 1 propagates back through all the recursive calls, but the program doesn't print it

**Output:**
```
Inside power_of_2(16)
Inside power_of_2(8)
Inside power_of_2(4)
Inside power_of_2(2)
Inside power_of_2(1)
```

### (b) File Handling Questions

**Questions about file handling:**

i. **What will happen if the file does not exist?**

For the code:
```c
FILE *fp = fopen("string.txt", "w");
fprintf(fp, "Yet another string\n");
fclose(fp);
```

If the file "string.txt" does not exist when opened in "w" (write) mode:
- A new file with the name "string.txt" will be created
- The content "Yet another string\n" will be written to the newly created file
- The file will be closed properly with `fclose(fp)`

ii. **What is the difference between read and append mode?**

**Read Mode ("r"):**
- Opens an existing file for reading only
- File pointer is positioned at the beginning of the file
- File must exist; if it doesn't, `fopen()` returns NULL
- Cannot modify the file's contents

**Append Mode ("a"):**
- Opens a file for writing only
- File pointer is positioned at the end of the file
- Creates the file if it doesn't exist
- All new data is added to the end of the file, preserving existing content
- Cannot read from the file or modify existing content

iii. **Write C code segment to re-open the same file in append mode and add a new string**

```c
#include <stdio.h>

int main() {
    // First open in write mode
    FILE *fp = fopen("string.txt", "w");
    if (fp == NULL) {
        printf("Error opening file in write mode!\n");
        return 1;
    }
    fprintf(fp, "Yet another string\n");
    fclose(fp);
    
    // Re-open in append mode
    fp = fopen("string.txt", "a");
    if (fp == NULL) {
        printf("Error opening file in append mode!\n");
        return 1;
    }
    fprintf(fp, "This is another string\n");
    fclose(fp);
    
    // Verify file contents by reading
    printf("File contents:\n");
    fp = fopen("string.txt", "r");
    if (fp == NULL) {
        printf("Error opening file for reading!\n");
        return 1;
    }
    char buffer[100];
    while (fgets(buffer, sizeof(buffer), fp) != NULL) {
        printf("%s", buffer);
    }
    fclose(fp);
    
    return 0;
}
```

**Expected Output:**
```
File contents:
Yet another string
This is another string
```


# Theory Questions and Solutions - Set 6

## Question 1

### (a) Bank Account Balance Management

**Implement a function updateBalance that takes four parameters: an array of floats representing customer balances, an integer representing the customer's unique identifier (which is the index of the array), an integer representing the type of transaction (1 for withdrawal, 2 for deposit), and a float representing the transaction amount. The function should update the customer's balance based on the transaction type, ensuring that withdrawals do not result in a negative balance.**

i) In the main function, initialize an array of floats to store the initial balances of 100 customers. Take the initial balances from user as input.

ii) Take three values: an integer (customer identifier), an integer (transaction type), and a float (transaction amount) from user.

iii) Call the updateBalance function passing these values. If the transaction is a withdrawal and the withdrawal amount is exceeding the available balance then print "Not sufficient balance" and do not activate the withdrawal.

iv) If transaction is successful in step (iii), print the updated balance of the customer.

**Solution:**

```c
#include <stdio.h>

// Function to update customer balance
void updateBalance(float balances[], int customerID, int transactionType, float amount) {
    // Check if transaction is withdrawal
    if (transactionType == 1) {
        // Check if sufficient balance available
        if (balances[customerID] >= amount) {
            balances[customerID] -= amount;
        } else {
            printf("Not sufficient balance\n");
            return;
        }
    }
    // Check if transaction is deposit
    else if (transactionType == 2) {
        balances[customerID] += amount;
    }
}

int main() {
    float balances[100];
    int customerID, transactionType;
    float amount;
    
    // Take initial balances as input
    printf("Enter initial balances for 100 customers:\n");
    for (int i = 0; i < 100; i++) {
        printf("Customer %d: ", i);
        scanf("%f", &balances[i]);
    }
    
    // Take transaction details as input
    printf("\nEnter customer ID (0-99): ");
    scanf("%d", &customerID);
    
    if (customerID < 0 || customerID >= 100) {
        printf("Invalid customer ID. Must be between 0 and 99.\n");
        return 1;
    }
    
    printf("Enter transaction type (1 for withdrawal, 2 for deposit): ");
    scanf("%d", &transactionType);
    
    if (transactionType != 1 && transactionType != 2) {
        printf("Invalid transaction type. Must be 1 or 2.\n");
        return 1;
    }
    
    printf("Enter amount: ");
    scanf("%f", &amount);
    
    if (amount <= 0) {
        printf("Invalid amount. Must be greater than 0.\n");
        return 1;
    }
    
    // Store initial balance for comparison
    float initialBalance = balances[customerID];
    
    // Update balance
    updateBalance(balances, customerID, transactionType, amount);
    
    // Check if transaction was successful
    if (balances[customerID] != initialBalance) {
        printf("Transaction successful!\n");
        printf("Updated balance for customer %d: %.2f\n", customerID, balances[customerID]);
    }
    
    return 0;
}
```

### (b) Find the output of the following program. Notice the local and global contexts.

```c
#include <stdio.h> 
int ara[5], x = 20; 
void change(int p) { 
   --p; 
   p--; 
} 
void update(int n) { 
   for(int i = n - 1; i >= 0; i--){ 
     ara[i] -= x; 
     change(x); 
   } 
} 
void main() { 
    int n = 5; 
    for(int i = 0; i < n; i++){ 
     ara[i] = (i + 5) * 2; 
    } 
    update(n); 
    for(int i = 0; i < n; i++){ 
     printf("%d, ", ara[i]); 
    } 
} 
```

**Step-by-step Trace:**

1. Initialize global array `ara[5]` and global variable `x = 20`
2. In `main()`:
   - Set `n = 5`
   - Initialize array elements:
     - `ara[0] = (0 + 5) * 2 = 10`
     - `ara[1] = (1 + 5) * 2 = 12`
     - `ara[2] = (2 + 5) * 2 = 14`
     - `ara[3] = (3 + 5) * 2 = 16`
     - `ara[4] = (4 + 5) * 2 = 18`
   - Call `update(5)`

3. In `update(5)`:
   - Loop starts with `i = 4` down to `i = 0`
   - When `i = 4`:
     - `ara[4] -= x` → `ara[4] = 18 - 20 = -2`
     - Call `change(x)` with `x = 20`
   - When `i = 3`:
     - `ara[3] -= x` → `ara[3] = 16 - 20 = -4`
     - Call `change(x)` with `x = 20`
   - When `i = 2`:
     - `ara[2] -= x` → `ara[2] = 14 - 20 = -6`
     - Call `change(x)` with `x = 20`
   - When `i = 1`:
     - `ara[1] -= x` → `ara[1] = 12 - 20 = -8`
     - Call `change(x)` with `x = 20`
   - When `i = 0`:
     - `ara[0] -= x` → `ara[0] = 10 - 20 = -10`
     - Call `change(x)` with `x = 20`

4. The `change(p)` function just decreases the local parameter `p` twice but doesn't affect the global `x`

5. Back in `main()`, print the array elements:
   - `ara[0] = -10`
   - `ara[1] = -8`
   - `ara[2] = -6`
   - `ara[3] = -4`
   - `ara[4] = -2`

**Output:**
```
-10, -8, -6, -4, -2,
```

## Question 2

### (a) Show manual tracing of the following program.

```c
#include <stdio.h> 
#include <string.h> 
int main(){ 
   char str1[50]="CSE-1111 SPL";    
   char str2[50]="I am a UIUian"; 
  
   int i=strlen(str1) * 0.5 - 2; 
 
   for(int m=0; i+m<strlen(str1); m+=3){ 
         str1[i+m]=str2[m]; 
   }    
 
   strcat(str1, str2); 
 
   if(strcmp(str2, str1)>0){ 
     strncat(str1, "CSE is awesome.",6); 
   } 
   else{ 
     strncat(str2, "CSE is awesome.",6); 
   } 
   return 0; 
} 
```

**Manual Tracing:**

| Step | Operation | i | m | str1 | str2 | Explanation |
|------|-----------|---|---|------|------|-------------|
| 1 | Initialize | - | - | "CSE-1111 SPL" | "I am a UIUian" | Initial values |
| 2 | `i=strlen(str1) * 0.5 - 2` | 3 | - | "CSE-1111 SPL" | "I am a UIUian" | `strlen(str1)` = 12, `12 * 0.5 - 2 = 4` |
| 3 | First iteration: `m=0` | 3 | 0 | "CSE-I111 SPL" | "I am a UIUian" | `i+m=3+0=3 < 12`, replace str1[3] with str2[0] |
| 4 | Second iteration: `m=3` | 3 | 3 | "CSE-I11a SPL" | "I am a UIUian" | `i+m=3+3=6 < 12`, replace str1[6] with str2[3] |
| 5 | Third iteration: `m=6` | 3 | 6 | "CSE-I11a UPL" | "I am a UIUian" | `i+m=3+6=9 < 12`, replace str1[9] with str2[6] |
| 6 | Fourth iteration: `m=9` | 3 | 9 | "CSE-I11a UPI" | "I am a UIUian" | `i+m=3+9=12 = 12`, loop ends |
| 7 | `strcat(str1, str2)` | 3 | 9 | "CSE-I11a UPIi am a UIUian" | "I am a UIUian" | Concatenate str2 to end of str1 |
| 8 | `strcmp(str2, str1)>0` | 3 | 9 | "CSE-I11a UPIi am a UIUian" | "I am a UIUian" | Compare: "I" comes after "C", so result > 0 |
| 9 | `strncat(str1, "CSE is awesome.", 6)` | 3 | 9 | "CSE-I11a UPIi am a UIUianCSE is" | "I am a UIUian" | Add first 6 chars of "CSE is awesome." to str1 |

**Final Values:**
- str1: "CSE-I11a UPIi am a UIUianCSE is"
- str2: "I am a UIUian"

### (b) Vowel Counter Program

**Write a C program that takes a string from the keyboard. The program will count (case insensitively) the number of different vowels and display the statistics as shown below.**

**Sample Input:**
```
Owls fly high above the clouds.
```

**Sample Output:**
```
A/a: 1
E/e: 2
I/i: 1
O/o: 3
U/u: 1
```

**Solution:**

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char str[100];
    int vowelCount[5] = {0}; // For a, e, i, o, u
    
    // Read input string
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    
    // Count vowels (case insensitively)
    for (int i = 0; str[i] != '\0'; i++) {
        char ch = tolower(str[i]);
        
        switch (ch) {
            case 'a':
                vowelCount[0]++;
                break;
            case 'e':
                vowelCount[1]++;
                break;
            case 'i':
                vowelCount[2]++;
                break;
            case 'o':
                vowelCount[3]++;
                break;
            case 'u':
                vowelCount[4]++;
                break;
        }
    }
    
    // Display results
    printf("A/a: %d\n", vowelCount[0]);
    printf("E/e: %d\n", vowelCount[1]);
    printf("I/i: %d\n", vowelCount[2]);
    printf("O/o: %d\n", vowelCount[3]);
    printf("U/u: %d\n", vowelCount[4]);
    
    return 0;
}
```

## Question 3

**Suppose you're developing a program for the United International University (UIU) Bookshop to manage customer purchases. Your task is to create a C program that can store, manage and manipulate the bookshop's last 12 months' customer data. As it is the end of the year, the bookshop is giving a "best customer award" to the customers who purchased the most in the past year. Write a C program that will:**

**1. Store the following information of a customer in a structure.
(i) Name (ii) ID (iii) Number of times shopped, and (iv) An array of spent money in each of the shoppings. Use appropriate data types and variable names for all the features.**

**2. Take input for 100 customers from the user.**

**3. Calculate the average purchase for each customer (total money spent divided by the total number of shopping).**

**4. To find the best customer, only consider the customers who have shopped more than 10 times. Among these selected customers, the customer having the best average purchase (calculated from (3)) will win the award. Print the customer's name who has won the award.**

**Solution:**

```c
#include <stdio.h>
#include <string.h>

#define MAX_CUSTOMERS 100
#define MAX_SHOPPINGS 50
#define MIN_SHOPPING_THRESHOLD 10

// Structure to store customer information
struct Customer {
    char name[50];
    int id;
    int timesShoppped;
    float spentMoney[MAX_SHOPPINGS];
    float averagePurchase;
};

int main() {
    struct Customer customers[MAX_CUSTOMERS];
    int i, j;
    float totalSpent;
    int bestCustomerIndex = -1;
    float highestAverage = 0.0;
    
    // Input customer data
    printf("Enter data for %d customers:\n", MAX_CUSTOMERS);
    for (i = 0; i < MAX_CUSTOMERS; i++) {
        printf("\nCustomer %d:\n", i + 1);
        
        printf("Name: ");
        scanf("%s", customers[i].name);
        
        printf("ID: ");
        scanf("%d", &customers[i].id);
        
        printf("Number of times shopped: ");
        scanf("%d", &customers[i].timesShoppped);
        
        if (customers[i].timesShoppped > 0) {
            printf("Enter amount spent in each shopping:\n");
            totalSpent = 0.0;
            
            for (j = 0; j < customers[i].timesShoppped; j++) {
                printf("Shopping %d: ", j + 1);
                scanf("%f", &customers[i].spentMoney[j]);
                totalSpent += customers[i].spentMoney[j];
            }
            
            // Calculate average purchase
            customers[i].averagePurchase = totalSpent / customers[i].timesShoppped;
        } else {
            customers[i].averagePurchase = 0.0;
        }
    }
    
    // Find the best customer
    for (i = 0; i < MAX_CUSTOMERS; i++) {
        if (customers[i].timesShoppped > MIN_SHOPPING_THRESHOLD) {
            if (customers[i].averagePurchase > highestAverage) {
                highestAverage = customers[i].averagePurchase;
                bestCustomerIndex = i;
            }
        }
    }
    
    // Print the best customer
    if (bestCustomerIndex != -1) {
        printf("\nBest Customer Award goes to: %s\n", customers[bestCustomerIndex].name);
        printf("Average Purchase: %.2f\n", customers[bestCustomerIndex].averagePurchase);
    } else {
        printf("\nNo customer has shopped more than %d times.\n", MIN_SHOPPING_THRESHOLD);
    }
    
    return 0;
}
```

## Question 4

### (a) Pointer Value Modification

**Write a C program that does the following:**
• Declare an integer variable num and initialize it with any value.
• Declare a pointer variable and assign the address of num to it.
• Use the pointer to double the value of num.
• Print the value of num both before and after the modification.

**Solution:**

```c
#include <stdio.h>

int main() {
    // Declare an integer variable and initialize it
    int num = 10;
    
    // Declare a pointer variable and assign address of num to it
    int *ptr = &num;
    
    // Print the value before modification
    printf("Value of num before modification: %d\n", num);
    
    // Use the pointer to double the value of num
    *ptr = *ptr * 2;
    
    // Print the value after modification
    printf("Value of num after modification: %d\n", num);
    
    return 0;
}
```

### (b) Find the output of the code.

```c
#include <stdio.h> 
void modifyArray(int arr[], int size){
    for (int i = 0; i < size; i++){
        arr[i] *= 2;
    }
}
void main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int *ptr = numbers;
    modifyArray(ptr, 5);
    for(int i = 0; i < 5; i++){
        *(ptr+i) = *(ptr+i) + i;
        printf("%d ", *(ptr+i));
    }
}
```

**Step-by-step Trace:**

1. Initialize `numbers[]` with values `{1, 2, 3, 4, 5}`
2. Set `ptr` to point to the start of `numbers[]`
3. Call `modifyArray(ptr, 5)`
   - Inside `modifyArray`, multiply each element by 2
   - After the function, `numbers[]` becomes `{2, 4, 6, 8, 10}`
4. Loop through and add the index to each element:
   - `i=0`: `*(ptr+0) = *(ptr+0) + 0 = 2 + 0 = 2`, print `2`
   - `i=1`: `*(ptr+1) = *(ptr+1) + 1 = 4 + 1 = 5`, print `5`
   - `i=2`: `*(ptr+2) = *(ptr+2) + 2 = 6 + 2 = 8`, print `8`
   - `i=3`: `*(ptr+3) = *(ptr+3) + 3 = 8 + 3 = 11`, print `11`
   - `i=4`: `*(ptr+4) = *(ptr+4) + 4 = 10 + 4 = 14`, print `14`

**Output:**
```
2 5 8 11 14
```

## Question 5

### (a) Write the output of the program.

```c
#include <stdio.h> 
void go(int num){
    printf("How are you?\n");
    if(num==0){
        return;
    }
    num /= 10;
    go(num);
    printf("I am fine\n");
}
int main(void){
    int num = 45633;
    go(num);
    return 0;
}
```

**Step-by-step Trace:**

1. Call `go(45633)`
   - Print: "How are you?"
   - `num != 0`, so continue
   - `num /= 10` → `num = 4563`
   - Call `go(4563)`
     - Print: "How are you?"
     - `num != 0`, so continue
     - `num /= 10` → `num = 456`
     - Call `go(456)`
       - Print: "How are you?"
       - `num != 0`, so continue
       - `num /= 10` → `num = 45`
       - Call `go(45)`
         - Print: "How are you?"
         - `num != 0`, so continue
         - `num /= 10` → `num = 4`
         - Call `go(4)`
           - Print: "How are you?"
           - `num != 0`, so continue
           - `num /= 10` → `num = 0`
           - Call `go(0)`
             - Print: "How are you?"
             - `num == 0`, so return
           - Print: "I am fine"
         - Print: "I am fine"
       - Print: "I am fine"
     - Print: "I am fine"
   - Print: "I am fine"

**Output:**
```
How are you?
How are you?
How are you?
How are you?
How are you?
How are you?
I am fine
I am fine
I am fine
I am fine
I am fine
```

### (b) File I/O Program

**Write a C program that performs the following tasks:**
1) Read the following "in.txt" file that has integer numbers on separate lines. Find the maximum value of those numbers.
2) Create a new file "out.txt" and print the maximum number into the new file.
3) Remember to display appropriate messages if the input or the output file couldn't be opened.

**Solution:**

```c
#include <stdio.h>

int main() {
    FILE *inputFile, *outputFile;
    int num, max = -2147483648; // Initialize to minimum integer value
    
    // Open input file
    inputFile = fopen("in.txt", "r");
    
    // Check if file opened successfully
    if (inputFile == NULL) {
        printf("Error: Could not open input file 'in.txt'\n");
        return 1;
    }
    
    // Read numbers and find maximum
    while (fscanf(inputFile, "%d", &num) == 1) {
        if (num > max) {
            max = num;
        }
    }
    
    // Close input file
    fclose(inputFile);
    
    // Open output file
    outputFile = fopen("out.txt", "w");
    
    // Check if file opened successfully
    if (outputFile == NULL) {
        printf("Error: Could not create output file 'out.txt'\n");
        return 1;
    }
    
    // Write maximum to output file
    fprintf(outputFile, "%d", max);
    
    // Close output file
    fclose(outputFile);
    
    printf("Maximum value %d has been written to 'out.txt'\n", max);
    
    return 0;
}
```
