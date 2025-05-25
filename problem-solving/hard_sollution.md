# Hard Level Problem Solutions

## H1. Implement Stack Data Structure

**Approach:** Simple array-based stack with push, pop, and display operations.

**Thinking:** Use array with top pointer to track current position.

```c
#include <stdio.h>
#define MAX 5

int stack[MAX];
int top = -1;

void push(int value) {
    if (top >= MAX - 1) {
        printf("Stack overflow\n");
        return;
    }
    stack[++top] = value;
    printf("Pushed: %d\n", value);
}

int pop() {
    if (top < 0) {
        printf("Stack underflow\n");
        return -1;
    }
    return stack[top--];
}

void display() {
    if (top < 0) {
        printf("Stack is empty\n");
        return;
    }
    printf("Stack: ");
    for (int i = 0; i <= top; i++) {
        printf("%d ", stack[i]);
    }
    printf("\n");
}

int main() {
    push(10);
    push(20);
    push(30);
    display();
    
    printf("Popped: %d\n", pop());
    display();
    
    return 0;
}
```

**Explanation:** Simple stack implementation with basic push, pop, and display operations.

---

## H2. Implement Queue Data Structure

**Approach:** Simple circular queue with enqueue, dequeue, and display operations.

**Thinking:** Use circular buffer to prevent shifting elements, track front and rear pointers.

```c
#include <stdio.h>
#define MAX 5

int queue[MAX];
int front = -1, rear = -1;

void enqueue(int value) {
    if ((rear + 1) % MAX == front) {
        printf("Queue overflow\n");
        return;
    }
    if (front == -1) front = 0;
    rear = (rear + 1) % MAX;
    queue[rear] = value;
    printf("Enqueued: %d\n", value);
}

int dequeue() {
    if (front == -1) {
        printf("Queue underflow\n");
        return -1;
    }
    int value = queue[front];
    if (front == rear) {
        front = rear = -1;
    } else {
        front = (front + 1) % MAX;
    }
    return value;
}

void display() {
    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }
    printf("Queue: ");
    int i = front;
    while (i != rear) {
        printf("%d ", queue[i]);
        i = (i + 1) % MAX;
    }
    printf("%d\n", queue[rear]);
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    display();
    
    printf("Dequeued: %d\n", dequeue());
    display();
    
    return 0;
}
```

**Explanation:** Simple circular queue implementation with basic enqueue, dequeue, and display operations.

---

## H3. Merge Sort

**Approach:** Divide array in half, sort each half, then merge sorted halves.

**Thinking:** Recursive divide-and-conquer algorithm with O(n log n) time complexity.

```c
#include <stdio.h>

void merge(int arr[], int left, int mid, int right) {
    int i, j, k;
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    int L[n1], R[n2];
    
    for (i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    i = 0; j = 0; k = left;
    
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    while (i < n1) {
        arr[k] = L[i];
        i++; k++;
    }
    
    while (j < n2) {
        arr[k] = R[j];
        j++; k++;
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    printf("Original array: ");
    printArray(arr, n);
    
    mergeSort(arr, 0, n - 1);
    
    printf("Sorted array: ");
    printArray(arr, n);
    
    return 0;
}
```

**Explanation:** Basic merge sort implementation using divide-and-conquer approach.

---

## H4. Quick Sort

**Approach:** Partition array around pivot element and recursively sort subarrays.

**Thinking:** Choose pivot, partition array so smaller elements are on left, larger on right.

```c
#include <stdio.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    printf("Original array: ");
    printArray(arr, n);
    
    quickSort(arr, 0, n - 1);
    
    printf("Sorted array: ");
    printArray(arr, n);
    
    return 0;
}
```

**Explanation:** Basic quick sort with partition function and recursive sorting.

---

## H5. Implement Linked List

**Approach:** Simple singly linked list with insert, delete, and display operations.

**Thinking:** Use nodes with data and next pointer, maintain head pointer to track list.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct {
    Node* head;
} LinkedList;

