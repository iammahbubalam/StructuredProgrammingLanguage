# Easy Problems Solutions (40 Problems)

This document contains solutions to all 40 easy problems with detailed explanations and problem-solving approaches to help students develop their programming thinking skills.

## Problem E1: Hello, World!

**Approach:** Start with the most basic program structure in C.
**Thinking:** Every C program needs a main function and printf to display output.

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

**Explanation:** This is the traditional first program. It demonstrates the basic structure of a C program: including headers, main function, and output using printf. The \n creates a new line after the text.

---

## Problem E2: Sum of Two Numbers

**Approach:** Read two numbers from user input and calculate their sum.
**Thinking:** Use scanf for input, variables to store values, and printf for output.

```c
#include <stdio.h>

int main() {
    int num1, num2, sum;
    
    printf("Enter two numbers: ");
    scanf("%d %d", &num1, &num2);
    
    sum = num1 + num2;
    printf("Sum: %d\n", sum);
    
    return 0;
}
```

**Explanation:** This program demonstrates basic input/output operations. We declare variables to store the numbers and their sum, use scanf to read input with the & operator for addresses, and perform arithmetic operation.

---

## Problem E3: Area of a Rectangle

**Approach:** Calculate area using the formula: Area = length × width.
**Thinking:** Get dimensions from user, apply mathematical formula, display result.

```c
#include <stdio.h>

int main() {
    float length, width, area;
    
    printf("Enter length and width: ");
    scanf("%f %f", &length, &width);
    
    area = length * width;
    printf("Area: %.2f\n", area);
    
    return 0;
}
```

**Explanation:** We use float data type to handle decimal values. The formula is straightforward multiplication. The %.2f format specifier shows 2 decimal places in the output.

---

## Problem E4: Even or Odd

**Approach:** Use the modulo operator (%) to check divisibility by 2.
**Thinking:** If a number divided by 2 has remainder 0, it's even; otherwise, it's odd.

```c
#include <stdio.h>

int main() {
    int num;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    if (num % 2 == 0) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }
    
    return 0;
}
```

**Explanation:** The modulo operator (%) returns the remainder of division. When a number is divided by 2, if the remainder is 0, it's even. This demonstrates conditional statements and the modulo operator.

---

## Problem E5: Largest Among Three Numbers

**Approach:** Compare three numbers using nested if-else statements.
**Thinking:** Compare first two numbers, then compare the larger one with the third.

```c
#include <stdio.h>

int main() {
    int a, b, c, largest;
    
    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);
    
    if (a >= b && a >= c) {
        largest = a;
    } else if (b >= a && b >= c) {
        largest = b;
    } else {
        largest = c;
    }
    
    printf("Largest: %d\n", largest);
    
    return 0;
}
```

**Explanation:** We use logical AND (&&) operator to check multiple conditions. Each number is compared with the other two to determine which is largest. This demonstrates conditional logic and logical operators.

---

## Problem E6: Swap Two Numbers

**Approach:** Use a temporary variable to exchange values between two variables.
**Thinking:** Store one value temporarily, copy the second to first, then copy temp to second.

```c
#include <stdio.h>

int main() {
    int a, b, temp;
    
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    
    printf("Before swapping: a = %d, b = %d\n", a, b);
    
    // Swapping using temporary variable
    temp = a;
    a = b;
    b = temp;
    
    printf("After swapping: a = %d, b = %d\n", a, b);
    
    return 0;
}
```

**Explanation:** Swapping requires a temporary variable to avoid losing data. We store 'a' in temp, copy 'b' to 'a', then copy temp to 'b'. This is a fundamental technique used in many algorithms.

---

## Problem E7: Celsius to Fahrenheit Converter

**Approach:** Apply the conversion formula: F = (C × 9/5) + 32.
**Thinking:** Use the mathematical relationship between temperature scales.

