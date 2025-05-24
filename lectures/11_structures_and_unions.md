# Structures and Unions in C

## Introduction to Structures

Structures in C are used to group related variables of different types under a single name. They allow the combination of data items of different kinds. Structures are particularly useful for organizing complex data in a manageable way.

### Basic Structure Definition

```c
struct tag_name {
    data_type member1;
    data_type member2;
    // more members...
};
```

### Example of a Structure

```c
#include <stdio.h>

struct Person {
    char name[50];
    int age;
    float height;
};

int main() {
    struct Person person1;
    
    // Assigning values to members
    strcpy(person1.name, "John Doe");
    person1.age = 30;
    person1.height = 5.9;
    
    // Accessing and printing member values
    printf("Name: %s\n", person1.name);
    printf("Age: %d\n", person1.age);
    printf("Height: %.1f\n", person1.height);
    
    return 0;
}
```

### Memory Allocation in Structures

The size of a structure is the sum of the sizes of its members, possibly plus some padding for alignment. Each member has its own memory location.

```c
#include <stdio.h>

struct Data {
    int i;         // 4 bytes
    float f;       // 4 bytes
    char str[20];  // 20 bytes
};

int main() {
    struct Data data;
    
    printf("Size of struct Data: %zu bytes\n", sizeof(data));  // Outputs: 28 bytes (with padding)
    
    // Show memory addresses of all members
    printf("Address of data.i: %p\n", &data.i);
    printf("Address of data.f: %p\n", &data.f);
    printf("Address of data.str: %p\n", data.str);
    
    return 0;
}
```

