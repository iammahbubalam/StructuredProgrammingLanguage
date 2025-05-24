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
