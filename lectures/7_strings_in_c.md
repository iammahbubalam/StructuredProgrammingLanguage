# Strings in C

## Character Arrays vs Strings

In C, there is no built-in string data type like in higher-level languages. Instead, strings are implemented as arrays of characters with a special termination character.

### Character Arrays

A character array is simply an array of characters:

```c
char name[10];  // Array that can hold up to 10 characters
```

### Strings

A string in C is a character array that ends with a null character (`'\0'`):

```c
char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

The null character (`'\0'`) marks the end of the string, allowing functions to know where the string terminates, regardless of the array's actual size.

### Key Differences

1. **Termination**: Strings always end with the null character, character arrays may not.
2. **Length**: The logical length of a string is the number of characters before the null character, not the array size.
3. **Processing**: String functions work on null-terminated strings, not simple character arrays.

### Memory Representation

![String Memory Representation](https://placeholder-for-string-memory-diagram.png)

The above diagram shows how the string "Hello" is stored in memory, with each character occupying one byte and the null terminator marking the end.

## Declaring and Initializing Strings

There are several ways to declare and initialize strings in C:

### 1. Array Initialization with Null Character

```c
char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

### 2. String Literal Initialization

The compiler automatically adds the null character:

```c
char greeting[] = "Hello";  // Equivalent to {'H', 'e', 'l', 'l', 'o', '\0'}
```

### 3. Fixed-Size Array Initialization

```c
char name[10] = "Alice";  // Remaining positions filled with '\0'
```

### 4. Uninitialized Declaration

```c
char title[50];  // Declared but not initialized - contains garbage values
```

### 5. Character Pointer Initialization

```c
const char *message = "Hello, World!";  // Points to string literal (read-only)
```

### Important Considerations

1. **Array Size**: When declaring a character array to hold a string, allow space for the null terminator:

```c
char name[5] = "John";  // Needs 5 chars: 'J', 'o', 'h', 'n', '\0'
```

2. **String Literals**: String literals are stored in read-only memory:

```c
const char *str = "Hello";  // Correct: constant pointer to string literal
char *str = "Hello";        // Bad practice: string literals shouldn't be modified
```

3. **Array vs Pointer Initialization**:

```c
char arr[] = "Hello";    // Creates a modifiable copy of the string
const char *ptr = "Hello";  // Points to the string literal (read-only)

arr[0] = 'h';  // Legal: modifies the array
// ptr[0] = 'h';  // ILLEGAL: attempts to modify string literal
```

## String Input and Output

### Reading Strings

#### 1. Using `scanf()`

```c
#include <stdio.h>

int main() {
    char name[50];
    
    printf("Enter your name: ");
    scanf("%s", name);  // No & operator needed for strings
    
    printf("Hello, %s!\n", name);
    return 0;
}
```

**Limitations of `scanf()` for strings**:
- Stops reading at whitespace
- Can cause buffer overflow if input exceeds array size

#### 2. Using `fgets()`

```c
#include <stdio.h>

int main() {
    char name[50];
    
    printf("Enter your name: ");
    fgets(name, 50, stdin);  // Reads up to 49 chars + null terminator
    
    printf("Hello, %s", name);  // fgets preserves newline character
    return 0;
}
```

**Handling the newline character in `fgets()`**:

```c
#include <stdio.h>
#include <string.h>

int main() {
    char name[50];
    
    printf("Enter your name: ");
    fgets(name, 50, stdin);
    
    // Remove trailing newline if present
    size_t len = strlen(name);
    if (len > 0 && name[len-1] == '\n') {
        name[len-1] = '\0';
    }
    
    printf("Hello, %s!\n", name);
    return 0;
}
```

#### 3. Character by Character Input

```c
#include <stdio.h>

int main() {
    char str[100];
    int i = 0;
    char ch;
    
    printf("Enter a string: ");
    
    while ((ch = getchar()) != '\n' && i < 99) {
        str[i++] = ch;
    }
    str[i] = '\0';  // Manually add null terminator
    
    printf("You entered: %s\n", str);
    return 0;
}
```

