go [back](ALGEBRA-MENU.md)
# __Euclidian algorithm for computing the greatest common divisor__

Given two non-negative integers *__a__* and *__b__*, we have to find their *__GCD__*. 

## __Implementation__

### C++

The recursive approach:
```c++
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}
```
The recursive approach in 1 line:
```c++
int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
}
```
And finally, here is a non-recursive implementation:

``` c++
int gcd (int a, int b) {
    while (b) {
        int r = a % b;
        a = b;
        b = r;
    }
    return a;
}
```

### Java

The recursive approach:

```java
public int gcd(int a, int b) {
    if (b == 0) {
        return a;
    } else {
        return gcd(b, a % b);
    }
}
```

Iterative implementation: 

```java 
public int gcd(int a, int b) {
    while (b != 0) {
        int r = a % b;
        a = b;
        b = r;
    }
    return a;
}
```


## __Time Complexity__

Worst case scenario is when we get 2 consecutive Fibonacci numbers, hence it 

works in __O(log min(a, b))__

## __Least common multiple__

To avoid integer overflows a possible implementation is as follows :

``` c++
int lcm (int a, int b) {
    return a / gcd(a, b) * b;
}
```