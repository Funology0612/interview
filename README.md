# Basic SW technical terms
* **Embedded System:**	A computer system built into a device to perform specific tasks (e.g., washing machine, smartwatch)
* **Microcontroller (MCU):**	A compact integrated chip with CPU, RAM, Flash memory, and peripherals to control hardware devices
* **GPIO (General Purpose Input/Output):** Pins on the microcontroller used for digital input (e.g., button) or output (e.g., LED)
* **Regiser:** A small memory location inside the MCU used to control or monitor hardware features
* **Interrupt:**	A signal that temporarily pauses the main program to handle important events (e.g., a timer interrupt)
* **ISR (Interrupt Service Routine):** A special function that runs when an interrupt occurs
* **Timer / Counter:** Hardware used for measuring time, generating delays, or creating periodic events
* **PWM (Pulse Width Modulation):** A technique for simulating analog signals using digital pulses (e.g., dimming an LED, controlling motor speed)
* **ADC (Analog to Digital Converter):**	Converts analog signals (like voltage from a sensor) into digital values
* **UART / USART:** Serial communication protocols used to send and receive data between the MCU and other devices (like a PC)
* **I2C/SPI:** High-speed communication protocols used for connecting multiple chips on the same board (e.g., sensors, displays)
* **Flash Memory:** Non-volatile memory where the program (firmware) is stored
* **RAM (Random Access Memory):** Temporary memory used for variables and data during program execution
* **Bootloader:** A small program that helps load the main firmware into the microcontroller from a computer or other device
* **Firmware:** Software programmed into the microcontroller that directly controls hardware
* **Bare-metal Programming:** Writing code directly on the hardware without using an operating system
* **RTOS (Real-Time Operating System):** A lightweight operating system that manages multiple tasks with strict timing requirements
* **Bit-masking / Bit-banding:** Techniques used to manipulate individual bits in registers for efficient hardware control
* **Memory Map:** A layout showing how memory (Flash, RAM, registers) is organized inside the MCU
* **SoC (System on Chip):** an integrated circuit that combines all the major components of a computer or embedded system into a single chip

# Basic mathematics
`+ - * / %`

Exampple:
* 17 + 5 = 22
* 17 - 5 = 12
* 17 * 5 = 85
* 17 / 5 = 3
* 17 % 5 = 2

## Division operator (/) and modulo operator (%)
* **Division**
```c
int a = 7 / 2;       // a = 3 (integer division)
float b = 7.0 / 2;   // b = 3.5 (floating-point division)

```
* **Modulo**
```c
int r1 = 7 % 2;   // r1 = 1 (because 7 = 2*3 + 1)
int r2 = 10 % 3;  // r2 = 1
```
    * Returns the remainder after division.

    * Only works with integers in C.

    * Useful in problems like:

        - Checking if a number is even or odd

        - Circular arrays

        - Clock arithmetic

* **AND, OR, NOT**
    * && – Logical AND
        * Definition: Returns true (1) if both conditions are true
        * Syntax: `condition1 && condition2`
        * Example:
        ```c
        if (a > 0 && b > 0) {
        printf("Both a and b are positive.\n");
        }
        ```

    * || – Logical OR
        * Definition: Returns true (1) if at least one condition is true
        * Syntax:  `condition1 && condition2`
        * Example:
        ```c
        if (a == 0 || b == 0) {
        printf("At least one is zero.\n");
        }
        ```

        * ! – Logical NOT
        * Definition: Returns the opposite of the condition
        * Syntax: `!condition`
        * Example:
        ```c
        if (!(a > 0)) {
        printf("a is not greater than 0.\n");
        }
        ```
    
    
* What is the difference between a = b and a == b?
    >a = b: assigns b to a
    >a == b: checks equality, usually used in conditional statements

* What is the output of !(1 && 0)? Explain
    >!(1 && 0) = !(0) = 1

* What's the time complexity of searching in an unsorted array?
    >Time complexity is O(n) because the algorithm have to look through all n elements in the array

