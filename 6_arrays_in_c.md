# Arrays in C

## Introduction to Arrays

An array is a collection of elements of the same data type stored in contiguous memory locations. Arrays provide an efficient way to store and access multiple values using a single variable name.

### Why Use Arrays?

Consider a scenario where you need to store the marks of 50 students. Without arrays, you would need 50 different variables:

```c
int mark1, mark2, mark3, ..., mark50;
```

With arrays, you can simply write:

```c
int marks[50];
```

Arrays make your code more maintainable, concise, and efficient, especially when dealing with large amounts of data.

![Array in Memory Visualization](https://placeholder-for-array-memory-diagram.png)

## Declaring and Initializing Arrays

### Array Declaration

The basic syntax for declaring an array is:

```c
data_type array_name[size];
```

Where:
- `data_type` is any valid C data type (int, float, char, etc.)
- `array_name` is the identifier for the array
- `size` is the number of elements the array can hold

Examples:

```c
int numbers[10];      // Array of 10 integers
float prices[100];    // Array of 100 floating-point numbers
char name[50];        // Array of 50 characters
```

### Array Initialization

#### Method 1: Initialize at Declaration

```c
int numbers[5] = {10, 20, 30, 40, 50};
```

#### Method 2: Initialize without Size (Size is inferred)

```c
int numbers[] = {10, 20, 30, 40, 50};  // Size is automatically set to 5
```

#### Method 3: Partial Initialization

```c
int numbers[5] = {10, 20};  // Other elements are initialized to 0: {10, 20, 0, 0, 0}
```

#### Method 4: Initialize All Elements to Zero

```c
int numbers[5] = {0};  // All elements set to 0: {0, 0, 0, 0, 0}
```

#### Method 5: Initialize Specific Elements

```c
int numbers[5] = {[0] = 10, [2] = 30, [4] = 50};  // {10, 0, 30, 0, 50}
```

### Memory Allocation for Arrays

Arrays in C are stored in contiguous memory locations. For example, if `numbers` is an array of integers starting at memory address 1000, and each integer occupies 4 bytes, then:

- `numbers[0]` is stored at address 1000
- `numbers[1]` is stored at address 1004
- `numbers[2]` is stored at address 1008
- And so on...

![Array Memory Allocation](https://placeholder-for-array-allocation-diagram.png)

## Accessing and Modifying Array Elements

### Accessing Elements

Array elements are accessed using the index (position) of the element. In C, array indices start from 0.

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    // Accessing individual elements
    printf("First element: %d\n", numbers[0]);    // 10
    printf("Third element: %d\n", numbers[2]);    // 30
    printf("Last element: %d\n", numbers[4]);     // 50
    
    return 0;
}
```

### Modifying Elements

You can modify array elements by assigning new values to them:

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    // Modify the second element
    numbers[1] = 25;
    
    // Print the modified array
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);  // Output: 10 25 30 40 50
    }
    
    return 0;
}
```

### Common Errors with Array Access

1. **Array Index Out of Bounds**:

```c
int numbers[5];
numbers[5] = 60;  // ERROR: Valid indices are 0 to 4
```

This is a common source of bugs because C does not perform bounds checking. Accessing out-of-bounds memory can lead to unpredictable behavior, segmentation faults, or security vulnerabilities.

2. **Using Uninitialized Arrays**:

```c
int numbers[5];  // Elements contain garbage values
printf("%d\n", numbers[2]);  // Unpredictable output
```

## Iterating Through Arrays

### Using for Loop

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    printf("Array elements: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    
    return 0;
}
```

### Using while Loop

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    printf("Array elements: ");
    int i = 0;
    while (i < 5) {
        printf("%d ", numbers[i]);
        i++;
    }
    
    return 0;
}
```

### Using do-while Loop

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    printf("Array elements: ");
    int i = 0;
    do {
        printf("%d ", numbers[i]);
        i++;
    } while (i < 5);
    
    return 0;
}
```

## Multi-dimensional Arrays

C supports multi-dimensional arrays, with two-dimensional arrays being the most common.

### Two-dimensional Arrays

A two-dimensional array is essentially an "array of arrays" and can be visualized as a table with rows and columns.

#### Declaration and Initialization

```c
// Declaration
int matrix[3][4];  // 3 rows and 4 columns