```c
#include <stdio.h>

int main() {
    float celsius, fahrenheit;
    
    printf("Enter temperature in Celsius: ");
    scanf("%f", &celsius);
    
    fahrenheit = (celsius * 9.0 / 5.0) + 32.0;
    
    printf("%.1f Celsius = %.1f Fahrenheit\n", celsius, fahrenheit);
    
    return 0;
}
```

**Explanation:** We use the standard temperature conversion formula. Using 9.0 and 5.0 ensures floating-point division. This demonstrates mathematical calculations and formula implementation.

---

## Problem E8: Print Multiplication Table

**Approach:** Use a for loop to iterate from 1 to 10 and multiply with the given number.
**Thinking:** Repetitive calculation suggests using a loop structure.

```c
#include <stdio.h>

int main() {
    int num, i;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    printf("Multiplication table of %d:\n", num);
    for (i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", num, i, num * i);
    }
    
    return 0;
}
```

**Explanation:** A for loop is perfect for repetitive tasks with a known number of iterations. The loop variable 'i' goes from 1 to 10, and we multiply it with the input number each time.

---

## Problem E9: Sum of First N Natural Numbers

**Approach:** Use a loop to add numbers from 1 to N, or use the formula N*(N+1)/2.
**Thinking:** Either iterate and accumulate, or apply the mathematical formula directly.

```c
#include <stdio.h>

int main() {
    int n, sum = 0, i;
    
    printf("Enter a number: ");
    scanf("%d", &n);
    
    // Method 1: Using loop
    for (i = 1; i <= n; i++) {
        sum += i;
    }
    
    printf("Sum: %d\n", sum);
    
    // Method 2: Using formula (alternative)
    // sum = n * (n + 1) / 2;
    // printf("Sum using formula: %d\n", sum);
    
    return 0;
}
```

**Explanation:** This shows two approaches: iterative (using loop) and mathematical (using formula). The loop method demonstrates accumulation, while the formula method shows mathematical optimization.

---

## Problem E10: Check Leap Year

**Approach:** Apply leap year rules: divisible by 4, but not by 100, unless also divisible by 400.
**Thinking:** Use nested conditions to check multiple divisibility criteria.

```c
#include <stdio.h>

int main() {
    int year;
    
    printf("Enter a year: ");
    scanf("%d", &year);
    
    if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
        printf("%d is a leap year\n", year);
    } else {
        printf("%d is not a leap year\n", year);
    }
    
    return 0;
}
```

**Explanation:** Leap year logic requires checking multiple conditions with logical operators. A year is leap if it's divisible by 4 AND not by 100, OR if it's divisible by 400. This demonstrates complex logical expressions.

---

## Problem E11: Simple Calculator

**Approach:** Read two numbers and an operator, then use switch or if-else to perform the operation.
**Thinking:** Parse the operator and apply the corresponding arithmetic operation.

```c
#include <stdio.h>

int main() {
    float num1, num2, result;
    char operator;
    
    printf("Enter expression (e.g., 10 + 5): ");
    scanf("%f %c %f", &num1, &operator, &num2);
    
    switch (operator) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 != 0) {
                result = num1 / num2;
            } else {
                printf("Error: Division by zero!\n");
                return 1;
            }
            break;
        default:
            printf("Error: Invalid operator!\n");
            return 1;
    }
    
    printf("Result: %.2f\n", result);
    return 0;
}
```

**Explanation:** Switch statement provides clean handling of multiple cases. We include error checking for division by zero and invalid operators. This demonstrates switch statements and error handling.

---

## Problem E12: Count Digits in a Number

**Approach:** Repeatedly divide the number by 10 until it becomes 0, counting each division.
**Thinking:** Each division by 10 removes one digit, so count the divisions.

```c
#include <stdio.h>

int main() {
    int num, count = 0, temp;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    temp = num;
    
    // Handle special case of 0
    if (temp == 0) {
        count = 1;
    } else {
        // Handle negative numbers
        if (temp < 0) {
            temp = -temp;
        }
        
        while (temp > 0) {
            temp /= 10;
            count++;
        }
    }
    
    printf("Number of digits: %d\n", count);
    return 0;
}
```