* Explain the range of signed vs unsigned 8-bit integers
    >Unsigned 8-bit: 0 to 255. Signed 8-bit: -128 to 127

## Binary and Hexadecimal
### Definition
* **Binary:** is a number system that uses only two digits: 0 and 1, used in everything from memory addresses to microcontroller registers,Essential for bit masking, logic, and low-level programming
* **Hexadecimal:** is a base-16 number system, using 16 digits (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F), Each hex digit = 4 

### Binary to Hexadecimal
* Group the binary number into 4 bits from right to left, then convert each group to its hex equivalent
* Example
```c
11010111 → [1101] [0111] → D7
```
### Hexadecimal to Binary
* Convert each hex digit to a 4-bit binary number using a lookup table
* Example
```c
2F -> 0010 1111
```

### Decimal to Binary
* Convert:
  * Divide the decimal number by 2.

  * Write down the remainder (0 or 1).

  * Update the number by dividing it by 2 (integer division).

  * Repeat steps 1-3 until the number becomes 0.

  * The binary number is the remainders read from bottom to top (last remainder is the most significant bit)

* Code C:
```c
#include <stdio.h>

void decimalToBinary(int n) {
    if (n > 1)
        decimalToBinary(n / 2);

    printf("%d", n % 2);
}

int main() {
    int decimal = 13;
    printf("Binary of %d is: ", decimal);
    decimalToBinary(decimal);
    return 0;
}
```

* Example: 
> 13 = 1101

### Decimal to Hexadecimal
* Similar to Binary
* Code C
```c
#include <stdio.h>

int main() {
    int decimal = 254;
    printf("Decimal: %d\n", decimal);
    printf("Hexadecimal: 0x%X\n", decimal);  // %X = uppercase hex
    return 0;
}
```

```c
#include <stdio.h>

void decimalToHex(int n) {
    // Array to store hex digits
    char hexDigits[100];
    int i = 0;

    if (n == 0) {
        printf("0");
        return;
    }

    // Repeat division by 16 and store remainders
    while (n != 0) {
        int remainder = n % 16;
        if (remainder < 10)
            hexDigits[i] = remainder + '0';     // 0–9 → '0'–'9'
        else
            hexDigits[i] = remainder - 10 + 'A'; // 10–15 → 'A'–'F'
        n = n / 16;
        i++;
    }

    // Print the digits in reverse (from most significant to least)
    for (int j = i - 1; j >= 0; j--) {
        printf("%c", hexDigits[j]);
    }
}

int main() {
    int decimal = 254;
    printf("Decimal: %d\n", decimal);
    printf("Hexadecimal: 0x");
    decimalToHex(decimal);  // Output: 0xFE
    printf("\n");
    return 0;
}
```

### Binary calculation
* **Addition**
    * 0 + 0 = 0
    * 0 + 1 = 1
    * 1 + 0 = 1
    * 1 + 1 = 0 (carry = 1)
    * Example: 1011 + 1101 = 11000
* **Subtraction**
    * 0 - 0 = 0
    * 0 - 1 = 1 (carry = 1)
    * 1 - 0 = 1
    * 1 - 1 = 0
    * Example: 1101 - 0101 = 1000
* **Multiplication**
    * 0 * 0 = 0
    * 0 * 1 = 0
    * 1 * 0 = 0
    * 1 * 1 = 1
* **Division** convert binary to decimal and do the calculation for a fast way
* **Shift left:** `x << n` means x * (2^n)
* **Shift right:** `x >> n` means x / (2^n)