### Displaying Strings

#### 1. Using `printf()`

```c
char greeting[] = "Hello, World!";
printf("%s\n", greeting);  // Prints the entire string
```

#### 2. Using `puts()`

```c
char greeting[] = "Hello, World!";
puts(greeting);  // Prints the string and adds a newline
```

#### 3. Character by Character Output

```c
char greeting[] = "Hello";
int i = 0;
while (greeting[i] != '\0') {
    putchar(greeting[i]);
    i++;
}
```

## Common String Functions

C provides a library of string manipulation functions in `<string.h>`. Here are the most commonly used ones:

### 1. `strlen()` - Find String Length

Returns the length of the string (excluding the null terminator).

```c
#include <stdio.h>
#include <string.h>

int main() {
    char text[] = "Hello, World!";
    size_t length = strlen(text);
    
    printf("Length of '%s' is %zu\n", text, length);  // Output: 13
    return 0;
}
```

### 2. `strcpy()` - Copy String

Copies one string to another.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char source[] = "Hello, World!";
    char destination[20];  // Must be large enough
    
    strcpy(destination, source);
    printf("Copied string: %s\n", destination);
    
    return 0;
}
```

#### Safe Alternative: `strncpy()`

```c
char destination[10];
strncpy(destination, source, 9);  // Copy up to 9 characters
destination[9] = '\0';  // Ensure null-termination
```

### 3. `strcat()` - Concatenate Strings

Appends one string to another.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char result[50] = "Hello, ";
    char name[] = "Alice!";
    
    strcat(result, name);
    printf("%s\n", result);  // Output: Hello, Alice!
    
    return 0;
}
```

#### Safe Alternative: `strncat()`

```c
strncat(result, name, 49 - strlen(result));  // Ensure no buffer overflow
```

### 4. `strcmp()` - Compare Strings

Compares two strings lexicographically.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[] = "apple";
    char str2[] = "banana";
    
    int result = strcmp(str1, str2);
    
    if (result < 0) {
        printf("%s comes before %s\n", str1, str2);
    } else if (result > 0) {
        printf("%s comes after %s\n", str1, str2);
    } else {
        printf("%s and %s are equal\n", str1, str2);
    }
    
    return 0;
}
```

### 5. `strchr()` - Find Character in String

Locates the first occurrence of a character in a string.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char text[] = "Hello, World!";
    char *position = strchr(text, 'o');
    
    if (position != NULL) {
        printf("'o' found at position: %ld\n", position - text);
    } else {
        printf("Character not found\n");
    }
    
    return 0;
}
```

### 6. `strstr()` - Find Substring

Finds the first occurrence of a substring within a string.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char text[] = "Programming in C is fun";
    char *substring = strstr(text, "in");
    
    if (substring != NULL) {
        printf("Substring found at position: %ld\n", substring - text);
        printf("Remaining string: %s\n", substring);
    } else {
        printf("Substring not found\n");
    }
    
    return 0;
}
```

### 7. `strtok()` - Tokenize String

Breaks a string into a series of tokens based on a delimiter.

```c
#include <stdio.h>
#include <string.h>

int main() {
    char sentence[] = "This is a sample sentence";
    const char delimiters[] = " ";
    char *token;
    
    // Get the first token
    token = strtok(sentence, delimiters);
    
    // Walk through other tokens
    while (token != NULL) {
        printf("%s\n", token);
        token = strtok(NULL, delimiters);  // Get next token
    }
    
    return 0;
}
```

## Memory Representation of Strings

### String Storage in Memory

1. **Stack Allocation**:
```c
char greeting[20] = "Hello";  // Stored on the stack
```

2. **String Literals**:
```c
const char *message = "Hello";  // Points to read-only memory segment
```

3. **Heap Allocation**:
```c
char *dynamic_str = (char *)malloc(20 * sizeof(char));
strcpy(dynamic_str, "Hello");
// ...
free(dynamic_str);  // Must be freed when done
```

### ASCII Values and Characters

Each character in a string is stored as its ASCII value:

```c
#include <stdio.h>

