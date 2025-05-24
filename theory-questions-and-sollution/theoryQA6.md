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
