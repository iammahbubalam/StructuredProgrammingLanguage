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