### Bit masking
`&& AND` `| OR` `^ XOR` `! NOT`
* Bit masking is a technique used to manipulate specific bits in a byte, word, or any binary number using bitwise operators and masks
    * **Set a bit**
    ```c
    int value = 0b00001000;  // 8
    value = value | (1 << 1);  // Set bit 1 → 00001010 (10)
    ```
    * **Clear a bit**
    ```c
    int value = 0b00001110;  // 14
    value = value & ~(1 << 2);  // Clear bit 2 → 00000110 (6)
    ```
    * **Toggle a bit**
    ```c
    int value = 0b00000101;  // 5
    value = value ^ (1 << 0);  // Toggle bit 0 → 00000100 (4)
    ```
    * **Check a bit**
    ```c
    if (value & (1 << n)) {
    // Bit n is set
    }
    ```
### True table
* **Truth Table: AND (&&)**
    0 && 0 = 0
    0 && 1 = 0
    1 && 0 = 0
    1 && 1 = 1
* **Truth Table: OR (||)**  
    0 || 0 = 0
    0 || 1 = 1
    1 || 0 = 1
    1 || 1 = 1
* **Truth Table: NOT (!)**
    !0 = 1
    !1 = 0

## SW Design Flow
* List the steps in the software design flow
>Requirement Analysis – Understand and gather what the software must do
>System Design – Define the overall architecture and break the system into modules
>Module Design – Detail the internal workings of each module and their interfaces
>Interface Definition – Specify how modules communicate with each other
>Implementation – Write the code according to the design
>Testing – Verify the software works as expected through unit and integration tests
>Documentation – Record the design, code explanations, and user instructions
>Maintenance – Fix bugs and update software after deployment

* Distinguish between High-level design and Low-level design. Give examples
>High-level design defines the main system modules and their interactions
Example: Dividing a system into Sensor, Control, and Display modules

>Low-level design details the internal workings of each module, like functions and algorithms
Example: Writing functions such as read_temperature() and display_on_LCD()

* Why is integrating testing into the design process important in embedded systems?
> Testing during design helps find bugs early, ensures reliability with hardware constraints, saves time, and improves overall system quality — especially important since embedded systems often have real-time and safety-critical requirements

## C language programming
### Variables
* Declare a variable ic C
```c
int count;
float temperature;
char letter;

```

* What is the difference between a local variable and a global variable?
>Local variable: Declared inside a function or block and only accessible within that scope.

>Global variable: Declared outside all functions and accessible throughout the entire program.

* What is the typical size (in bytes) of int, float, and char on a 32-bit system?
> `int` 4 bytes, `float` 4 bytes, `char` byte

* What is the default value of an uninitialized variable?
>Uninitialized local variables have undefined values (garbage)
>Uninitialized global variables are automatically initialized to 0

* Declare a constant in C
> const int MAX_VALUE = 100;

* Explain the `static` keyword when declaring a variable
> For a local variable, static makes it retain its value between function calls

> For a global variable, static restricts its scope to the file where it is declared (internal linkage)

* When should you use static variables and global variables?
> Use static local variables when you want a function to remember its state between calls but keep the variable hidden outside the function

> Use global variables when multiple functions need to share data, but use them carefully to avoid unintended side effects
### Pointers
Giá trị của con trỏ là địa chỉ của ô nhớ mà nó trỏ đến
```c
int x = 10;
int *p = &x;  // &x lấy địa chỉ của biến x, gán cho con trỏ p

printf("Giá trị x: %d\n", x);     // In ra giá trị của x: 10
printf("Địa chỉ x: %p\n", &x);    // In ra địa chỉ của x
printf("Giá trị qua con trỏ p: %d\n", *p);  // *p: lấy giá trị tại địa chỉ p, in ra 10
```
* Explain the meaning of `*` and `&` in C
> `*`: Used to declare a pointer or dereference it (access the value it points to)
> `&`: Used to get the address of a variable
```c
int a = 10;
int *p = &a;   // &a is the address of a
int b = *p;    // *p gives the value at that address (10)
```
Change the value of a variable using pointer
```c
#include <stdio.h>

int main() {
    int a = 5;
    int *p = &a;
    *p = 10;  // changes value of a
    printf("a = %d\n", a);  // Output: a = 10
    return 0;
}
```