int main() {
    char c = 'A';
    printf("Character: %c, ASCII Value: %d\n", c, c);  // A, 65
    
    char str[] = "Hello";
    printf("String characters and their ASCII values:\n");
    
    for (int i = 0; str[i] != '\0'; i++) {
        printf("%c: %d\n", str[i], str[i]);
    }
    
    return 0;
}
```

![ASCII Table Reference](https://placeholder-for-ascii-table.png)

## Iterating Through Strings

There are several ways to iterate through a string in C:

### 1. Index-Based Iteration

```c
#include <stdio.h>

int main() {
    char str[] = "Hello";
    
    // Using index
    for (int i = 0; str[i] != '\0'; i++) {
        printf("%c ", str[i]);
    }
    
    return 0;
}
```

### 2. Pointer-Based Iteration

```c
#include <stdio.h>

int main() {
    char str[] = "Hello";
    
    // Using pointer
    for (char *p = str; *p != '\0'; p++) {
        printf("%c ", *p);
    }
    
    return 0;
}
```

### 3. While Loop Iteration

```c
#include <stdio.h>

int main() {
    char str[] = "Hello";
    int i = 0;
    
    while (str[i] != '\0') {
        printf("%c ", str[i]);
        i++;
    }
    
    return 0;
}
```

## String Manipulation Examples

### 1. Converting a String to Uppercase

```c
#include <stdio.h>
#include <ctype.h>

void toUpperCase(char *str) {
    for (int i = 0; str[i] != '\0'; i++) {
        str[i] = toupper(str[i]);
    }
}

int main() {
    char text[] = "Hello, World!";
    
    printf("Original: %s\n", text);
    toUpperCase(text);
    printf("Uppercase: %s\n", text);
    
    return 0;
}
```

### 2. Reversing a String

```c
#include <stdio.h>
#include <string.h>

void reverseString(char *str) {
    int length = strlen(str);
    int i, j;
    char temp;
    
    for (i = 0, j = length - 1; i < j; i++, j--) {
        temp = str[i];
        str[i] = str[j];
        str[j] = temp;
    }
}

int main() {
    char text[] = "Hello, World!";
    
    printf("Original: %s\n", text);
    reverseString(text);
    printf("Reversed: %s\n", text);
    
    return 0;
}
```

### 3. Counting Vowels and Consonants

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char text[100];
    int vowels = 0, consonants = 0;
    
    printf("Enter a string: ");
    fgets(text, sizeof(text), stdin);
    
    for (int i = 0; text[i] != '\0'; i++) {
        char c = tolower(text[i]);
        
        if (c >= 'a' && c <= 'z') {
            if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u')
                vowels++;
            else
                consonants++;
        }
    }
    
    printf("Vowels: %d\n", vowels);
    printf("Consonants: %d\n", consonants);
    
    return 0;
}
```

### 4. Checking if a String is a Palindrome

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int isPalindrome(char *str) {
    int left = 0;
    int right = strlen(str) - 1;
    
    while (left < right) {
        // Skip non-alphanumeric characters
        while (left < right && !isalnum(str[left]))
            left++;
        while (left < right && !isalnum(str[right]))
            right--;
        
        // Compare characters (case-insensitive)
        if (tolower(str[left]) != tolower(str[right]))
            return 0;  // Not a palindrome
            
        left++;
        right--;
    }
    
    return 1;  // Is a palindrome
}

int main() {
    char text[100];
    
    printf("Enter a string: ");
    fgets(text, sizeof(text), stdin);
    
    // Remove trailing newline
    text[strcspn(text, "\n")] = '\0';
    
    if (isPalindrome(text))
        printf("\"%s\" is a palindrome.\n", text);
    else
        printf("\"%s\" is not a palindrome.\n", text);
    
    return 0;
}
```

## Common Pitfalls and Best Practices

### Common Pitfalls

1. **Buffer Overflow**:
```c
// Dangerous: Destination might not be big enough
char small[5];
strcpy(small, "This is too long");  // Buffer overflow!

