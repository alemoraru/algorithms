go [back](ALGEBRA-MENU.md)
# __Integer Factorization__

There are multiple approaches to this.

## __Trial division__
* This is the most basic algorithm to find a prime factorization
We divide by each possible divisor until 2 <= d <= sqrt(n)
* Prime factorization in O(sqrt(n))

```c++
vector<long long> trial_division1(long long n) {
    vector<long long> factorization;
    for (long long d = 2; d * d <= n; d++) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
## __Wheel Factorization__

* This is an optimization of the trial division. The idea is the following. Once we know that the number is not divisible by 2, we don't need to check every other even number. This leaves us with only 50% of the numbers to check. After checking 2, we can simply start with 3 and skip every other number.

```c++
vector<long long> trial_division1(long long n) {
    vector<long long> factorization;
    for (long long d = 2; d * d <= n; d++) {
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```

## __Precomputed primes__

* Extending the wheel factorization with more and more primes will leave exactly the primes to check. So a good way of checking is just to precompute all prime numbers with the Sieve of Eratosthenes until n−−√ and test them individually.

```c++
vector<long long> primes;

vector<long long> trial_division4(long long n) {
    vector<long long> factorization;
    for (long long d : primes) {
        if (d * d > n)
            break;
        while (n % d == 0) {
            factorization.push_back(d);
            n /= d;
        }
    }
    if (n > 1)
        factorization.push_back(n);
    return factorization;
}
```
