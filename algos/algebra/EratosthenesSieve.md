go [back](ALGEBRA-MENU.md)
# __Sieve of Eratosthenes__

Sieve of Eratosthenes is an algorithm for finding all the prime numbers in a segment [1 ; n] using O(**n logn**) operations.

## __Implementation__

```c++
int n;
vector<char> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i * i <= n; i++) {
    if (is_prime[i]) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
//elements at index i with value true are prime
```

## __Sieving by the odd numbers only__

Since all even numbers (except 2) are composite, we can stop checking even numbers at all. Instead, we need to operate with odd numbers only.

First, it will allow us to half the needed memory. Second, it will reduce the number of operations performing by algorithm approximately in half.

Optimization : 

```c++
int n;
vector<char> not_prime(n+1, false);
not_prime[0] = not_prime[1] = true;
not_prime[2] = false; //counter approach to previous way

for (int i = 3; i * i <= n; i += 2) {
    if (!not_prime[i]) {
        for (int j = i * i; j <= n; j += i)
            not_prime[j] = true;
    }
}
//elements at index i with value false are prime
```