// Safe: Use strncpy or check size
char small[5];
strncpy(small, "Hi", sizeof(small));
small[sizeof(small) - 1] = '\0';  // Ensure null termination
```

2. **Forgetting the Null Terminator**:
```c
// Bad practice:
char str[5];
str[0] = 'H';
str[1] = 'i';
// Missing null terminator!

// Good practice:
char str[5];
str[0] = 'H';
str[1] = 'i';
str[2] = '\0';  // Add null terminator
```

3. **Modifying String Literals**:
```c
// Dangerous: Undefined behavior
char *str = "Hello";
str[0] = 'h';  // Attempt to modify a string literal

// Safe:
char str[] = "Hello";  // Creates a modifiable copy
str[0] = 'h';  // This is fine
```

4. **Not Checking Return Values**:
```c
// Bad practice:
char *result = strstr(str, "search");
printf("%s\n", result);  // Might be NULL!

// Good practice:
char *result = strstr(str, "search");
if (result != NULL) {
    printf("%s\n", result);
} else {
    printf("Substring not found\n");
}
```

### Best Practices

1. **Always Allocate Enough Space**:
```c
// Account for the null terminator
char name[31];  // Can store up to 30 characters plus '\0'
```

2. **Check Buffer Sizes**:
```c
// Use safer functions
size_t dest_size = sizeof(destination);
strncpy(destination, source, dest_size - 1);
destination[dest_size - 1] = '\0';  // Ensure null termination
```

3. **Free Dynamically Allocated Strings**:
```c
char *dynamic_str = (char *)malloc(50 * sizeof(char));
// ... use dynamic_str ...
free(dynamic_str);  // Prevent memory leaks
```

4. **Use const for Read-Only Strings**:
```c
void printMessage(const char *message) {
    // Using const indicates we won't modify the string
    puts(message);
}
```

5. **Consider Using String Libraries**:
For complex string manipulation, consider safer alternatives:
- POSIX string functions
- C++ std::string (if using C++)
- Third-party string libraries

## Implementing Your Own String Functions

Understanding string functions by implementing them yourself:

### 1. Custom `strlen()`

```c
size_t my_strlen(const char *str) {
    size_t length = 0;
    while (str[length] != '\0') {
        length++;
    }
    return length;
}
```

### 2. Custom `strcpy()`

```c
char *my_strcpy(char *dest, const char *src) {
    char *original_dest = dest;
    
    while ((*dest++ = *src++) != '\0');
    
    return original_dest;
}
```

### 3. Custom `strcmp()`

```c
int my_strcmp(const char *s1, const char *s2) {
    while (*s1 != '\0' && *s1 == *s2) {
        s1++;
        s2++;
    }
    
    return (unsigned char)*s1 - (unsigned char)*s2;
}
```

## Practice Exercises

1. Write a function to count the occurrences of a specific character in a string.
2. Implement a function to remove all spaces from a string.
3. Create a program that checks if two strings are anagrams of each other.
4. Write a function to convert a string to title case (capitalize the first letter of each word).
5. Implement a simple string compression algorithm (e.g., "aaabbc" becomes "a3b2c1").

## Key Takeaways

1. Strings in C are arrays of characters terminated by a null character `'\0'`.
2. Always ensure there's space for the null terminator when declaring character arrays.
3. The standard library provides various functions for string manipulation in `<string.h>`.
4. String literals are stored in read-only memory and should not be modified.
5. Buffer overflows are a common security vulnerability - always check buffer sizes.
6. Understanding memory management is crucial when working with strings in C.

## Additional Resources

- [C String Handling Documentation](https://en.cppreference.com/w/c/string/byte)
- [Common String Functions Tutorial](https://www.tutorialspoint.com/c_standard_library/string_h.htm)
- [C Programming: A Modern Approach (K.N. King)](https://www.amazon.com/C-Programming-Modern-Approach-2nd/dp/0393979504)
