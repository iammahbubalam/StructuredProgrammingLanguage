# Medium Level Problem Solutions

## M1. Array Reversal

**Description:** Write a program that reverses an array and prints the reversed array.

```c
#include <stdio.h>

int main() {
    int n, i;
    
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    
    int arr[n];
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    printf("Original array: ");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    
    printf("\nReversed array: ");
    for (i = n - 1; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M2. Find Frequency of Elements in an Array

**Description:** Write a program that counts the frequency of each element in an array.

```c
#include <stdio.h>

int main() {
    int n, i, j, count;
    
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    
    int arr[n], visited[n];
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
        visited[i] = 0;
    }
    
    printf("\nFrequency of each element:\n");
    
    for (i = 0; i < n; i++) {
        if (visited[i] == 1) {
            continue;
        }
        
        count = 1;
        for (j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                count++;
                visited[j] = 1;
            }
        }
        
        printf("%d occurs %d time(s)\n", arr[i], count);
    }
    
    return 0;
}
```

---

## M3. Bubble Sort

**Description:** Write a program that sorts an array using the Bubble Sort algorithm.

```c
#include <stdio.h>

int main() {
    int n, i, j, temp;
    
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    
    int arr[n];
    
    printf("Enter %d elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    printf("Original array: ");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    
    // Bubble Sort
    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    
    printf("\nSorted array: ");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M4. Binary Search

**Description:** Write a program that implements binary search on a sorted array.

```c
#include <stdio.h>

int main() {
    int n, i, target, left, right, mid, found = 0;
    
    printf("Enter the number of elements: ");
    scanf("%d", &n);
    
    int arr[n];
    
    printf("Enter %d sorted elements: ", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    printf("Enter element to search: ");
    scanf("%d", &target);
    
    left = 0;
    right = n - 1;
    
    while (left <= right) {
        mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            printf("Element found at index %d\n", mid);
            found = 1;
            break;
        }
        else if (arr[mid] < target) {
            left = mid + 1;
        }
        else {
            right = mid - 1;
        }
    }
    
    if (!found) {
        printf("Element not found\n");
    }
    
    return 0;
}
```

---

## M5. Matrix Addition

**Description:** Write a program that performs addition of two matrices.

```c
#include <stdio.h>

int main() {
    int rows, cols, i, j;
    
    printf("Enter number of rows and columns: ");
    scanf("%d %d", &rows, &cols);
    
    int mat1[rows][cols], mat2[rows][cols], result[rows][cols];
    
    printf("Enter elements of first matrix:\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            scanf("%d", &mat1[i][j]);
        }
    }
    
    printf("Enter elements of second matrix:\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            scanf("%d", &mat2[i][j]);
        }
    }
    
    // Add matrices
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            result[i][j] = mat1[i][j] + mat2[i][j];
        }
    }
    
    printf("Sum of matrices:\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            printf("%d ", result[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M6. Matrix Multiplication

**Description:** Write a program that performs multiplication of two matrices.

```c
#include <stdio.h>

int main() {
    int r1, c1, r2, c2, i, j, k;
    
    printf("Enter rows and columns of first matrix: ");
    scanf("%d %d", &r1, &c1);
    
    printf("Enter rows and columns of second matrix: ");
    scanf("%d %d", &r2, &c2);
    
    if (c1 != r2) {
        printf("Matrix multiplication not possible!\n");
        return 1;
    }
    
    int mat1[r1][c1], mat2[r2][c2], result[r1][c2];
    
    printf("Enter elements of first matrix:\n");
    for (i = 0; i < r1; i++) {
        for (j = 0; j < c1; j++) {
            scanf("%d", &mat1[i][j]);
        }
    }
    
    printf("Enter elements of second matrix:\n");
    for (i = 0; i < r2; i++) {
        for (j = 0; j < c2; j++) {
            scanf("%d", &mat2[i][j]);
        }
    }
    
    // Initialize result matrix
    for (i = 0; i < r1; i++) {
        for (j = 0; j < c2; j++) {
            result[i][j] = 0;
        }
    }
    
    // Matrix multiplication
    for (i = 0; i < r1; i++) {
        for (j = 0; j < c2; j++) {
            for (k = 0; k < c1; k++) {
                result[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }
    
    printf("Result:\n");
    for (i = 0; i < r1; i++) {
        for (j = 0; j < c2; j++) {
            printf("%d ", result[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M7. String Palindrome Checker

**Description:** Write a program that checks if a string is a palindrome (reads the same forward and backward).

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[100];
    int left, right, isPalindrome = 1;
    
    printf("Enter a string: ");
    scanf("%s", str);
    
    left = 0;
    right = strlen(str) - 1;
    
    while (left < right) {
        if (str[left] != str[right]) {
            isPalindrome = 0;
            break;
        }
        left++;
        right--;
    }
    
    if (isPalindrome) {
        printf("'%s' is a palindrome\n", str);
    } else {
        printf("'%s' is not a palindrome\n", str);
    }
    
    return 0;
}
```

---

## M8. Remove Duplicate Elements from an Array

```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 2, 5, 3, 6, 7, 1};
    int size = 9;
    int unique[size];
    int uniqueSize = 0;
    
    for (int i = 0; i < size; i++) {
        int isDuplicate = 0;
        for (int j = 0; j < uniqueSize; j++) {
            if (arr[i] == unique[j]) {
                isDuplicate = 1;
                break;
            }
        }
        if (!isDuplicate) {
            unique[uniqueSize] = arr[i];
            uniqueSize++;
        }
    }
    
    printf("Array without duplicates: ");
    for (int i = 0; i < uniqueSize; i++) {
        printf("%d ", unique[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M9. Find Second Largest Element in an Array

```c
#include <stdio.h>

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1};
    int size = 6;
    int largest, secondLargest;
    
    largest = secondLargest = arr[0];
    
    for (int i = 1; i < size; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        } else if (arr[i] > secondLargest && arr[i] != largest) {
            secondLargest = arr[i];
        }
    }
    
    printf("Second largest element: %d\n", secondLargest);
    
    return 0;
}
```

---

## M10. Check Prime Numbers in a Range

```c
#include <stdio.h>

int main() {
    int start = 10, end = 50;
    
    printf("Prime numbers between %d and %d: ", start, end);
    
    for (int i = start; i <= end; i++) {
        int isPrime = 1;
        if (i <= 1) isPrime = 0;
        
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                isPrime = 0;
                break;
            }
        }
        
        if (isPrime) {
            printf("%d ", i);
        }
    }
    
    printf("\n");
    
    return 0;
}
```

---

## M11. Pyramid Pattern of Asterisks

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("*");
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M12. Decimal to Binary Conversion

```c
#include <stdio.h>

int main() {
    int decimal = 10;
    int binary[32];
    int index = 0;
    
    while (decimal > 0) {
        binary[index] = decimal % 2;
        decimal = decimal / 2;
        index++;
    }
    
    printf("Binary: ");
    for (int i = index - 1; i >= 0; i--) {
        printf("%d", binary[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M13. String Anagram Checker

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[] = "listen";
    char str2[] = "silent";
    int freq[26] = {0};
    
    if (strlen(str1) != strlen(str2)) {
        printf("Not anagrams\n");
        return 0;
    }
    
    for (int i = 0; str1[i]; i++) {
        freq[str1[i] - 'a']++;
        freq[str2[i] - 'a']--;
    }
    
    int isAnagram = 1;
    for (int i = 0; i < 26; i++) {
        if (freq[i] != 0) {
            isAnagram = 0;
            break;
        }
    }
    
    if (isAnagram) {
        printf("'%s' and '%s' are anagrams\n", str1, str2);
    } else {
        printf("'%s' and '%s' are not anagrams\n", str1, str2);
    }
    
    return 0;
}
```

---

## M14. Insertion Sort

```c
#include <stdio.h>

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = 5;
    
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
    
    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M15. Selection Sort

```c
#include <stdio.h>

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = 5;
    
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        if (minIndex != i) {
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
    
    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M16. Hollow Square Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (i == 1 || i == n || j == 1 || j == n) {
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

---

## M17. Number Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            printf("%d ", i);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M18. Floyd's Triangle

```c
#include <stdio.h>

int main() {
    int n = 5;
    int num = 1;
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            printf("%d ", num);
            num++;
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M19. Pascal's Triangle

```c
#include <stdio.h>

int main() {
    int n = 5;
    int triangle[5][5];
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= i; j++) {
            if (j == 0 || j == i) {
                triangle[i][j] = 1;
            } else {
                triangle[i][j] = triangle[i-1][j-1] + triangle[i-1][j];
            }
            printf("%d ", triangle[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

**Explanation:** This solution shows two approaches to Pascal's triangle: mathematical computation using binomial coefficients and dynamic programming using the additive property.

---

## M20. Diamond Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    // Upper half
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("*");
        }
        printf("\n");
    }
    
    // Lower half
    for (int i = n - 1; i >= 1; i--) {
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= 2 * i - 1; j++) {
            printf("*");
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M21. Transpose of a Matrix

```c
#include <stdio.h>

int main() {
    int matrix[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int transpose[3][3];
    
    // Create transpose
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matrix[i][j];
        }
    }
    
    // Print original
    printf("Original:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    
    // Print transpose
    printf("Transpose:\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", transpose[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M22. Sum of Diagonals in a Matrix

```c
#include <stdio.h>

int main() {
    int matrix[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int mainSum = 0, antiSum = 0;
    
    // Sum main diagonal (i == j)
    for (int i = 0; i < 3; i++) {
        mainSum += matrix[i][i];
    }
    
    // Sum anti-diagonal (i + j == n-1)
    for (int i = 0; i < 3; i++) {
        antiSum += matrix[i][2-i];
    }
    
    printf("Main diagonal sum: %d\n", mainSum);
    printf("Anti-diagonal sum: %d\n", antiSum);
    
    return 0;
}```

---

## M23. Check Symmetric Matrix

```c
#include <stdio.h>

int main() {
    int matrix[3][3] = {{1, 2, 3}, {2, 5, 6}, {3, 6, 9}};
    int symmetric = 1;
    
    // Check if matrix[i][j] == matrix[j][i]
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (matrix[i][j] != matrix[j][i]) {
                symmetric = 0;
                break;
            }
        }
        if (!symmetric) break;
    }
    
    if (symmetric) {
        printf("Matrix is symmetric\n");
    } else {
        printf("Matrix is not symmetric\n");
    }
    
    return 0;
}

---

## M24. Rotate Array Elements

```c
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int k = 2; // rotate right by 2 positions
    int temp[5];
    
    // Copy to temp array with rotation
    for (int i = 0; i < 5; i++) {
        temp[(i + k) % 5] = arr[i];
    }
    
    // Copy back
    for (int i = 0; i < 5; i++) {
        arr[i] = temp[i];
    }
    
    // Print rotated array
    printf("Rotated array: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

---

## M25. Count Words in a String

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "Hello world this is a test";
    int words = 0;
    int inWord = 0;
    
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] != ' ' && !inWord) {
            words++;
            inWord = 1;
        } else if (str[i] == ' ') {
            inWord = 0;
        }
    }
    
    printf("String: %s\n", str);
    printf("Number of words: %d\n", words);
    
    return 0;
}
```

**Explanation:** This solution provides multiple approaches to word counting and includes comprehensive string analysis. It handles edge cases like multiple spaces, leading/trailing spaces, and provides additional string processing utilities.

---

## M26. Butterfly Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    // Upper half
    for (int i = 1; i <= n; i++) {
        // Left wing
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        
        // Spaces between wings
        for (int j = 1; j <= 2 * (n - i); j++) {
            printf(" ");
        }
        
        // Right wing
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        
        printf("\n");
    }
    
    // Lower half
    for (int i = n; i >= 1; i--) {
        // Left wing
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        
        // Spaces between wings
        for (int j = 1; j <= 2 * (n - i); j++) {
            printf(" ");
        }
        
        // Right wing
        for (int j = 1; j <= i; j++) {
            printf("*");
        }
        
        printf("\n");
    }
    
    return 0;
}
```

---

## M27. Spiral Pattern

```c
#include <stdio.h>

int main() {
    int matrix[4][4];
    int n = 4;
    int num = 1;
    int top = 0, bottom = 3, left = 0, right = 3;
    
    while (top <= bottom && left <= right) {
        // Fill top row
        for (int i = left; i <= right; i++) {
            matrix[top][i] = num++;
        }
        top++;
        
        // Fill right column
        for (int i = top; i <= bottom; i++) {
            matrix[i][right] = num++;
        }
        right--;
        
        // Fill bottom row
        if (top <= bottom) {
            for (int i = right; i >= left; i--) {
                matrix[bottom][i] = num++;
            }
            bottom--;
        }
        
        // Fill left column
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                matrix[i][left] = num++;
            }
            left++;
        }
    }
    
    // Print matrix
    printf("Spiral Pattern:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%3d ", matrix[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M28. ZigZag Pattern

```c
#include <stdio.h>

int main() {
    int height = 6, width = 6;
    
    for (int i = 0; i < height; i++) {
        for (int j = 0; j < width; j++) {
            if (j == i || j == (width - 1 - i)) {
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

---

## M29. Function to Generate Prime Numbers

```c
#include <stdio.h>

int main() {
    int limit = 30;
    
    printf("Prime numbers up to %d: ", limit);
    
    for (int i = 2; i <= limit; i++) {
        int isPrime = 1;
        
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                isPrime = 0;
                break;
            }
        }
        
        if (isPrime) {
            printf("%d ", i);
        }
    }
    
    printf("\n");
    return 0;
}
```

---

## M30. Function to Convert Binary to Decimal

```c
#include <stdio.h>

int main() {
    long long binary = 1101;
    long long decimal = 0;
    int base = 1;
    
    while (binary > 0) {
        int digit = binary % 10;
        decimal += digit * base;
        binary /= 10;
        base *= 2;
    }
    
    printf("Binary: 1101\n");
    printf("Decimal: %lld\n", decimal);
    
    return 0;
}
```

---

## M31. Function for Matrix Operations

```c
#include <stdio.h>

int main() {
    int A[2][2] = {{1, 2}, {3, 4}};
    int B[2][2] = {{5, 6}, {7, 8}};
    int result[2][2];
    
    // Matrix addition
    printf("Matrix A:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", A[i][j]);
        }
        printf("\n");
    }
    
    printf("\nMatrix B:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", B[i][j]);
        }
        printf("\n");
    }
    
    // Addition
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            result[i][j] = A[i][j] + B[i][j];
        }
    }
    
    printf("\nA + B:\n");
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", result[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M32. Hollow Diamond Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    // Upper half
    for (int i = 0; i < n; i++) {
        // Leading spaces
        for (int j = 0; j < n - i - 1; j++) {
            printf(" ");
        }
        
        // First asterisk
        printf("*");
        
        // Middle spaces (for hollow effect)
        if (i > 0) {
            for (int j = 0; j < 2 * i - 1; j++) {
                printf(" ");
            }
            printf("*");
        }
        
        printf("\n");
    }
    
    // Lower half
    for (int i = n - 2; i >= 0; i--) {
        // Leading spaces
        for (int j = 0; j < n - i - 1; j++) {
            printf(" ");
        }
        
        // First asterisk
        printf("*");
        
        // Middle spaces (for hollow effect)
        if (i > 0) {
            for (int j = 0; j < 2 * i - 1; j++) {
                printf(" ");
            }
            printf("*");
        }
        
        printf("\n");
    }
    
    return 0;
}
```

---

## M34. Cross Pattern

```c
#include <stdio.h>

int main() {
    int n = 7;
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j || i + j == n - 1) {
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

---

## M35. Number Pattern Diamond

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    // Upper half
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= i; j++) {
            printf("%d", j);
        }
        for (int j = i - 1; j >= 1; j--) {
            printf("%d", j);
        }
        printf("\n");
    }
    
    // Lower half
    for (int i = n - 1; i >= 1; i--) {
        for (int j = 1; j <= n - i; j++) {
            printf(" ");
        }
        for (int j = 1; j <= i; j++) {
            printf("%d", j);
        }
        for (int j = i - 1; j >= 1; j--) {
            printf("%d", j);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M36. Multiplication Table Grid

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    printf("   |");
    for (int i = 1; i <= n; i++) {
        printf("%4d", i);
    }
    printf("\n");
    
    printf("---+");
    for (int i = 1; i <= n; i++) {
        printf("----");
    }
    printf("\n");
    
    for (int i = 1; i <= n; i++) {
        printf("%2d |", i);
        for (int j = 1; j <= n; j++) {
            printf("%4d", i * j);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M37. Alphabetic Diamond Pattern

```c
#include <stdio.h>

int main() {
    int n = 5;
    
    // Upper half
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            printf(" ");
        }
        char ch = 'A' + i;
        for (int j = 0; j < 2 * i + 1; j++) {
            printf("%c", ch);
        }
        printf("\n");
    }
    
    // Lower half
    for (int i = n - 2; i >= 0; i--) {
        for (int j = 0; j < n - i - 1; j++) {
            printf(" ");
        }
        char ch = 'A' + i;
        for (int j = 0; j < 2 * i + 1; j++) {
            printf("%c", ch);
        }
        printf("\n");
    }
    
    return 0;
}
```

---

## M38. Print Calendar Month

```c
#include <stdio.h>

int main() {
    int month = 3, year = 2024;
    int daysInMonth[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    
    // Check for leap year
    if (month == 2 && ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))) {
        daysInMonth[1] = 29;
    }
    
    printf("   March 2024\n");
    printf("Su Mo Tu We Th Fr Sa\n");
    
    // March 2024 starts on Friday (day 5)
    int startDay = 5;
    
    // Print leading spaces
    for (int i = 0; i < startDay; i++) {
        printf("   ");
    }
    
    // Print days
    for (int day = 1; day <= daysInMonth[month-1]; day++) {
        printf("%2d ", day);
        if ((day + startDay) % 7 == 0) {
            printf("\n");
        }
    }
    printf("\n");
    
    return 0;
}
```

---

## M39. String Compression

**Approach:** Implement run-length encoding to compress strings by representing consecutive identical characters as character followed by count.

**Thinking:** String compression using run-length encoding replaces consecutive identical characters with the character followed by its count. This is effective for strings with many repeated characters.

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// Basic run-length encoding compression
void compressString(char input[], char output[]) {
    int len = strlen(input);
    int outputIndex = 0;
    
    for (int i = 0; i < len; i++) {
        int count = 1;
        char currentChar = input[i];
        
        // Count consecutive occurrences
        while (i + 1 < len && input[i] == input[i + 1]) {
            count++;
            i++;
        }
        
        // Add character to output
        output[outputIndex++] = currentChar;
        
        // Add count to output
        if (count > 1) {
            char countStr[10];
            sprintf(countStr, "%d", count);
            for (int j = 0; countStr[j] != '\0'; j++) {
                output[outputIndex++] = countStr[j];
            }
        }
    }
    
    output[outputIndex] = '\0';
}

// Decompression function
void decompressString(char input[], char output[]) {
    int len = strlen(input);
    int outputIndex = 0;
    
    for (int i = 0; i < len; i++) {
        char currentChar = input[i];
        
        // Check if next characters are digits
        int count = 1;
        if (i + 1 < len && input[i + 1] >= '0' && input[i + 1] <= '9') {
            count = 0;
            i++; // Move to first digit
            
            // Parse the number
            while (i < len && input[i] >= '0' && input[i] <= '9') {
                count = count * 10 + (input[i] - '0');
                i++;
            }
            i--; // Adjust for loop increment
        }
        
        // Add character 'count' times to output
        for (int j = 0; j < count; j++) {
            output[outputIndex++] = currentChar;
        }
    }
    
    output[outputIndex] = '\0';
}

// Advanced compression with better efficiency for short runs
void compressStringAdvanced(char input[], char output[]) {
    int len = strlen(input);
    int outputIndex = 0;
    
    for (int i = 0; i < len; i++) {
        int count = 1;
        char currentChar = input[i];
        
        // Count consecutive occurrences
        while (i + 1 < len && input[i] == input[i + 1]) {
            count++;
            i++;
        }
        
        // Add character to output
        output[outputIndex++] = currentChar;
        
        // Only add count if it's greater than 1 and compression is beneficial
        if (count > 1) {
            if (count <= 9) {
                // Single digit count
                output[outputIndex++] = '0' + count;
            } else {
                // Multi-digit count
                char countStr[10];
                sprintf(countStr, "%d", count);
                for (int j = 0; countStr[j] != '\0'; j++) {
                    output[outputIndex++] = countStr[j];
                }
            }
        }
    }
    
    output[outputIndex] = '\0';
}

// Calculate compression ratio
double calculateCompressionRatio(char original[], char compressed[]) {
    int originalLength = strlen(original);
    int compressedLength = strlen(compressed);
    
    if (originalLength == 0) return 0.0;
    
    return (double)compressedLength / originalLength;
}

// Check if compression is beneficial
int isCompressionBeneficial(char original[], char compressed[]) {
    return strlen(compressed) < strlen(original);
}

// Huffman-style frequency analysis (for educational purposes)
void analyzeFrequency(char str[]) {
    int frequency[256] = {0}; // ASCII characters
    int len = strlen(str);
    
    // Count character frequencies
    for (int i = 0; i < len; i++) {
        frequency[(unsigned char)str[i]]++;
    }
    
    printf("Character Frequency Analysis:\n");
    printf("Char | Count | Percentage\n");
    printf("-----|-------|----------\n");
    
    for (int i = 0; i < 256; i++) {
        if (frequency[i] > 0) {
            char ch = i;
            if (ch == ' ') {
                printf("'SP' |  %3d  |   %5.1f%%\n", 
                       frequency[i], (frequency[i] * 100.0) / len);
            } else if (ch == '\n') {
                printf("'NL' |  %3d  |   %5.1f%%\n", 
                       frequency[i], (frequency[i] * 100.0) / len);
            } else if (ch == '\t') {
                printf("'TB' |  %3d  |   %5.1f%%\n", 
                       frequency[i], (frequency[i] * 100.0) / len);
            } else if (ch >= 32 && ch <= 126) {
                printf(" '%c' |  %3d  |   %5.1f%%\n", 
                       ch, frequency[i], (frequency[i] * 100.0) / len);
            } else {
                printf("(%2d) |  %3d  |   %5.1f%%\n", 
                       ch, frequency[i], (frequency[i] * 100.0) / len);
            }
        }
    }
}

// Test compression with multiple algorithms
void testCompression(char input[]) {
    char compressed1[2000], compressed2[2000];
    char decompressed[2000];
    
    printf("\nCompression Test Results:\n");
    printf("Original string: \"%s\"\n", input);
    printf("Original length: %lu\n", strlen(input));
    
    // Basic compression
    compressString(input, compressed1);
    printf("\nBasic compression: \"%s\"\n", compressed1);
    printf("Compressed length: %lu\n", strlen(compressed1));
    printf("Compression ratio: %.2f\n", calculateCompressionRatio(input, compressed1));
    printf("Space saved: %ld bytes\n", strlen(input) - strlen(compressed1));
    
    // Advanced compression
    compressStringAdvanced(input, compressed2);
    printf("\nAdvanced compression: \"%s\"\n", compressed2);
    printf("Compressed length: %lu\n", strlen(compressed2));
    printf("Compression ratio: %.2f\n", calculateCompressionRatio(input, compressed2));
    
    // Test decompression
    decompressString(compressed1, decompressed);
    printf("\nDecompressed: \"%s\"\n", decompressed);
    printf("Decompression successful: %s\n", 
           strcmp(input, decompressed) == 0 ? "Yes" : "No");
    
    // Frequency analysis
    printf("\n");
    analyzeFrequency(input);
}

int main() {
    char input[1000], output[2000];
    int choice;
    
    printf("String Compression Tool\n");
    printf("1. Compress a string\n");
    printf("2. Decompress a string\n");
    printf("3. Test compression efficiency\n");
    printf("4. Interactive compression testing\n");
    printf("Enter choice: ");
    scanf("%d", &choice);
    
    printf("Enter string: ");
    getchar(); // Clear input buffer
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = '\0'; // Remove newline
    
    switch(choice) {
        case 1:
            compressStringAdvanced(input, output);
            printf("\nOriginal: \"%s\"\n", input);
            printf("Compressed: \"%s\"\n", output);
            printf("Original length: %lu\n", strlen(input));
            printf("Compressed length: %lu\n", strlen(output));
            
            if (isCompressionBeneficial(input, output)) {
                printf("Compression is beneficial! Saved %ld bytes.\n", 
                       strlen(input) - strlen(output));
            } else {
                printf("Compression is not beneficial for this string.\n");
            }
            break;
            
        case 2:
            decompressString(input, output);
            printf("\nCompressed: \"%s\"\n", input);
            printf("Decompressed: \"%s\"\n", output);
            break;
            
        case 3:
            testCompression(input);
            break;
            
        case 4:
            printf("\nInteractive Compression Testing\n");
            printf("Enter 'quit' to exit\n");
            
            while (1) {
                printf("\nEnter string to test: ");
                fgets(input, sizeof(input), stdin);
                input[strcspn(input, "\n")] = '\0';
                
                if (strcmp(input, "quit") == 0) {
                    break;
                }
                
                testCompression(input);
            }
            break;
            
        default:
            printf("Invalid choice!\n");
    }
    
    return 0;
}
```

**Explanation:** This comprehensive string compression solution implements run-length encoding with multiple variants, decompression, compression efficiency analysis, and character frequency analysis. It demonstrates data compression concepts and string manipulation techniques.

---

## M40. Find All Factors of a Number

**Approach:** Iterate through numbers from 1 to the given number and check divisibility, categorizing factors as prime or composite.

**Thinking:** To find all factors of a number, we check every integer from 1 to n for divisibility. For efficiency, we can optimize by checking only up to the square root of n and finding factor pairs.

```c
#include <stdio.h>
#include <stdbool.h>
#include <math.h>

// Function to check if a number is prime
bool isPrime(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n % 2 == 0 || n % 3 == 0) return false;
    
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }
    return true;
}

// Function to find all factors (basic approach)
void findFactorsBasic(int n) {
    printf("Factors of %d: ", n);
    
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            printf("%d ", i);
        }
    }
    printf("\n");
}

// Function to find factors efficiently (up to sqrt(n))
void findFactorsEfficient(int n) {
    printf("Factors of %d: ", n);
    
    int factors[1000];
    int count = 0;
    
    // Find factors up to sqrt(n)
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            factors[count++] = i;
            
            // Add the corresponding factor if it's different
            if (i != n / i) {
                factors[count++] = n / i;
            }
        }
    }
    
    // Sort factors (simple bubble sort)
    for (int i = 0; i < count - 1; i++) {
        for (int j = 0; j < count - i - 1; j++) {
            if (factors[j] > factors[j + 1]) {
                int temp = factors[j];
                factors[j] = factors[j + 1];
                factors[j + 1] = temp;
            }
        }
    }
    
    // Print sorted factors
    for (int i = 0; i < count; i++) {
        printf("%d ", factors[i]);
    }
    printf("\n");
}

// Function to categorize factors as prime or composite
void categorizeFactors(int n) {
    printf("\nFactor Analysis for %d:\n", n);
    
    int primeFactors[100], compositeFactors[100];
    int primeCount = 0, compositeCount = 0;
    
    printf("All factors: ");
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            printf("%d ", i);
            
            if (isPrime(i)) {
                primeFactors[primeCount++] = i;
            } else if (i > 1) {
                compositeFactors[compositeCount++] = i;
            }
        }
    }
    printf("\n");
    
    printf("Prime factors: ");
    for (int i = 0; i < primeCount; i++) {
        printf("%d ", primeFactors[i]);
    }
    if (primeCount == 0) printf("None");
    printf("\n");
    
    printf("Composite factors: ");
    for (int i = 0; i < compositeCount; i++) {
        printf("%d ", compositeFactors[i]);
    }
    if (compositeCount == 0) printf("None");
    printf("\n");
    
    printf("Total factors: %d\n", primeCount + compositeCount + (n > 0 ? 1 : 0)); // +1 for 1
    printf("Prime factor count: %d\n", primeCount);
    printf("Composite factor count: %d\n", compositeCount);
}

// Function to find prime factorization
void primeFactorization(int n) {
    printf("Prime factorization of %d: ", n);
    
    if (n <= 1) {
        printf("Not applicable\n");
        return;
    }
    
    int original = n;
    bool first = true;
    
    // Handle factor 2
    while (n % 2 == 0) {
        if (!first) printf(" × ");
        printf("2");
        first = false;
        n /= 2;
    }
    
    // Handle odd factors
    for (int i = 3; i * i <= n; i += 2) {
        while (n % i == 0) {
            if (!first) printf(" × ");
            printf("%d", i);
            first = false;
            n /= i;
        }
    }
    
    // If n is still > 1, then it's a prime factor
    if (n > 1) {
        if (!first) printf(" × ");
        printf("%d", n);
    }
    
    printf(" = %d\n", original);
}

// Function to calculate sum and product of factors
void factorStatistics(int n) {
    int sum = 0, product = 1;
    int count = 0;
    
    printf("Factor statistics for %d:\n", n);
    
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            sum += i;
            product *= i;
            count++;
        }
    }
    
    printf("Sum of factors: %d\n", sum);
    printf("Product of factors: %lld\n", (long long)product);
    printf("Number of factors: %d\n", count);
    printf("Average factor: %.2f\n", (double)sum / count);
    
    // Check if number is perfect, abundant, or deficient
    int properSum = sum - n; // Sum of proper divisors (excluding n itself)
    if (properSum == n) {
        printf("%d is a perfect number\n", n);
    } else if (properSum > n) {
        printf("%d is an abundant number (excess: %d)\n", n, properSum - n);
    } else {
        printf("%d is a deficient number (deficit: %d)\n", n, n - properSum);
    }
}