**Explanation:** We use integer division by 10 to remove digits one by one. The loop continues until no digits remain. Special cases like 0 and negative numbers need separate handling.

---

## Problem E13: Factorial Calculator

**Approach:** Multiply all numbers from 1 to N, or use recursive approach.
**Thinking:** Factorial is the product of all positive integers up to N.

```c
#include <stdio.h>

int main() {
    int n, i;
    long long factorial = 1;
    
    printf("Enter a number: ");
    scanf("%d", &n);
    
    if (n < 0) {
        printf("Factorial is not defined for negative numbers.\n");
    } else {
        for (i = 1; i <= n; i++) {
            factorial *= i;
        }
        printf("Factorial of %d = %lld\n", n, factorial);
    }
    
    return 0;
}
```

**Explanation:** We use long long to handle large factorial values. The loop multiplies all numbers from 1 to n. We include validation for negative inputs since factorial is undefined for negative numbers.

---

## Problem E14: Reverse a Number

**Approach:** Extract digits from right to left using modulo, build reversed number by multiplying by 10.
**Thinking:** Extract last digit, add to result, remove last digit from original number.

```c
#include <stdio.h>

int main() {
    int num, reversed = 0, remainder, temp;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    temp = num;
    
    while (temp != 0) {
        remainder = temp % 10;
        reversed = reversed * 10 + remainder;
        temp /= 10;
    }
    
    printf("Reversed: %d\n", reversed);
    return 0;
}
```

**Explanation:** We extract the last digit using modulo 10, add it to our result (after shifting previous digits left by multiplying by 10), then remove the last digit using integer division by 10.

---

## Problem E15: Check if a Number is Positive, Negative, or Zero

**Approach:** Use simple if-else statements to compare the number with zero.
**Thinking:** Compare the number against zero using relational operators.

```c
#include <stdio.h>

int main() {
    int num;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    if (num > 0) {
        printf("Positive\n");
    } else if (num < 0) {
        printf("Negative\n");
    } else {
        printf("Zero\n");
    }
    
    return 0;
}
```

**Explanation:** This demonstrates basic conditional logic using if-else if-else structure. We check three mutually exclusive conditions: greater than, less than, or equal to zero.

---

## Problem E16: Print ASCII Value

**Approach:** Read a character and cast it to integer to get its ASCII value.
**Thinking:** Characters are internally stored as ASCII values, so casting reveals the numeric value.

```c
#include <stdio.h>

int main() {
    char ch;
    
    printf("Enter a character: ");
    scanf("%c", &ch);
    
    printf("ASCII value of '%c' is %d\n", ch, (int)ch);
    
    return 0;
}
```

**Explanation:** Characters in C are represented by their ASCII values. By casting a character to int, we can see its numeric ASCII value. This demonstrates type casting and character handling.

---

## Problem E17: Sum of Digits

**Approach:** Extract each digit using modulo 10 and add to sum, then remove digit using division by 10.
**Thinking:** Similar to digit counting, but accumulate the digit values instead of counting them.

```c
#include <stdio.h>

int main() {
    int num, sum = 0, remainder, temp;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    temp = num;
    
    // Handle negative numbers
    if (temp < 0) {
        temp = -temp;
    }
    
    while (temp > 0) {
        remainder = temp % 10;
        sum += remainder;
        temp /= 10;
    }
    
    printf("Sum of digits: %d\n", sum);
    return 0;
}
```

**Explanation:** We extract each digit using modulo 10, add it to our sum, then remove it using integer division. This is similar to the reverse number algorithm but accumulates the digits instead.

---

## Problem E18: Check Vowel or Consonant

**Approach:** Compare the input character with all vowels (both uppercase and lowercase).
**Thinking:** Check if the character matches any of the vowel characters: a, e, i, o, u.