// Initialization
int matrix[3][4] = {
    {1, 2, 3, 4},    // First row
    {5, 6, 7, 8},    // Second row
    {9, 10, 11, 12}  // Third row
};
```

#### Accessing Elements

```c
#include <stdio.h>

int main() {
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };
    
    // Accessing specific element (row 1, column 2)
    printf("Element at matrix[1][2]: %d\n", matrix[1][2]);  // 7
    
    return 0;
}
```

#### Iterating Through a 2D Array

```c
#include <stdio.h>

int main() {
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };
    
    // Print all elements of the matrix
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            printf("%3d", matrix[i][j]);  // %3d for formatting
        }
        printf("\n");
    }
    
    return 0;
}
```

### Three-dimensional Arrays

Three-dimensional arrays can be thought of as a collection of 2D arrays.

```c
// Declaration
int cube[3][3][3];

// Initialization
int cube[2][2][3] = {
    {  // First 2D array
        {1, 2, 3},
        {4, 5, 6}
    },
    {  // Second 2D array
        {7, 8, 9},
        {10, 11, 12}
    }
};
```

![3D Array Visualization](https://placeholder-for-3d-array-diagram.png)

## Common Operations on Arrays

### 1. Finding the Sum and Average

```c
#include <stdio.h>

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    int sum = 0;
    
    // Calculate the sum
    for (int i = 0; i < 5; i++) {
        sum += numbers[i];
    }
    
    // Calculate the average
    float average = (float)sum / 5;
    
    printf("Sum: %d\n", sum);
    printf("Average: %.2f\n", average);
    
    return 0;
}
```

### 2. Finding the Maximum and Minimum

```c
#include <stdio.h>

int main() {
    int numbers[5] = {30, 10, 50, 20, 40};
    
    int max = numbers[0];  // Assume first element is the maximum
    int min = numbers[0];  // Assume first element is the minimum
    
    // Find maximum and minimum
    for (int i = 1; i < 5; i++) {
        if (numbers[i] > max) {
            max = numbers[i];
        }
        if (numbers[i] < min) {
            min = numbers[i];
        }
    }
    
    printf("Maximum: %d\n", max);
    printf("Minimum: %d\n", min);
    
    return 0;
}
```

### 3. Linear Search

Linear search is a simple algorithm that searches for an element by checking each element sequentially.

```c
#include <stdio.h>

int linearSearch(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i;  // Return the index if found
        }
    }
    return -1;  // Return -1 if not found
}

int main() {
    int numbers[5] = {30, 10, 50, 20, 40};
    int target = 50;
    
    int index = linearSearch(numbers, 5, target);
    
    if (index != -1) {
        printf("%d found at index %d\n", target, index);
    } else {
        printf("%d not found in the array\n", target);
    }
    
    return 0;
}
```

### 4. Binary Search (for Sorted Arrays)

Binary search is an efficient algorithm that works on sorted arrays by repeatedly dividing the search interval in half.

```c
#include <stdio.h>

int binarySearch(int arr[], int left, int right, int target) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        // Check if target is present at mid
        if (arr[mid] == target)
            return mid;
        
        // If target greater, ignore left half
        if (arr[mid] < target)
            left = mid + 1;
        // If target is smaller, ignore right half
        else
            right = mid - 1;
    }
    
    // Element not present
    return -1;
}

int main() {
    int sortedNumbers[5] = {10, 20, 30, 40, 50};  // Must be sorted
    int target = 30;
    
    int index = binarySearch(sortedNumbers, 0, 4, target);
    
    if (index != -1) {
        printf("%d found at index %d\n", target, index);
    } else {
        printf("%d not found in the array\n", target);
    }
    
    return 0;
}
```

### 5. Sorting Arrays

#### Bubble Sort

```c
#include <stdio.h>

void bubbleSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int numbers[5] = {30, 10, 50, 20, 40};
    
    printf("Before sorting: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    
    bubbleSort(numbers, 5);
    
    printf("\nAfter sorting: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    
    return 0;
}
```

#### Selection Sort

```c
#include <stdio.h>

void selectionSort(int arr[], int size) {
    for (int i = 0; i < size - 1; i++) {
        // Find the minimum element in unsorted array
        int min_idx = i;
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        
        // Swap the found minimum element with the first element
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main() {
    int numbers[5] = {30, 10, 50, 20, 40};
    
    printf("Before sorting: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    
    selectionSort(numbers, 5);
    
    printf("\nAfter sorting: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }
    
    return 0;
}
```

## Arrays and Functions

### Passing Arrays to Functions

In C, when you pass an array to a function, you're actually passing a pointer to the first element of the array.

```c
#include <stdio.h>

// Function that takes an array as a parameter
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Function that modifies the array
void doubleElements(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2;
    }
}

int main() {
    int numbers[5] = {10, 20, 30, 40, 50};
    
    printf("Original array: ");
    printArray(numbers, 5);
    
    doubleElements(numbers, 5);
    
    printf("Modified array: ");
    printArray(numbers, 5);
    
    return 0;
}
```

### Returning Arrays from Functions

C doesn't allow functions to return arrays directly. However, you can:
1. Return a pointer to an array
2. Pass an array to a function, and modify it in place
3. Use dynamically allocated arrays (covered later)

```c
#include <stdio.h>

// Return pointer to a static array (not recommended for general use)
int* getStaticArray() {
    static int arr[5] = {10, 20, 30, 40, 50};
    return arr;
}

// Fill an existing array (better approach)
void fillArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] = i * 10 + 10;
    }
}

int main() {
    // Approach 1: Using a function that returns a static array
    int *staticArr = getStaticArray();
    printf("Static array: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", staticArr[i]);
    }
    printf("\n");
    
    // Approach 2: Passing an array to be filled
    int dynamicArr[5];
    fillArray(dynamicArr, 5);
    printf("Filled array: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", dynamicArr[i]);
    }
    printf("\n");
    
    return 0;
}
```

## Variable-Length Arrays (VLAs)

C99 introduced Variable-Length Arrays (VLAs), which allow array dimensions to be specified by runtime expressions.

```c
#include <stdio.h>

void processArray(int size) {
    int vla[size];  // Size determined at runtime
    
    // Fill the array
    for (int i = 0; i < size; i++) {
        vla[i] = i * i;
    }
    
    // Print the array
    for (int i = 0; i < size; i++) {
        printf("%d ", vla[i]);
    }
    printf("\n");
}

int main() {
    int size;
    
    printf("Enter the size of the array: ");
    scanf("%d", &size);
    
    processArray(size);
    
    return 0;
}
```

**Note**: VLAs have limitations:
- They cannot be initialized at declaration
- They must be allocated on the stack, which has limited size
- Some compilers don't fully support them, and they were made optional in C11

## Common Pitfalls and Best Practices

### Pitfalls

1. **Array Index Out of Bounds**:
   C does not check for array bounds, leading to undefined behavior.

2. **Forgetting that Array Indices Start at 0**:
   The last valid index is `size - 1`.

3. **Confusing Arrays with Pointers**:
   While arrays decay to pointers when passed to functions, they are not the same.

4. **Using Uninitialized Arrays**:
   Uninitialized arrays contain garbage values.

5. **Stack Overflow with Large Arrays**:
   Declaring large arrays on the stack can cause stack overflow.

### Best Practices

1. **Check Array Bounds**:
   Always validate indices before accessing array elements.

2. **Use Symbolic Constants for Array Sizes**:
   ```c
   #define SIZE 100
   int array[SIZE];
   ```

3. **Initialize Arrays**:
   Always initialize arrays, at least to zero if no specific values are needed.

4. **Use Dynamic Allocation for Large Arrays**:
   Use heap memory (malloc) for large arrays to avoid stack overflow.

5. **Pass Array Size to Functions**:
   Always pass the size along with the array.

## Practice Exercises

1. Write a program to reverse an array without using another array.

2. Implement a function that removes duplicate elements from an array.

3. Write a program to find the second largest element in an array.

4. Implement a function that merges two sorted arrays into a third sorted array.

5. Create a function to rotate an array left or right by a given number of positions.

6. Write a program to find the most frequent element in an array.

7. Implement matrix multiplication for two 2D arrays.

## Key Takeaways

1. Arrays provide a way to store multiple elements of the same type under a single name.

2. Array indices start at 0, and the last valid index is `size - 1`.

3. Arrays are stored in contiguous memory locations.

4. Multi-dimensional arrays can represent tables, matrices, or higher-dimensional data.

5. When passing arrays to functions, C actually passes a pointer to the first element.

6. Common array operations include searching, sorting, and calculating statistical values.

7. Always be careful with array bounds to avoid undefined behavior.
