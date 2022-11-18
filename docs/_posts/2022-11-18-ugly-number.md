---
layout:	post
title:	"263.Ugly Number"
description: Leetcode problem 
date:	2022-11-18
featured_image: '/images/posts/leetcode.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Problem
Today I solved another `c++` leetcode problem. This one was an <span style="color:green">*easy*</span>. and asked us to determine whether a number was an *ugly number*. The idea is, a number is ugly if **it's prime factorisation** only consists of `2, 3, 5`.

*One way to factorise a number into it's primes is to just pick the smallest possible prime number and divide this number by that prime and do the same and so on until the number is 1.*

### Wrong way to go
I originally went ahead and tried to find an algorithm that could produce all prime factors of a number and check to see if it only consisted of `2, 3, 5`. This was not the right way to go.

### The simple solution
It was simple to realise that all we needed to do was continually check if this number `n` was divisable with `mod = 0` for any of those primes. If we eventually got to `1` it meant that we could factorise `n` with only `2, 3, 5` if this check broke and `n` was not equal to one, that meant other factors exist for `n` and it isn't ugly (which isn't the worst thing for a number. Nobody likes being called ugly).

## Code
### C++
```cpp
#include<set>
#include <cmath>

class Solution {
public:
    bool isUgly(int n) {
        vector<int> primes = {2, 3, 5};
        if (n == 0) return false; // edge case

        for (int p: primes) {
            while (n % p == 0) {
                n /= p;
            }
        }
        return n == 1;
    }
};
```

### Python3

```python
class Solution:
    def isUgly(self, n: int) -> bool:
        if n == 0: return False
        primes = (2, 3, 5)

        for p in primes:
            while (n % p == 0):
                n /= p

        return n == 1
```