```c
#include <stdio.h>

int main() {
    char ch;
    
    printf("Enter a character: ");
    scanf("%c", &ch);
    
    if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' ||
        ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U') {
        printf("'%c' is a vowel\n", ch);
    } else if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')) {
        printf("'%c' is a consonant\n", ch);
    } else {
        printf("'%c' is not a letter\n", ch);
    }
    
    return 0;
}
```

**Explanation:** We check against all vowels in both cases. We also validate that the input is actually a letter before classifying as consonant. This demonstrates multiple OR conditions and input validation.

---

## Problem E19: GCD of Two Numbers

**Approach:** Use Euclidean algorithm - repeatedly replace larger number with remainder of division.
**Thinking:** GCD(a,b) = GCD(b, a%b) until one number becomes 0.

```c
#include <stdio.h>

int main() {
    int a, b, temp;
    
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    
    // Store original values for display
    int orig_a = a, orig_b = b;
    
    // Euclidean algorithm
    while (b != 0) {
        temp = b;
        b = a % b;
        a = temp;
    }
    
    printf("GCD of %d and %d is %d\n", orig_a, orig_b, a);
    return 0;
}
```

**Explanation:** The Euclidean algorithm is efficient for finding GCD. We repeatedly replace the larger number with the remainder until one becomes zero. The other number is the GCD.

---

## Problem E20: LCM of Two Numbers

**Approach:** Use the relationship: LCM(a,b) = (a*b)/GCD(a,b).
**Thinking:** Calculate GCD first, then use the mathematical relationship to find LCM.

```c
#include <stdio.h>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int a, b, lcm, gcd_value;
    
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);
    
    gcd_value = gcd(a, b);
    lcm = (a * b) / gcd_value;
    
    printf("LCM of %d and %d is %d\n", a, b, lcm);
    return 0;
}
```

**Explanation:** We create a separate function for GCD calculation, then use the mathematical relationship between LCM and GCD. This demonstrates function creation and mathematical relationships.

---

## Problem E21: Check Armstrong Number

**Approach:** Calculate sum of cubes of digits and compare with original number.
**Thinking:** For a 3-digit Armstrong number, sum of cubes of digits equals the number itself.

```c
#include <stdio.h>
#include <math.h>

int main() {
    int num, temp, sum = 0, remainder;
    
    printf("Enter a three-digit number: ");
    scanf("%d", &num);
    
    temp = num;
    
    while (temp != 0) {
        remainder = temp % 10;
        sum += pow(remainder, 3);
        temp /= 10;
    }
    
    if (sum == num) {
        printf("%d is an Armstrong number\n", num);
    } else {
        printf("%d is not an Armstrong number\n", num);
    }
    
    return 0;
}
```

**Explanation:** We extract each digit, cube it using pow function, and add to sum. If the sum equals the original number, it's an Armstrong number. This combines digit extraction with mathematical operations.

---

## Problem E22: Find Power of a Number

**Approach:** Use a loop to multiply the base by itself exponent number of times.
**Thinking:** Power is repeated multiplication of the base.

```c
#include <stdio.h>

int main() {
    int base, exponent, result = 1, i;
    
    printf("Enter base and exponent: ");
    scanf("%d %d", &base, &exponent);
    
    if (exponent < 0) {
        printf("This program handles only non-negative exponents.\n");
        return 1;
    }
    
    for (i = 1; i <= exponent; i++) {
        result *= base;
    }
    
    printf("%d^%d = %d\n", base, exponent, result);
    return 0;
}
```

**Explanation:** We multiply the base by itself exponent number of times using a loop. We start with result = 1 and multiply by base in each iteration. This demonstrates iterative calculation and exponentiation.

---

## Problem E23: Check Perfect Number

**Approach:** Find all proper divisors (excluding the number itself) and check if their sum equals the number.
**Thinking:** A perfect number equals the sum of its proper positive divisors.