* Explain the difference between `int *p;` and `int` p;`
> `int p;` declares a regular integer variable

> `int *p;` declares a pointer to an integer (stores an address, not a value)

* Declare a pointer to pointer
> int **p; 

*  What is a NULL pointer? Why should you check for NULL before using a pointer?
> A NULL pointer is a pointer that does not point to any valid memory address
> We check for NULL to avoid segmentation faults or undefined behavior when dereferencing

* How to allocate and free dynamic memory using pointers?
```c
#include <stdlib.h>

int *p = (int *)malloc(sizeof(int));  // allocate memory
if (p != NULL) {
    *p = 42;
    free(p);  // free memory
}
```
* malloc() and calloc()
    * malloc(): void *malloc(size_t size);
        * Allocates a block of memory of size bytes
        * Returns a pointer to the first byte of the block
        * Does NOT initialize the memory (the contents are garbage)
        * Returns NULL if the allocation fails
    Ex: 
    ```c
    int *arr = (int *)malloc(5 * sizeof(int));  // allocates memory for 5 integers
    ```
  * calloc(): void* calloc(size_t num, size_t size);
        * Allocates memory for an array of `num` elements, each of `size` bytes
        * Initializes all bytes to zero
        * Returns NULL if allocation fails
    Ex: 
    ```c
    iint *arr = (int *)calloc(5, sizeof(int));  // allocates and zero-initializes array of 5 integers
    ```

* Write a function to swap two integers using pointers
```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

* What is dangling pointer? How to prevent it?
> Dangling pointer is a pointer that still points to a memory location that has been freed or is no longer valid

Prevent:
```c
free(p);
p = NULL;
```

### Array
* What is the difference between one-dimensional and two-dimensional arrays?
> A one-dimensional array is a linear list of elements (like a vector)

> A two-dimensional array is an array of arrays, forming a matrix (rows and columns)

* What is an array name in C actually?
> The array name acts as a pointer to the first element of the array

* Can the size of an array be changed after declaration?
> No, the size of a statically declared array cannot be changed after compilation

* What happens if you access beyond the array bounds?
> Accessing out-of-bounds elements causes undefined behavior which can lead to crashes or incorrect results

* What is the difference between arrays and pointers in C?
>Arrays have a fixed size and contiguous memory allocated automatically

>Pointers hold memory addresses and can be reassigned to different locations

* What is the difference between static arrays and dynamic arrays?
> Static arrays have fixed size determined at compile time and are usually allocated on the stack

> Dynamic arrays are allocated at runtime on the heap using functions like malloc() and can have flexible sizes

### Struct
* A struct is a user-defined data type that groups different types of variables together under one name

* Each member has its own memory space

* The total size of the struct is at least the sum of the sizes of all members (may include padding for alignment)

* Syntax:
```c
struct Person {
    char name[50];
    int age;
    float height;
};
struct Person p1;
p1.age = 25;
```

### Union
* A union is similar to a struct but all members share the same memory space

* The size of the union is equal to the size of its largest member

* Only one member can hold a value at any given time; changing one member affects the others

* Syntax:
```c
union Data {
    int i;
    float f;
    char str[20];
};
union Data d;
d.i = 10;
d.f = 220.5;  // overwrites previous value of i
```
## Essay writing
**Describe a project you did**

I worked on a digital weighing scale project that measures the weight of objects and displays the result on an LCD screen. Additionally, the weight data is transmitted to a laptop via UART communication for further processing and monitoring. The system integrates a load cell sensor for accurate weight measurement, a microcontroller that called STM32F103C8T6 to process the signals, and UART protocol to enable real-time data transfer to the computer. This project demonstrates the practical application of embedded systems in data acquisition and user interface design

Code for BlinkLed using register:
```c
GPIOC->ODR &= ~(1 << 13);  // Ghi 0 vào bit 13 → LED ON
delay_ms(500);
GPIOC->ODR |=  (1 << 13);  // Ghi 1 vào bit 13 → LED OFF
delay_ms(500);
```
> ODR: Output Data Register