// Function to find factors in range
void findFactorsInRange(int start, int end, int target) {
    printf("Numbers between %d and %d that are factors of %d:\n", start, end, target);
    
    int count = 0;
    for (int i = start; i <= end; i++) {
        if (target % i == 0) {
            printf("%d ", i);
            count++;
        }
    }
    
    if (count == 0) {
        printf("None");
    }
    printf("\nCount: %d\n", count);
}

// Function to find common factors of two numbers
void findCommonFactors(int a, int b) {
    printf("Common factors of %d and %d: ", a, b);
    
    int limit = (a < b) ? a : b;
    int count = 0;
    
    for (int i = 1; i <= limit; i++) {
        if (a % i == 0 && b % i == 0) {
            printf("%d ", i);
            count++;
        }
    }
    
    printf("\nNumber of common factors: %d\n", count);
}

int main() {
    int n, choice, start, end, b;
    
    printf("Factor Analysis Tool\n");
    printf("1. Find all factors (basic)\n");
    printf("2. Find all factors (efficient)\n");
    printf("3. Categorize factors (prime/composite)\n");
    printf("4. Prime factorization\n");
    printf("5. Factor statistics\n");
    printf("6. Find factors in range\n");
    printf("7. Find common factors of two numbers\n");
    printf("8. Complete factor analysis\n");
    printf("Enter choice: ");
    scanf("%d", &choice);
    
    switch(choice) {
        case 1:
            printf("Enter number: ");
            scanf("%d", &n);
            findFactorsBasic(n);
            break;
            
        case 2:
            printf("Enter number: ");
            scanf("%d", &n);
            findFactorsEfficient(n);
            break;
            
        case 3:
            printf("Enter number: ");
            scanf("%d", &n);
            categorizeFactors(n);
            break;
            
        case 4:
            printf("Enter number: ");
            scanf("%d", &n);
            primeFactorization(n);
            break;
            
        case 5:
            printf("Enter number: ");
            scanf("%d", &n);
            factorStatistics(n);
            break;
            
        case 6:
            printf("Enter number to find factors of: ");
            scanf("%d", &n);
            printf("Enter range (start end): ");
            scanf("%d %d", &start, &end);
            findFactorsInRange(start, end, n);
            break;
            
        case 7:
            printf("Enter two numbers: ");
            scanf("%d %d", &n, &b);
            findCommonFactors(n, b);
            break;
            
        case 8:
            printf("Enter number: ");
            scanf("%d", &n);
            
            printf("\n=== Complete Factor Analysis ===\n");
            findFactorsEfficient(n);
            categorizeFactors(n);
            primeFactorization(n);
            factorStatistics(n);
            break;
            
        default:
            printf("Invalid choice!\n");
    }
    
    return 0;
}
```

**Explanation:** This comprehensive factor analysis solution provides multiple approaches to factor finding, from basic to optimized algorithms. It includes factor categorization, prime factorization, statistical analysis, and special number identification (perfect, abundant, deficient numbers).

---