```c
#include <stdio.h>

int main() {
    int num, sum = 0, i;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    if (num <= 1) {
        printf("%d is not a perfect number\n", num);
        return 0;
    }
    
    // Find proper divisors and calculate their sum
    for (i = 1; i < num; i++) {
        if (num % i == 0) {
            sum += i;
        }
    }
    
    if (sum == num) {
        printf("%d is a perfect number\n", num);
    } else {
        printf("%d is not a perfect number\n", num);
    }
    
    return 0;
}
```

**Explanation:** We iterate through all numbers less than the input, check if they divide evenly (using modulo), and sum them up. If the sum equals the original number, it's perfect.

---

## Problem E24: Print First N Fibonacci Numbers

**Approach:** Start with 0 and 1, then each subsequent number is the sum of the previous two.
**Thinking:** Use two variables to track the last two numbers and generate the sequence.

```c
#include <stdio.h>

int main() {
    int n, i, first = 0, second = 1, next;
    
    printf("Enter the number of terms: ");
    scanf("%d", &n);
    
    if (n <= 0) {
        printf("Please enter a positive number.\n");
        return 1;
    }
    
    printf("Fibonacci sequence: ");
    
    if (n >= 1) {
        printf("%d ", first);
    }
    if (n >= 2) {
        printf("%d ", second);
    }
    
    for (i = 3; i <= n; i++) {
        next = first + second;
        printf("%d ", next);
        first = second;
        second = next;
    }
    
    printf("\n");
    return 0;
}
```

**Explanation:** We handle the first two terms separately, then use a loop to generate subsequent terms by adding the previous two. We update the tracking variables in each iteration.

---

## Problem E25: Check if a Number is Prime

**Approach:** Check if the number has any divisors other than 1 and itself.
**Thinking:** Test divisibility from 2 to sqrt(n) for efficiency.

```c
#include <stdio.h>
#include <math.h>

int main() {
    int num, i, isPrime = 1;
    
    printf("Enter a number: ");
    scanf("%d", &num);
    
    if (num <= 1) {
        isPrime = 0;
    } else {
        for (i = 2; i <= sqrt(num); i++) {
            if (num % i == 0) {
                isPrime = 0;
                break;
            }
        }
    }
    
    if (isPrime) {
        printf("%d is a prime number\n", num);
    } else {
        printf("%d is not a prime number\n", num);
    }
    
    return 0;
}
```

**Explanation:** We only need to check divisors up to the square root of the number because if a number has a divisor greater than its square root, it must also have a corresponding divisor less than the square root.

---

## Problem E26: Print Inverted Number Pattern

**Approach:** Use nested loops - outer loop for rows, inner loop for numbers in each row.
**Thinking:** Each row starts with the row number and decreases to 1.

```c
#include <stdio.h>

int main() {
    int n, i, j;
    
    printf("Enter number of rows: ");
    scanf("%d", &n);
    
    for (i = n; i >= 1; i--) {
        for (j = i; j >= 1; j--) {
            printf("%d ", j);
        }
        printf("\n");
    }
    
    return 0;
}
```

**Explanation:** The outer loop controls rows (from n down to 1), and the inner loop prints numbers in each row (from the row number down to 1). This demonstrates nested loops and pattern logic.

---

## Problem E27: Find Maximum Element in an Array

**Approach:** Assume first element is maximum, then compare with each subsequent element.
**Thinking:** Linear search through array, updating maximum when a larger element is found.

```c
#include <stdio.h>

int main() {
    int arr[100], n, i, max;
    
    printf("Enter number of elements: ");
    scanf("%d", &n);
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    max = arr[0];  // Assume first element is maximum
    
    for (i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    
    printf("Maximum element: %d\n", max);
    return 0;
}
```

**Explanation:** We initialize max with the first element, then compare each subsequent element. If we find a larger element, we update max. This demonstrates array handling and linear search.

---

## Problem E28: Find Minimum Element in an Array

**Approach:** Similar to maximum, but compare for smaller values.
**Thinking:** Initialize with first element, update when finding smaller elements.