![Structure Memory Layout](https://placeholder-for-structure-memory-diagram.png)

### Initializing Structures

Structures can be initialized using curly braces `{}` with values corresponding to the order of the members:

```c
#include <stdio.h>

struct Data {
    int i;
    float f;
    char str[20];
};

int main() {
    // Initialize all members
    struct Data data1 = {10, 3.14, "Hello"};
    
    // Partially initialize (remaining members will be zeroed)
    struct Data data2 = {.f = 2.71, .str = "World"};
    
    printf("data1: %d, %.2f, %s\n", data1.i, data1.f, data1.str);
    printf("data2: %d, %.2f, %s\n", data2.i, data2.f, data2.str);
    
    return 0;
}
```

## Differences Between Structures and Unions

| Feature | Structure | Union |
|---------|-----------|-------|
| Memory Allocation | Each member has its own memory space | All members share the same memory space |
| Size | Sum of the sizes of all members (plus padding) | Size of the largest member |
| Member Access | All members can hold valid values simultaneously | Only one member can hold a valid value at a time |
| Use Case | Group related data of different types | Save memory when different fields are used at different times |

### Visual Comparison

![Structure vs Union Comparison](https://placeholder-for-struct-union-comparison.png)

## Practical Applications of Structures

### 1. Managing Complex Data

Structures are ideal for representing complex data entities with multiple attributes. For example, a `Book` structure in a library management system can have members like `title`, `author`, `ISBN`, and `publication_year`.

### 2. Organizing Related Data

Structures help in organizing data that belongs together. For instance, in a student database, a structure can group `name`, `ID`, and `grades` for each student.

### 3. Abstracting Data Representation

Structures provide a way to abstract and encapsulate data. For example, a `Date` structure can have `day`, `month`, and `year` members, abstracting the representation of a date.

### 4. Enabling Easy Data Manipulation

Structures enable easy manipulation and passing of related data to functions. For instance, a function can take a `Person` structure as an argument to process or display person-related information.

## Introduction to Unions

Unions provide a way to use the same memory location for multiple variables of different types. Unlike structures where each member has its own memory, all members of a union share the same memory space.

### Basic Union Definition

```c
union tag_name {
    data_type member1;
    data_type member2;
    // more members...
};
```

### Example of a Union

```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;
    
    // Using the integer member
    data.i = 10;
    printf("data.i: %d\n", data.i);
    
    // Using the float member (overwrites the same memory)
    data.f = 220.5;
    printf("data.f: %.1f\n", data.f);
    
    // Using the string member (overwrites the same memory)
    strcpy(data.str, "C Programming");
    printf("data.str: %s\n", data.str);
    
    // The integer and float values are now corrupted
    printf("data.i: %d\n", data.i);     // Garbage value
    printf("data.f: %.1f\n", data.f);   // Garbage value
    
    return 0;
}
```

### Memory Allocation in Unions

The size of a union is determined by its largest member. All members share the same beginning address.

```c
#include <stdio.h>

union Data {
    int i;         // 4 bytes
    float f;       // 4 bytes
    char str[20];  // 20 bytes
};

int main() {
    union Data data;
    
    printf("Size of union Data: %zu bytes\n", sizeof(data));  // Outputs: 20 bytes
    
    // Show memory addresses of all members
    printf("Address of data.i: %p\n", &data.i);
    printf("Address of data.f: %p\n", &data.f);
    printf("Address of data.str: %p\n", data.str);
    
    return 0;
}
```

![Union Memory Layout](https://placeholder-for-union-memory-diagram.png)

### Initializing Unions

You can initialize a union with the value of its first member, or using designated initializers:

```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    // Initialize first member
    union Data data1 = {10};
    
    // Using designated initializer (C99)
    union Data data2 = {.f = 3.14};
    union Data data3 = {.str = "Hello"};
    
    printf("data1.i: %d\n", data1.i);
    printf("data2.f: %.2f\n", data2.f);
    printf("data3.str: %s\n", data3.str);
    
    return 0;
}
```

## Differences Between Structures and Unions

| Feature | Structure | Union |
|---------|-----------|-------|
| Memory Allocation | Each member has its own memory space | All members share the same memory space |
| Size | Sum of the sizes of all members (plus padding) | Size of the largest member |
| Member Access | All members can hold valid values simultaneously | Only one member can hold a valid value at a time |
| Use Case | Group related data of different types | Save memory when different fields are used at different times |

### Visual Comparison

![Structure vs Union Comparison](https://placeholder-for-struct-union-comparison.png)

## Practical Applications of Unions

### 1. Type Punning (Reinterpreting Data)

```c
#include <stdio.h>

union Converter {
    float f;
    unsigned int i;
};

int main() {
    union Converter convert;
    
    convert.f = 3.14;
    
    // Examine the bit pattern of the float as an integer
    printf("Float value: %.2f\n", convert.f);
    printf("Bit pattern (as hex): 0x%X\n", convert.i);
    
    return 0;
}
```

### 2. Implementing Variant Types

```c
#include <stdio.h>
#include <string.h>

// Enumeration for different value types
enum ValueType {
    INTEGER,
    FLOAT,
    STRING
};

// A variant type using union
struct Variant {
    enum ValueType type;
    union {
        int i;
        float f;
        char str[20];
    } value;
};

void printVariant(struct Variant var) {
    switch (var.type) {
        case INTEGER:
            printf("Integer value: %d\n", var.value.i);
            break;
        case FLOAT:
            printf("Float value: %.2f\n", var.value.f);
            break;
        case STRING:
            printf("String value: %s\n", var.value.str);
            break;
        default:
            printf("Unknown type\n");
    }
}

int main() {
    struct Variant var1, var2, var3;
    
    // Set up an integer variant
    var1.type = INTEGER;
    var1.value.i = 42;
    
    // Set up a float variant
    var2.type = FLOAT;
    var2.value.f = 3.14;
    
    // Set up a string variant
    var3.type = STRING;
    strcpy(var3.value.str, "Hello");
    
    // Print all variants
    printVariant(var1);
    printVariant(var2);
    printVariant(var3);
    
    return 0;
}
```

### 3. Memory-Efficient Record Storage

```c
#include <stdio.h>
#include <string.h>

// Different record types
struct PersonalRecord {
    char name[30];
    int age;
};

struct BusinessRecord {
    char company[30];
    float revenue;
};

// Record with discriminated union
struct Record {
    char id[10];
    char type;  // 'P' for personal, 'B' for business
    
    union {
        struct PersonalRecord personal;
        struct BusinessRecord business;
    } data;
};

int main() {
    struct Record records[2];
    
    // Create a personal record
    strcpy(records[0].id, "P12345");
    records[0].type = 'P';
    strcpy(records[0].data.personal.name, "John Smith");
    records[0].data.personal.age = 35;
    
    // Create a business record
    strcpy(records[1].id, "B98765");
    records[1].type = 'B';
    strcpy(records[1].data.business.company, "Acme Corp");
    records[1].data.business.revenue = 1500000.0;
    
    // Display the records
    for (int i = 0; i < 2; i++) {
        printf("Record ID: %s\n", records[i].id);
        
        if (records[i].type == 'P') {
            printf("Type: Personal\n");
            printf("Name: %s\n", records[i].data.personal.name);
            printf("Age: %d\n", records[i].data.personal.age);
        } else if (records[i].type == 'B') {
            printf("Type: Business\n");
            printf("Company: %s\n", records[i].data.business.company);
            printf("Revenue: $%.2f\n", records[i].data.business.revenue);
        }
        printf("\n");
    }
    
    return 0;
}
```

## Memory Alignment and Padding

In structures, the compiler automatically adds padding between members to ensure proper memory alignment. This doesn't affect unions since members share the same starting address.

### Structure Padding Example

```c
#include <stdio.h>

struct Padded {
    char c;      // 1 byte
    // 3 bytes padding
    int i;       // 4 bytes
    char c2;     // 1 byte
    // 3 bytes padding
};

struct Packed {
    char c;      // 1 byte
    int i;       // 4 bytes
    char c2;     // 1 byte
} __attribute__((packed));  // Compiler-specific attribute to remove padding

int main() {
    printf("Size of struct Padded: %zu bytes\n", sizeof(struct Padded));  // Likely 12 bytes
    printf("Size of struct Packed: %zu bytes\n", sizeof(struct Packed));  // 6 bytes
    
    return 0;
}
```

### Controlling Padding

1. **Using packed attribute (GCC):**
```c
struct Packed {
    char c;
    int i;
    char c2;
} __attribute__((packed));
```

2. **Using #pragma pack (Visual Studio):**
```c
#pragma pack(push, 1)  // Set alignment to 1 byte
struct Packed {
    char c;
    int i;
    char c2;
};
#pragma pack(pop)  // Restore default alignment
```

3. **Ordering members by size (descending):**
```c
struct OptimizedOrder {
    int i;       // 4 bytes
    char c;      // 1 byte
    char c2;     // 1 byte
};  // Minimizes padding
```

## Nested Unions and Anonymous Unions

### Nested Union Example

```c
#include <stdio.h>

union OuterUnion {
    int i;
    
    union InnerUnion {
        float f;
        char c;
    } inner;
};

int main() {
    union OuterUnion data;
    
    data.i = 65;
    printf("data.i: %d\n", data.i);
    
    data.inner.c = 'A';
    printf("data.inner.c: %c\n", data.inner.c);
    printf("data.i: %d\n", data.i);  // May be corrupted
    
    return 0;
}
```

### Anonymous Unions (C11)

```c
#include <stdio.h>

struct Value {
    int type;  // 0: int, 1: float, 2: char
    
    // Anonymous union
    union {
        int i;
        float f;
        char c;
    };  // No name required
};

int main() {
    struct Value val;
    
    val.type = 0;
    val.i = 42;  // Access directly without a union variable name
    
    printf("Integer value: %d\n", val.i);
    
    val.type = 1;
    val.f = 3.14;
    
    printf("Float value: %.2f\n", val.f);
    
    return 0;
}
```

## Practical Examples

### Example 1: Color Representation

```c
#include <stdio.h>

// Different ways to represent a color
union Color {
    struct {
        unsigned char r, g, b, a;  // RGBA format
    } rgba;
    unsigned int value;  // Packed 32-bit color
};

int main() {
    union Color color;
    
    // Set color using components
    color.rgba.r = 255;  // Red
    color.rgba.g = 128;  // Green
    color.rgba.b = 0;    // Blue
    color.rgba.a = 255;  // Fully opaque
    
    printf("Color as RGBA: (%d, %d, %d, %d)\n", 
           color.rgba.r, color.rgba.g, color.rgba.b, color.rgba.a);
           
    printf("Color as 32-bit value: 0x%08X\n", color.value);
    
    // Modify using packed value
    color.value = 0x00FF00FF;  // Green + Alpha
    
    printf("Modified color: (%d, %d, %d, %d)\n", 
           color.rgba.r, color.rgba.g, color.rgba.b, color.rgba.a);
    
    return 0;
}
```

### Example 2: Network Packet Processing

```c
#include <stdio.h>
#include <string.h>

#define MAX_PAYLOAD 100

enum PacketType {
    DATA,
    CONTROL,
    ACKNOWLEDGMENT
};

struct Packet {
    unsigned short id;
    enum PacketType type;
    
    union {
        struct {
            unsigned short length;
            char payload[MAX_PAYLOAD];
        } data;
        
        struct {
            unsigned char command;
            unsigned char parameter;
        } control;
        
        struct {
            unsigned short ack_id;
        } ack;
    } content;
};

void processPacket(struct Packet *packet) {
    printf("Processing packet ID: %d\n", packet->id);
    
    switch (packet->type) {
        case DATA:
            printf("Data packet, length: %d\n", packet->content.data.length);
            printf("Payload: %.*s\n", packet->content.data.length, 
                   packet->content.data.payload);
            break;
            
        case CONTROL:
            printf("Control packet\n");
            printf("Command: 0x%02X, Parameter: 0x%02X\n", 
                   packet->content.control.command,
                   packet->content.control.parameter);
            break;
            
        case ACKNOWLEDGMENT:
            printf("Acknowledgment packet for ID: %d\n", 
                   packet->content.ack.ack_id);
            break;
            
        default:
            printf("Unknown packet type\n");
    }
    printf("\n");
}

int main() {
    struct Packet packets[3];
    
    // Set up a data packet
    packets[0].id = 1;
    packets[0].type = DATA;
    packets[0].content.data.length = 13;
    strcpy(packets[0].content.data.payload, "Hello, World!");
    
    // Set up a control packet
    packets[1].id = 2;
    packets[1].type = CONTROL;
    packets[1].content.control.command = 0x01;
    packets[1].content.control.parameter = 0xFF;
    
    // Set up an acknowledgment packet
    packets[2].id = 3;
    packets[2].type = ACKNOWLEDGMENT;
    packets[2].content.ack.ack_id = 1;  // Acknowledging packet 1
    
    // Process all packets
    for (int i = 0; i < 3; i++) {
        processPacket(&packets[i]);
    }
    
    // Print sizes
    printf("Size of Packet struct: %zu bytes\n", sizeof(struct Packet));
    printf("Size of data content: %zu bytes\n", 
           sizeof(packets[0].content.data));
    printf("Size of control content: %zu bytes\n", 
           sizeof(packets[1].content.control));
    printf("Size of ack content: %zu bytes\n", 
           sizeof(packets[2].content.ack));
    
    return 0;
}
```

## Common Pitfalls and Best Practices

### Common Pitfalls

1. **Accessing the Wrong Union Member**:
   Since all union members share the same memory, accessing a member after storing a value in another member leads to undefined behavior.

2. **Forgetting the Byte Ordering**:
   When using unions for type punning, be aware of the system's endianness (byte order).

3. **Using Unions for Type Conversion**:
   Type punning with unions may violate strict aliasing rules in C and cause undefined behavior.

4. **Forgetting to Track the Active Member**:
   Without an external indicator of which union member is active, it's easy to misinterpret the data.

### Best Practices

1. **Always Track the Active Member**:
   Use an enum or type field to keep track of which union member currently contains valid data.

2. **Use Unions for Memory Conservation**:
   Only use unions when the members are mutually exclusive and memory conservation is important.

3. **Consider Platform Differences**:
   Be aware that structure padding, alignment, and byte ordering can differ between platforms.

4. **Use Designated Initializers**:
   With C99 or later, use designated initializers to make it clear which union member you're initializing.

5. **Comment Union Usage**:
   Always document the intended use of unions in your code to make it clear to other developers.

## Practice Exercises

1. Create a structure for a library book with members for title, author, ISBN, and publication year.

2. Create an array of structures for a student database that tracks name, ID, and grades in three subjects.

3. Implement a function to swap two structures without using a temporary variable.

4. Create a structure for a complex number and implement functions for addition, subtraction, multiplication, and division.

5. Implement a variant data type using a union that can store integers, floats, or strings, along with functions to print and manipulate the values.

6. Create a structure for a point in 3D space, and implement functions to calculate distance and midpoint between two points.

7. Implement a binary tree node structure that contains data and pointers to left and right children, along with basic tree operations.

8. Create a memory-efficient representation of a sparse matrix using structures and dynamic memory allocation.

## Key Takeaways

1. **Structures** group related variables of different types under a single name, providing organization and abstraction.

2. **Unions** allow different data types to share the same memory space, which is useful for memory conservation and variant types.

3. Structure members each have their own memory, while union members share memory.

4. Arrays of structures are powerful for managing collections of similar data records.

5. Structures and unions can be passed to and returned from functions.

6. Structure padding may add extra bytes for memory alignment, while unions are sized according to their largest member.

7. Nested structures and unions allow for complex data relationships.

8. Anonymous unions (C11) provide a convenient way to directly access union members from a containing structure.

## Further Reading

1. **The C Programming Language** by Kernighan and Ritchie – Chapter 6 covers structures and unions

2. **C: A Reference Manual** by Harbison and Steele – Provides in-depth coverage of C data types

3. **Advanced C Programming** by Milan Bhatt – Has dedicated chapters on structures and unions with advanced examples

4. **Data Structures Through C in Depth** by S. K. Srivastava – Covers practical applications of structures in data structures