go [back](ALGEBRA-MENU.md)
# __Binary Exponentiation__

Binary exponentiation (also known as exponentiation by squaring) is a trick which allows to calculate an using only O(logn) multiplications (instead of O(n) multiplications required by the naive approach).

It also has important applications in many tasks unrelated to arithmetic, since it can be used with any operations that have the property of associativity:

(X⋅Y)⋅Z=X⋅(Y⋅Z)
Most obviously this applies to modular multiplication, to multiplication of matrices and to other problems which we will discuss below.

## __Algorithm__

Raising *__a__* to the power of *__n__* is expressed as multiplication by *__a__* done *__n-1__* times. However, this is not practical when it comes for large *__a__* or *__n__*.

The idea is to write n in base 2, for example :
* 3<sup>13</sup> = 3<sup>1101<sub>2</sub></sup>
* Since the number *__n__* has exactly floor(log<sub>2</sub>*__n__*) + 1 digits in base 2, we need only to perform O(logn) multiplications, if we just know powers *__a<sup>1</sup>__*, *__a<sup>2</sup>__*, *__a<sup>4</sup>__*, *__a<sup>8</sup>__*,..., *__a<sup>floor(log<sub>2</sub>n)</sup>__*
* This is easy, since an element in the sequence is the square of the previous element, for example :
    * 3<sup>1</sup> = 3
    * 3<sup>2</sup> = (3<sup>1<sup>2</sup></sup>) = 3<sup>2</sup> = 9
    * 3<sup>4</sup> = (3<sup>2<sup>2</sup></sup>) = 9<sup>2</sup> = 81
    * 3<sup>8</sup> = (3<sup>4<sup>2</sup></sup>) = 81<sup>2</sup> = 6561

* To get the final answer for 3<sup>13</sup> we need only multiply 3 of them because the corresponding bit for 3<sup>2</sup> is not set in *__n__*.
* 3<sup>13</sup> = 6561 * 81 * 3 = 1594323

* Final complexity is O(**log n**)

## __Implementation__

The recursive approach :
```c++
long long binpow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = binpow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
```

The iterative approach, which although has the same complexity, it will be faster in practice since we have the overhead of the recursive calls : 

``` c++
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
```