```c
#include <stdio.h>

int main() {
    int arr[100], n, i, min;
    
    printf("Enter number of elements: ");
    scanf("%d", &n);
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    min = arr[0];  // Assume first element is minimum
    
    for (i = 1; i < n; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
    }
    
    printf("Minimum element: %d\n", min);
    return 0;
}
```

**Explanation:** Same logic as finding maximum, but we compare for smaller values. This demonstrates the pattern of finding extremes in arrays.

---

## Problem E29: Calculate Average of Array Elements

**Approach:** Sum all elements and divide by the count.
**Thinking:** Use accumulation to find sum, then perform division for average.

```c
#include <stdio.h>

int main() {
    int arr[100], n, i, sum = 0;
    float average;
    
    printf("Enter number of elements: ");
    scanf("%d", &n);
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
        sum += arr[i];  // Add to sum while reading
    }
    
    average = (float)sum / n;
    
    printf("Average: %.2f\n", average);
    return 0;
}
```

**Explanation:** We accumulate the sum while reading elements, then divide by count to get average. We cast to float to ensure floating-point division and accurate results.

---

## Problem E30: String Length Calculator

**Approach:** Count characters until we reach the null terminator '\0'.
**Thinking:** Iterate through string characters and count until end marker.

```c
#include <stdio.h>

int main() {
    char str[1000];
    int length = 0, i = 0;
    
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    
    while (str[i] != '\0' && str[i] != '\n') {
        length++;
        i++;
    }
    
    printf("Length: %d\n", length);
    return 0;
}
```

**Explanation:** We iterate through each character of the string until we hit the null terminator or newline. We increment a counter for each character. This demonstrates string handling and manual length calculation.

---

## Problem E31: String Copy

**Approach:** Copy each character from source to destination until null terminator.
**Thinking:** Iterate through source string and copy each character to destination.

```c
#include <stdio.h>

int main() {
    char source[1000], destination[1000];
    int i = 0;
    
    printf("Enter source string: ");
    fgets(source, sizeof(source), stdin);
    
    // Copy each character
    while (source[i] != '\0') {
        destination[i] = source[i];
        i++;
    }
    destination[i] = '\0';  // Add null terminator
    
    printf("Copied string: %s", destination);
    return 0;
}
```

**Explanation:** We manually copy each character from source to destination array. We ensure to copy the null terminator to properly terminate the destination string.

---

## Problem E32: String Concatenation

**Approach:** Find end of first string, then append second string from that position.
**Thinking:** Locate the end of the first string, then copy the second string starting from there.

```c
#include <stdio.h>

int main() {
    char str1[1000], str2[1000];
    int i = 0, j = 0;
    
    printf("Enter first string: ");
    fgets(str1, sizeof(str1), stdin);
    
    printf("Enter second string: ");
    fgets(str2, sizeof(str2), stdin);
    
    // Find end of first string (excluding newline)
    while (str1[i] != '\0' && str1[i] != '\n') {
        i++;
    }
    
    // Append second string
    while (str2[j] != '\0') {
        str1[i] = str2[j];
        i++;
        j++;
    }
    str1[i] = '\0';  // Null terminate
    
    printf("Concatenated string: %s", str1);
    return 0;
}
```

**Explanation:** We first find the end of the first string, then append the second string character by character. We ensure proper null termination of the result.

---

## Problem E33: Count Vowels and Consonants

**Approach:** Iterate through string and classify each character as vowel, consonant, or other.
**Thinking:** Check each character against vowel list and alphabet range.

```c
#include <stdio.h>

int main() {
    char str[1000];
    int vowels = 0, consonants = 0, i = 0;
    
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    
    while (str[i] != '\0') {
        char ch = str[i];
        
        if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')) {
            // It's a letter
            if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u' ||
                ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U') {
                vowels++;
            } else {
                consonants++;
            }
        }
        // Ignore non-alphabetic characters
        i++;
    }
    
    printf("Vowels: %d\n", vowels);
    printf("Consonants: %d\n", consonants);
    return 0;
}
```

