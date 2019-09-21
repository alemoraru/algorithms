# C++ Classes 

*  C++ is an object-oriented programming language.

* Everything in C++ is associated with classes and objects, along with its attributes and methods. For example: in real life, a car is an __object__. The car has __attributes__, such as weight and color, and __methods__, such as drive and brake.

* Attributes and methods are basically __variables__ and __functions__ that belongs to the class. These are often referred to as "class members".

## How to create a class?

To create a class, we use the ``` class ``` keyword:

Example: 

```c++
class MyClass {       // The class
  public:             // Access specifier
    int myNum;        // Attribute (int variable)
    string myString;  // Attribute (string variable)
};
```

## Well how do I create an object?

```c++
class MyClass {       // The class
  public:             // Access specifier
    int myNum;        // Attribute (int variable)
    string myString;  // Attribute (string variable)
};

int main() {
  MyClass myObj;  // Create an object of MyClass

  // Access attributes and set values
  myObj.myNum = 15; 
  myObj.myString = "Some text";

  // Print attribute values
  cout << myObj.myNum << "\n";
  cout << myObj.myString;
  return 0;
}
```

## Class Methods

Methods are __functions__ that belongs to the class.

There are two ways to define functions that belongs to a class:

* Inside class definition
* Outside class definition
In the following example, we define a function inside the class, and we name it "myMethod".

__Note:__ You access methods just like you access attributes; by creating an object of the class and by using the dot syntax (.):

Example: 

```c++
class MyClass {        // The class
  public:              // Access specifier
    void myMethod() {  // Method/function defined inside the class
      cout << "Hello World!";
    }
};

int main() {
  MyClass myObj;     // Create an object of MyClass
  myObj.myMethod();  // Call the method
  return 0;
}
```

One thing you can also do in c++ is to define a function outside the class definition. 
you have to declare it inside the class and then define it outside of the class. This is done by specifiying the name of the class, followed the scope resolution :: operator, followed by the name of the function:

__Outside example:__

```c++
class MyClass {        // The class
  public:              // Access specifier
    void myMethod();   // Method/function declaration
};

// Method/function definition outside the class
void MyClass::myMethod() {
  cout << "Hello World!";
}

int main() {
  MyClass myObj;     // Create an object of MyClass
  myObj.myMethod();  // Call the method
  return 0;
}
```

## Constructors 

In c++, constructors are very similar to its java counterpart, as following: 

```c++
class Car {        // The class
  public:          // Access specifier
    string brand;  // Attribute
    string model;  // Attribute
    int year;      // Attribute
    Car(string x, string y, int z) { // Constructor with parameters
      brand = x;
      model = y;
      year = z;
    }
};

int main() {
  // Create Car objects and call the constructor with different values
  Car carObj1("BMW", "X5", 1999);
  Car carObj2("Ford", "Mustang", 1969);

  // Print values
  cout << carObj1.brand << " " << carObj1.model << " " << carObj1.year << "\n";
  cout << carObj2.brand << " " << carObj2.model << " " << carObj2.year << "\n";
  return 0;
}
```

## Encapsulation

```c++
#include <iostream>
using namespace std;

class Employee {
  private:
    // Private attribute
    int salary;

  public:
    // Setter
    void setSalary(int s) {
      salary = s;
    }
    // Getter
    int getSalary() {
      return salary;
    }
};

int main() {
  Employee myObj;
  myObj.setSalary(50000);
  cout << myObj.getSalary();
  return 0;
}
```

### Why encapsulation?

* It is considered good practice to declare your class attributes as private (as often as you can). 
* Encapsulation ensures better control of your data, because you (or others) can change one part of the code without affecting other parts
Increased security of data.

## C++ Inheritance

n C++, it is possible to inherit attributes and methods from one class to another. We group the "inheritance concept" into two categories:

* __derived class__ (child) - the class that inherits from another class
* __base class__ (parent) - the class being inherited from
In the example below, the Car class (child) inherits the attributes and methods from the Vehicle class (parent):

```c++
// Base class
class Vehicle {
  public:
    string brand = "Ford";
    void honk() {
      cout << "Tuut, tuut! \n" ;
    }
};

// Derived class
class Car: public Vehicle {
  public:
    string model = "Mustang";
};

int main() {
  Car myCar;
  myCar.honk();
  cout << myCar.brand + " " + myCar.model;
  return 0;
}
```

## Multiple Inheritance

Unlike java, it is possible to inherit from multiple classes, using a __comma-separated list:__

```c++
// Base class
class MyClass {
  public:
    void myFunction() {
      cout << "Some content in parent class." ;
    }
};

// Another base class
class MyOtherClass {
  public:
    void myOtherFunction() {
      cout << "Some content in another class." ;
    }
};

// Derived class
class MyChildClass: public MyClass, public MyOtherClass {
};

int main() {
  MyChildClass myObj;
  myObj.myFunction();
  myObj.myOtherFunction();
  return 0;
}
```

## How does this compare to Java? (Opinion)

When it comes to inheritance, Java might seem a bit easier in terms of syntax, however C++ offers more freedom when it comes to inheriting from multiple classes, as shown above. Java does make use of a sleek feature, namely interfaces which make it useful when inheriting more "classes". Access modifiers are the same, therefore switching from one language to another should be fairly easy.