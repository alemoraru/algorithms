# __Euclidian algorithm for computing the greatest common divisor__

While the __Euclidian Algorithm__ calculates only the GCD of integers *__a__* and *__b__*, the extended version also finds a way to represent GCD in terms of *__a__* and *__b__*, i.e. coefficients *__x__* and *__y__* for which : 
* *__a__* * *__x__* + *__b__* * *__y__* = gcd(*__a__*,*__b__*)

## __Implementation__

The recursive approach :
```c++
int gcd(int a, int b, int & x, int & y) {
    if (a == 0) {
        x = 0;
        y = 1;
        return b;
    }
    int x1, y1;
    int d = gcd(b % a, a, x1, y1);
    x = y1 - (b / a) * x1;
    y = x1;
    return d;
}
```

The recursive function above returns the GCD and the values of coefficients to x and y (which are passed by reference to the function).

Base case for the recursion is *__a__* = 0, when the GCD equals *__b__*, so the coefficients *__x__* and *__y__* are 0 and 1, respectively. In all other cases the above formulas are used to re-calculate the coefficients on each iteration.

This implementation of extended Euclidean algorithm produces correct results for negative integers as well.