**Explanation:** We iterate through each character, first checking if it's a letter, then classifying it as vowel or consonant. Non-alphabetic characters are ignored.

---

## Problem E34: Function to Find Square

**Approach:** Create a function that takes an integer parameter and returns its square.
**Thinking:** Encapsulate the square calculation in a reusable function.

```c
#include <stdio.h>

int findSquare(int num) {
    return num * num;
}

int main() {
    int number, result;
    
    printf("Enter a number: ");
    scanf("%d", &number);
    
    result = findSquare(number);
    
    printf("Square of %d is %d\n", number, result);
    return 0;
}
```

**Explanation:** This demonstrates function creation with parameter passing and return values. The function encapsulates the square calculation logic, making it reusable and modular.

---

## Problem E35: Function to Check Even or Odd

**Approach:** Create a function that returns 1 for even numbers and 0 for odd numbers.
**Thinking:** Use modulo operation inside a function and return boolean-like result.

```c
#include <stdio.h>

int isEven(int num) {
    return (num % 2 == 0);
}

int main() {
    int number;
    
    printf("Enter a number: ");
    scanf("%d", &number);
    
    if (isEven(number)) {
        printf("%d is even\n", number);
    } else {
        printf("%d is odd\n", number);
    }
    
    return 0;
}
```

**Explanation:** The function returns 1 (true) if the number is even, 0 (false) if odd. This demonstrates boolean-like return values and function-based logic encapsulation.

---

## Problem E36: Character Pattern

**Approach:** Use nested loops with ASCII arithmetic to generate character sequences.
**Thinking:** Each row prints characters from 'A' up to the row's corresponding letter.

```c
#include <stdio.h>

int main() {
    int n, i, j;
    
    printf("Enter number of rows: ");
    scanf("%d", &n);
    
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= i; j++) {
            printf("%c", 'A' + j - 1);
        }
        printf("\n");
    }
    
    return 0;
}
```

**Explanation:** We use ASCII arithmetic where 'A' + 0 = 'A', 'A' + 1 = 'B', etc. The outer loop controls rows, inner loop prints characters for each row.

---

## Problem E37: Simple File Operations

**Approach:** Use file I/O functions to create, write, and read from files.
**Thinking:** Demonstrate basic file operations: opening, writing, closing, reopening, reading.

```c
#include <stdio.h>

int main() {
    FILE *file;
    char text[1000];
    char readText[1000];
    
    printf("Enter text to write: ");
    fgets(text, sizeof(text), stdin);
    
    // Create and write to file
    file = fopen("sample.txt", "w");
    if (file == NULL) {
        printf("Error creating file!\n");
        return 1;
    }
    
    fprintf(file, "%s", text);
    fclose(file);
    printf("File created successfully\n");
    printf("Data written to file\n");
    
    // Read from file
    file = fopen("sample.txt", "r");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    
    fgets(readText, sizeof(readText), file);
    fclose(file);
    
    printf("Reading from file: %s", readText);
    
    return 0;
}
```

**Explanation:** This demonstrates file I/O operations including creating files, writing data, and reading data back. We include error checking for file operations.

---

## Problem E38: Day of Week Calculator

**Approach:** Implement Zeller's Congruence algorithm for day calculation.
**Thinking:** Use the mathematical formula that relates date components to day of week.

```c
#include <stdio.h>

int main() {
    int day, month, year, dayOfWeek;
    char* days[] = {"Saturday", "Sunday", "Monday", "Tuesday", 
                    "Wednesday", "Thursday", "Friday"};
    char* months[] = {"", "January", "February", "March", "April", "May", "June",
                      "July", "August", "September", "October", "November", "December"};
    
    printf("Enter day month year (e.g., 15 8 2023): ");
    scanf("%d %d %d", &day, &month, &year);
    
    // Zeller's Congruence algorithm
    if (month < 3) {
        month += 12;
        year--;
    }
    
    dayOfWeek = (day + (13 * (month + 1)) / 5 + year + year / 4 - year / 100 + year / 400) % 7;
    
    printf("%d %s %d is a %s\n", day, months[month > 12 ? month - 12 : month], 
           month > 12 ? year + 1 : year, days[dayOfWeek]);
    
    return 0;
}
```

