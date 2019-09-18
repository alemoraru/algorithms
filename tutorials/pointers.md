# Pointers

Pointers are symbolic representation of addresses. They enable programs to simulate call-by-reference as well as to create and manipulate dynamic data structures. It’s general declaration in C/C++ has the format:

__Syntax__:

```c++
datatype *var_name; //pseudocode
int *ptr;   //ptr can point to an address which holds int data
```

## How do I use a pointer?

Simple, there are 3 easy steps: 

* Define a pointer variable
* Assigning the address of a variable to a pointer using unary operator (&) which returns the address of that variable.
* Accessing the value stored in the address using unary operator (*) which returns the value of the variable located at the address specified by its operand.

__Example:__
```c++
// C++ program to illustrate Pointers in C++ 
#include <stdio.h> 
  
void example() { 
    int var = 20;  
      
    // declare pointer variable     
    int *ptr;  
      
    // note that data type of ptr and var must be same 
    ptr = &var;     
  
    // assign the address of a variable to a pointer 
    printf("Value at ptr = %p \n",ptr); 
    printf("Value at var = %d \n",var); 
    printf("Value at *ptr = %d \n", *ptr);      
} 
  
// Driver program 
int main() { 
    example(); 
} 
```

This will output: 

```c++
//output example

Value at ptr = 0x7ffcb9e9ea4c
Value at var = 20
Value at *ptr = 20
```

## References and Pointers

There are 3 ways to pass C++ arguments to a function
* call-by-value
* call-by-reference with pointer argument
* call-by-reference with reference argument

```c++
// C++ program to illustrate call-by-methods in C++ 
  
#include <bits/stdc++.h> 
using namespace std; 
//Pass-by-Value 
int square1(int n) { 
    //Address of n in square1() is not the same as n1 in main() 
    cout << "address of n1 in square1(): " << &n << "\n";   
    
    // clone modified inside the function 
    n *= n; 
    return n; 
} 
//Pass-by-Reference with Pointer Arguments 
void square2(int *n) { 
    //Address of n in square2() is the same as n2 in main() 
    cout << "address of n2 in square2(): " << n << "\n"; 
      
    // Explicit de-referencing to get the value pointed-to 
    *n *= *n; 
} 
//Pass-by-Reference with Reference Arguments 
void square3(int &n) { 
    //Address of n in square3() is the same as n3 in main() 
    cout << "address of n3 in square3(): " << &n << "\n"; 
      
    // Implicit de-referencing (without '*') 
    n *= n; 
} 
void example() { 
    //Call-by-Value 
    int n1=8; 
    cout << "address of n1 in main(): " << &n1 << "\n"; 
    cout << "Square of n1: " << square1(n1) << "\n"; 
    cout << "No change in n1: " << n1 << "\n"; 
      
    //Call-by-Reference with Pointer Arguments 
    int n2=8; 
    cout << "address of n2 in main(): " << &n2 << "\n"; 
    square2(&n2); 
    cout << "Square of n2: " << n2 << "\n"; 
    cout << "Change reflected in n2: " << n2 << "\n"; 
      
    //Call-by-Reference with Reference Arguments 
    int n3=8; 
    cout << "address of n3 in main(): " << &n3 << "\n"; 
    square3(n3); 
    cout << "Square of n3: " << n3 << "\n"; 
    cout << "Change reflected in n3: " << n3 << "\n"; 
      
      
} 
//Driver program 
int main() { 
    example(); 
} 
```

__Output example:__

```c++
//example

address of n1 in main(): 0x7ffcdb2b4a44
address of n1 in square1(): 0x7ffcdb2b4a2c
Square of n1: 64
No change in n1: 8
address of n2 in main(): 0x7ffcdb2b4a48
address of n2 in square2(): 0x7ffcdb2b4a48
Square of n2: 64
Change reflected in n2: 64
address of n3 in main(): 0x7ffcdb2b4a4c
address of n3 in square3(): 0x7ffcdb2b4a4c
Square of n3: 64
Change reflected in n3: 64
```

__Note:__

*In C++, by default arguments are passed by value and the changes made in the called function will not reflect in the passed variable. The changes are made into a clone made by the called function.
If wish to modify the original copy directly (especially in passing huge object or array) and/or avoid the overhead of cloning, we use pass-by-reference. Pass-by-Reference with Reference Arguments does not require any clumsy syntax for referencing and dereferencing.*

## Array Name as Pointers

An array name contains the address of first element of the array which acts like constant pointer. It means, the address stored in array name can’t be changed.
For example, if we have an array named val then __val__ and __&val[0]__ can be used interchangeably.

```c++
// C++ program to illustrate Array Name as Pointers in C++ 
#include <bits/stdc++.h> 
using namespace std; 
void example() { 
    //Declare an array 
    int val[3] = { 5, 10, 20 }; 
      
    //declare pointer variable  
    int *ptr; 
      
    //Assign the address of val[0] to ptr 
    // We can use ptr=&val[0];(both are same) 
    ptr = val ; 
    cout << "Elements of the array are: "; 
    cout << ptr[0] << " " << ptr[1] << " " << ptr[2]; 
} 
//Driver program 
int main() { 
    example(); 
}
```

__Output example:__

```c++
//example output: 

Elements of the array are: 5 10 20
```