void initList(LinkedList* list) {
    list->head = NULL;
}

Node* createNode(int data) {
    Node* newNode = malloc(sizeof(Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

void insertAtBeginning(LinkedList* list, int data) {
    Node* newNode = createNode(data);
    newNode->next = list->head;
    list->head = newNode;
    printf("Inserted %d at beginning\n", data);
}

void insertAtEnd(LinkedList* list, int data) {
    Node* newNode = createNode(data);
    
    if (list->head == NULL) {
        list->head = newNode;
    } else {
        Node* current = list->head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }
    printf("Inserted %d at end\n", data);
}

void deleteValue(LinkedList* list, int value) {
    if (list->head == NULL) {
        printf("List is empty\n");
        return;
    }
    
    if (list->head->data == value) {
        Node* temp = list->head;
        list->head = list->head->next;
        free(temp);
        printf("Deleted %d\n", value);
        return;
    }
    
    Node* current = list->head;
    while (current->next != NULL && current->next->data != value) {
        current = current->next;
    }
    
    if (current->next != NULL) {
        Node* temp = current->next;
        current->next = temp->next;
        free(temp);
        printf("Deleted %d\n", value);
    }
}

void display(LinkedList* list) {
    if (list->head == NULL) {
        printf("List is empty\n");
        return;
    }
    
    printf("List: ");
    Node* current = list->head;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
    printf("\n");
}

void freeList(LinkedList* list) {
    Node* current = list->head;
    while (current != NULL) {
        Node* temp = current;
        current = current->next;
        free(temp);
    }

int main() {
    LinkedList list;
    initList(&list);
    
    insertAtEnd(&list, 10);
    insertAtEnd(&list, 20);
    insertAtBeginning(&list, 5);
    display(&list);
    
    deleteValue(&list, 20);
    display(&list);
    
    freeList(&list);
    return 0;
}
```

**Explanation:** Simple singly linked list with basic insert, delete, and display operations.

---

## H6. Recursive Maze Solver

**Approach:** Use backtracking to find a path through the maze.

**Thinking:** Try each direction recursively, backtrack if path leads to dead end.

```c
#include <stdio.h>

#define SIZE 5

int maze[SIZE][SIZE] = {
    {1, 0, 0, 0, 1},
    {1, 1, 0, 1, 1},
    {0, 1, 0, 0, 1},
    {1, 1, 1, 1, 1},
    {0, 0, 0, 0, 1}
};

int solution[SIZE][SIZE];

int solveMaze(int x, int y) {
    if (x == SIZE-1 && y == SIZE-1 && maze[x][y] == 1) {
        solution[x][y] = 1;
        return 1;
    }
    
    if (x >= 0 && y >= 0 && x < SIZE && y < SIZE && maze[x][y] == 1) {
        solution[x][y] = 1;
        
        if (solveMaze(x+1, y)) return 1;
        if (solveMaze(x, y+1)) return 1;
        
        solution[x][y] = 0;
    }
    return 0;
}

void printSolution() {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%d ", solution[i][j]);
        }
        printf("\n");
    }
}

int main() {
    if (solveMaze(0, 0)) {
        printf("Solution exists:\n");
        printSolution();
    } else {
        printf("No solution exists\n");
    }
    return 0;
}
```

**Explanation:** Simple recursive backtracking to find path from top-left to bottom-right.

---

## H7. Binary Search Tree

**Approach:** Implement BST with insert, delete, and traversal operations.

**Thinking:** BST maintains ordering property - left subtree < root < right subtree.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
} Node;

Node* createNode(int data) {
    Node* newNode = malloc(sizeof(Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

Node* insert(Node* root, int data) {
    if (root == NULL) return createNode(data);
    
    if (data < root->data)
        root->left = insert(root->left, data);
    else
        root->right = insert(root->right, data);
    
    return root;
}

Node* findMin(Node* root) {
    while (root->left) root = root->left;
    return root;
}

Node* delete(Node* root, int data) {
    if (root == NULL) return root;
    
    if (data < root->data)
        root->left = delete(root->left, data);
    else if (data > root->data)
        root->right = delete(root->right, data);
    else {
        if (root->left == NULL) {
            Node* temp = root->right;
            free(root);
            return temp;
        }
        if (root->right == NULL) {
            Node* temp = root->left;
            free(root);
            return temp;
        }
        
        Node* temp = findMin(root->right);
        root->data = temp->data;
        root->right = delete(root->right, temp->data);
    }
    return root;
}

void inorder(Node* root) {
    if (root) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 70);
    insert(root, 20);
    insert(root, 40);
    
    printf("Inorder: ");
    inorder(root);
    printf("\n");
    
    root = delete(root, 30);
    printf("After deleting 30: ");
    inorder(root);
    printf("\n");
    
    return 0;
}
```

**Explanation:** Basic BST with insert, delete, and inorder traversal operations.

---

## H8. N-Queens Problem

**Approach:** Use backtracking to place N queens on NxN chessboard.

**Thinking:** Place queens one by one in different rows, check if placement is safe.

```c
#include <stdio.h>
#include <stdbool.h>

#define N 4

int board[N][N];

bool isSafe(int row, int col) {
    for (int i = 0; i < col; i++)
        if (board[row][i]) return false;
    
    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j]) return false;
    
    for (int i = row, j = col; j >= 0 && i < N; i++, j--)
        if (board[i][j]) return false;
    
    return true;
}

bool solveNQueens(int col) {
    if (col >= N) {
        return true;  // All queens placed
    }
    
    for (int i = 0; i < N; i++) {
        if (isSafe(i, col)) {
            board[i][col] = 1;
            
            if (solveNQueens(col + 1)) {
                return true;
            }
            
            board[i][col] = 0;  // Backtrack
        }
    }
    return false;
}

void printBoard() {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            printf("%d ", board[i][j]);
        }
        printf("\n");
    }
}

int main() {
    if (solveNQueens(0)) {
        printf("Solution:\n");
        printBoard();
    } else {
        printf("No solution exists\n");
    }
    return 0;
}
```

**Explanation:** Backtracking solution to place N queens such that no two queens attack each other.

---

## H9. Palindrome Permutation Checker

**Approach:** Check if any permutation of string can form a palindrome.

**Thinking:** For palindrome, at most one character can have odd frequency.

```c
#include <stdio.h>
#include <string.h>

int canFormPalindrome(char* str) {
    int freq[256] = {0};
    int len = strlen(str);
    
    for (int i = 0; i < len; i++) {
        freq[str[i]]++;
    }
    
    int oddCount = 0;
    for (int i = 0; i < 256; i++) {
        if (freq[i] % 2 == 1) {
            oddCount++;
        }
    }
    
    return oddCount <= 1;
}

int main() {
    char str[100];
    printf("Enter string: ");
    scanf("%s", str);
    
    if (canFormPalindrome(str)) {
        printf("Can form palindrome\n");
    } else {
        printf("Cannot form palindrome\n");
    }
    
    return 0;
}
```

**Explanation:** Count character frequencies; palindrome possible if at most one character has odd frequency.

---

## H10. Tower of Hanoi

**Approach:** Recursive solution to move disks from source to destination.

**Thinking:** Move n-1 disks to auxiliary, move largest to destination, move n-1 from auxiliary to destination.

```c
#include <stdio.h>

void towerOfHanoi(int n, char from, char to, char aux) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", from, to);
        return;
    }
    
    towerOfHanoi(n-1, from, aux, to);
    printf("Move disk %d from %c to %c\n", n, from, to);
    towerOfHanoi(n-1, aux, to, from);
}

int main() {
    int n;
    printf("Enter number of disks: ");
    scanf("%d", &n);
    
    printf("Steps to solve Tower of Hanoi:\n");
    towerOfHanoi(n, 'A', 'C', 'B');
    
    return 0;
}
```

**Explanation:** Classic recursive problem - move n disks from rod A to rod C using rod B as auxiliary.

---

## H11. Recursive Binary Search

**Approach:** Divide array in half and search recursively.

**Thinking:** Compare with middle element, search left or right half based on comparison.

```c
#include <stdio.h>

int binarySearch(int arr[], int left, int right, int target) {
    if (right >= left) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) return mid;
        
        if (arr[mid] > target)
            return binarySearch(arr, left, mid - 1, target);
        
        return binarySearch(arr, mid + 1, right, target);
    }
    
    return -1;
}

int main() {
    int arr[] = {2, 3, 4, 10, 40, 50, 80};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target;
    
    printf("Enter target: ");
    scanf("%d", &target);
    
    int result = binarySearch(arr, 0, n - 1, target);
    
    if (result != -1)
        printf("Element found at index %d\n", result);
    else
        printf("Element not found\n");
    
    return 0;
}
```

**Explanation:** Recursive binary search with O(log n) time complexity on sorted array.

---

## H12. Longest Palindromic Substring

**Approach:** Expand around each possible center to find longest palindrome.

**Thinking:** Check each position as center and expand outward while characters match.

```c
#include <stdio.h>
#include <string.h>

int expandAroundCenter(char* s, int left, int right) {
    while (left >= 0 && right < strlen(s) && s[left] == s[right]) {
        left--;
        right++;
    }
    return right - left - 1;
}

void longestPalindrome(char* s) {
    int start = 0, maxLen = 1;
    int len = strlen(s);
    
    for (int i = 0; i < len; i++) {
        int len1 = expandAroundCenter(s, i, i);
        int len2 = expandAroundCenter(s, i, i + 1);
        int currentMax = (len1 > len2) ? len1 : len2;
        
        if (currentMax > maxLen) {
            maxLen = currentMax;
            start = i - (currentMax - 1) / 2;
        }
    }
    
    printf("Longest palindromic substring: ");
    for (int i = start; i < start + maxLen; i++) {
        printf("%c", s[i]);
    }
    printf("\n");
}

int main() {
    char s[100];
    printf("Enter string: ");
    scanf("%s", s);
    
    longestPalindrome(s);
    
    return 0;
}
```

**Explanation:** Expand around each center to find the longest palindromic substring.

---

## H13. Recursive String Reversal

**Approach:** Recursively swap characters from ends moving inward.

**Thinking:** Swap first and last characters, then recursively reverse the middle substring.

```c
#include <stdio.h>
#include <string.h>

void reverseString(char* str, int start, int end) {
    if (start >= end) return;
    
    char temp = str[start];
    str[start] = str[end];
    str[end] = temp;
    
    reverseString(str, start + 1, end - 1);
}

int main() {
    char str[100];
    printf("Enter string: ");
    scanf("%s", str);
    
    printf("Original: %s\n", str);
    
    reverseString(str, 0, strlen(str) - 1);
    
    printf("Reversed: %s\n", str);
    
    return 0;
}
```

**Explanation:** Recursive approach to reverse string by swapping characters from both ends.

---

## H14. Count Ways to Reach Nth Stair

**Approach:** Use dynamic programming with memoization.

**Thinking:** To reach stair n, we can come from stair n-1 or n-2.

```c
#include <stdio.h>

int memo[100];

int countWays(int n) {
    if (n <= 1) return 1;
    if (n == 2) return 2;
    
    if (memo[n] != -1) return memo[n];
    
    memo[n] = countWays(n-1) + countWays(n-2);
    return memo[n];
}

int main() {
    int n;
    printf("Enter number of stairs: ");
    scanf("%d", &n);
    
    for (int i = 0; i <= n; i++) {
        memo[i] = -1;
    }
    
    printf("Number of ways to reach %d stairs: %d\n", n, countWays(n));
    
    return 0;
}
```

**Explanation:** Dynamic programming solution with memoization to count ways to reach nth stair.

---

## H15. Heapsort Implementation

**Approach:** Build max heap and repeatedly extract maximum element.

**Thinking:** Use heap property to sort array in-place.

```c
#include <stdio.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    
    if (left < n && arr[left] > arr[largest])
        largest = left;
    
    if (right < n && arr[right] > arr[largest])
        largest = right;
    
    if (largest != i) {
        swap(&arr[i], &arr[largest]);
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
    
    for (int i = n - 1; i > 0; i--) {
        swap(&arr[0], &arr[i]);
        heapify(arr, i, 0);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    printf("Original array: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    
    heapSort(arr, n);
    
    printf("\nSorted array: ");
    for (int i = 0; i < n; i++) printf("%d ", arr[i]);
    printf("\n");
    
    return 0;
}
```

**Explanation:** Heap-based sorting algorithm with O(n log n) time complexity.

---

## H16. Huffman Coding

**Approach:** Build frequency table for basic Huffman coding demonstration.

**Thinking:** Count character frequencies as foundation for Huffman tree.

```c
#include <stdio.h>
#include <string.h>

void huffmanCoding(char* text) {
    int freq[256] = {0};
    int len = strlen(text);
    
    for (int i = 0; i < len; i++) {
        freq[text[i]]++;
    }
    
    printf("Character frequencies:\n");
    for (int i = 0; i < 256; i++) {
        if (freq[i] > 0) {
            printf("'%c': %d\n", i, freq[i]);
        }
    }
}

int main() {
    char text[100];
    printf("Enter text: ");
    fgets(text, sizeof(text), stdin);
    
    huffmanCoding(text);
    
    return 0;
}
```

**Explanation:** Basic frequency counting for Huffman coding implementation.

---

## H17. Red-Black Tree

**Approach:** Basic red-black tree structure demonstration.

**Thinking:** Self-balancing BST with color property for balance.

```c
#include <stdio.h>
#include <stdlib.h>

typedef enum { RED, BLACK } Color;

typedef struct Node {
    int data;
    Color color;
    struct Node* left;
    struct Node* right;
    struct Node* parent;
} Node;

Node* createNode(int data) {
    Node* node = malloc(sizeof(Node));
    node->data = data;
    node->color = RED;
    node->left = node->right = node->parent = NULL;
    return node;
}

void inorder(Node* root) {
    if (root) {
        inorder(root->left);
        printf("%d(%s) ", root->data, root->color == RED ? "R" : "B");
        inorder(root->right);
    }
}

int main() {
    Node* root = createNode(10);
    root->color = BLACK;
    root->left = createNode(5);
    root->right = createNode(15);
    
    printf("Red-Black Tree (simplified): ");
    inorder(root);
    printf("\n");
    
    return 0;
}
```

**Explanation:** Basic red-black tree structure with color properties.

---

## H18. Dynamic Memory Management

**Approach:** Simple malloc/free implementation demonstration.

**Thinking:** Basic memory allocation and deallocation simulation.

```c
#include <stdio.h>
#include <stdlib.h>

#define MEMORY_SIZE 1024

char memory[MEMORY_SIZE];
int allocated[MEMORY_SIZE] = {0};

void* myMalloc(int size) {
    for (int i = 0; i <= MEMORY_SIZE - size; i++) {
        int canAllocate = 1;
        for (int j = i; j < i + size; j++) {
            if (allocated[j]) {
                canAllocate = 0;
                break;
            }
        }
        
        if (canAllocate) {
            for (int j = i; j < i + size; j++) {
                allocated[j] = 1;
            }
            return &memory[i];
        }
    }
    return NULL;
}

void myFree(void* ptr, int size) {
    int index = (char*)ptr - memory;
    for (int i = index; i < index + size; i++) {
        allocated[i] = 0;
    }
}

int main() {
    void* ptr1 = myMalloc(100);
    void* ptr2 = myMalloc(50);
    
    printf("Allocated memory at: %p and %p\n", ptr1, ptr2);
    
    myFree(ptr1, 100);
    myFree(ptr2, 50);
    
    printf("Memory freed\n");
    
    return 0;
}
```

**Explanation:** Simplified memory management system with allocation and deallocation.

---

## H19. Dijkstra's Algorithm

**Approach:** Find shortest path in weighted graph using greedy approach.

**Thinking:** Always select unvisited vertex with minimum distance.

```c
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define V 5

int minDistance(int dist[], bool visited[]) {
    int min = INT_MAX, min_index;
    
    for (int v = 0; v < V; v++) {
        if (!visited[v] && dist[v] <= min) {
            min = dist[v];
            min_index = v;
        }
    }
    return min_index;
}

void dijkstra(int graph[V][V], int src) {
    int dist[V];
    bool visited[V];
    
    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
        visited[i] = false;
    }
    
    dist[src] = 0;
    
    for (int count = 0; count < V - 1; count++) {
        int u = minDistance(dist, visited);
        visited[u] = true;
        
        for (int v = 0; v < V; v++) {
            if (!visited[v] && graph[u][v] && dist[u] != INT_MAX && 
                dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }
    
    printf("Shortest distances from vertex %d:\n", src);
    for (int i = 0; i < V; i++) {
        printf("To vertex %d: %d\n", i, dist[i]);
    }
}

int main() {
    int graph[V][V] = {
        {0, 9, 0, 0, 0},
        {9, 0, 3, 0, 0},
        {0, 3, 0, 5, 4},
        {0, 0, 5, 0, 1},
        {0, 0, 4, 1, 0}
    };
    
    dijkstra(graph, 0);
    
    return 0;
}
```

**Explanation:** Dijkstra's algorithm to find shortest paths from source vertex to all other vertices.

---

## H20. A* Pathfinding

**Approach:** Use heuristic search with f(n) = g(n) + h(n).

**Thinking:** Combine actual cost and heuristic estimate for efficient pathfinding.

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define SIZE 5

typedef struct {
    int x, y;
    int f, g, h;
    struct Node* parent;
} Node;

int heuristic(int x1, int y1, int x2, int y2) {
    return abs(x1 - x2) + abs(y1 - y2);
}

int aStar(int grid[SIZE][SIZE], int startX, int startY, int goalX, int goalY) {
    Node* openList[SIZE * SIZE];
    int openSize = 0;
    bool closedList[SIZE][SIZE] = {false};
    
    Node* start = malloc(sizeof(Node));
    start->x = startX;
    start->y = startY;
    start->g = 0;
    start->h = heuristic(startX, startY, goalX, goalY);
    start->f = start->g + start->h;
    start->parent = NULL;
    
    openList[openSize++] = start;
    
    while (openSize > 0) {
        int minIndex = 0;
        for (int i = 1; i < openSize; i++) {
            if (openList[i]->f < openList[minIndex]->f) {
                minIndex = i;
            }
        }
        
        Node* current = openList[minIndex];
        
        if (current->x == goalX && current->y == goalY) {
            printf("Path found! Cost: %d\n", current->g);
            return 1;
        }
        
        closedList[current->x][current->y] = true;
        
        // Remove from open list
        for (int i = minIndex; i < openSize - 1; i++) {
            openList[i] = openList[i + 1];
        }
        openSize--;
    }
    
    printf("No path found\n");
    return 0;
}

int main() {
    int grid[SIZE][SIZE] = {
        {1, 1, 1, 1, 1},
        {1, 0, 0, 1, 1},
        {1, 1, 1, 1, 1},
        {1, 0, 0, 0, 1},
        {1, 1, 1, 1, 1}
    };
    
    aStar(grid, 0, 0, 4, 4);
    
    return 0;
}
```

**Explanation:** A* pathfinding algorithm using Manhattan distance heuristic for grid-based navigation.

---