**Explanation:** Zeller's Congruence is a mathematical algorithm to calculate the day of the week. We handle the special case where January and February are treated as months 13 and 14 of the previous year.

---

## Problem E39: Binary to Hexadecimal Conversion

**Approach:** Group binary digits in sets of 4 and convert each group to hexadecimal.
**Thinking:** Each group of 4 binary digits represents one hexadecimal digit.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char binary[1000], hex[1000] = "";
    int len, i, decimal;
    char hexDigits[] = "0123456789ABCDEF";
    
    printf("Enter binary number: ");
    scanf("%s", binary);
    
    len = strlen(binary);
    
    // Pad with leading zeros if necessary to make length multiple of 4
    int padding = (4 - len % 4) % 4;
    for (i = 0; i < padding; i++) {
        printf("0");
    }
    printf("%s -> ", binary);
    
    // Process 4 bits at a time
    for (i = 0; i <= len - 1; i += 4) {
        decimal = 0;
        
        // Convert 4 binary digits to decimal
        for (int j = 0; j < 4 && (i + j) < len; j++) {
            if (binary[i + j] == '1') {
                decimal += (1 << (3 - j));
            }
        }
        
        printf("%c", hexDigits[decimal]);
    }
    
    printf("\n");
    return 0;
}
```

**Explanation:** We process 4 binary digits at a time, convert each group to decimal (0-15), then map to hexadecimal characters. This demonstrates string processing and number base conversion.

---

## Problem E40: Digit Frequency Counter

**Approach:** Count occurrences of each digit (0-9) in the given number.
**Thinking:** Extract each digit and increment its counter in a frequency array.

```c
#include <stdio.h>

int main() {
    long long num, temp;
    int frequency[10] = {0}; // Initialize all to 0
    int digit;
    
    printf("Enter a number: ");
    scanf("%lld", &num);
    
    temp = num;
    
    // Handle the case of 0
    if (temp == 0) {
        frequency[0] = 1;
    } else {
        // Handle negative numbers
        if (temp < 0) {
            temp = -temp;
        }
        
        while (temp > 0) {
            digit = temp % 10;
            frequency[digit]++;
            temp /= 10;
        }
    }
    
    printf("Digit frequencies:\n");
    for (int i = 0; i <= 9; i++) {
        if (frequency[i] > 0) {
            printf("Digit %d: %d time%s\n", i, frequency[i], 
                   frequency[i] > 1 ? "s" : "");
        }
    }
    
    return 0;
}
```

**Explanation:** We use an array to count frequency of each digit (0-9). We extract digits one by one and increment the corresponding array element. This demonstrates array indexing and frequency counting patterns.

---

## Summary of Key Programming Concepts Covered:

1. **Basic I/O Operations**: scanf, printf, fgets
2. **Control Structures**: if-else, switch, loops (for, while)
3. **Data Types**: int, float, char, arrays
4. **Operators**: Arithmetic, relational, logical, modulo
5. **Functions**: Parameter passing, return values
6. **Arrays**: Declaration, initialization, traversal
7. **Strings**: Character arrays, manual string operations
8. **File I/O**: fopen, fprintf, fgets, fclose
9. **Mathematical Operations**: Powers, factorials, GCD/LCM
10. **Pattern Recognition**: Nested loops, ASCII arithmetic
11. **Algorithm Implementation**: Search, mathematical formulas
12. **Error Handling**: Input validation, edge cases

These solutions provide a solid foundation for understanding C programming fundamentals and developing problem-solving skills.