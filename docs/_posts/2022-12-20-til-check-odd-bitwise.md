---
layout:	post
title:	"TIL: bitwise & to check odd number"
description: "0b100" 
date:	2022-12-20
featured_image: '/images/posts/til.webp'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

We can use the bitwise operator `&` to check if an integer is odd. Bitwise operators operate on element wise on bits. You can think of it has checking: 
> Are both bits 1?

## Example

```c
01001001
00101000
```

If we take the example above and `&` it we get:

```c
00001000
```

as only the 5th element had both 1s. 

## What does this have to do with even and odd numbers? 
We can use this operator to check if an integer is odd. We do this by `&` any integer with 1. 

The idea is if the least significant bit (the right most bit) is 'on' (equal to 1) then we are just adding one to powers of two which is odd. Otherwise it's even.

## Odd
For example the number 17 in binary is:

```c
10001
```

If we `&` this with one:

```c
10001 &
00001
-----
00001
```

We get a `1`, meaning it is odd. 

## Even
Contrast that with 12:

```c
1100 &
0001
----
0000
```
We get `0`, which means the number is even. 

Next time you want to check even and odd numbers, this may be a quicker way then using `n % 2 == 0`. Or better yet just run the code below and see for yourself.


```python
import numpy as np
import random
import time

def even_bit(n):
    if (n & 1) == 1:
        return "Odd"

    else:
        return "Even"

def even_mod(n):
    if (n % 2) == 0:
        return "Even"

    else:
        return "Odd"

def test_even_bit():
    for _ in range(100):
        time_start = time.time()
        arr = np.random.randint(-(2**31) / 2, ((2**31) - 1) / 2, size=random.randint(0, 10**3), dtype=np.int32)

        for num in arr:
            even_bit(num)

    print(f'100 iterations testing even with bits {time.time() - time_start}')

def test_even_mod():
    time_start = time.time()
    for _ in range(100):
        arr = np.random.randint(-(2**31) / 2, ((2**31) - 1) / 2, size=random.randint(0, 10**3), dtype=np.int32)

        for num in arr:
            even_mod(num)
        
    print(f'100 iterations testing even with mod {time.time() - time_start}')

def main():
    test_even_bit()
    test_even_mod()

if __name__ == "__main__":
    main()
```

## Results
On one of the runs on my Macbook Pro M1:

100 iterations testing even with bits: **0.0006432533264160156s**

100 iterations testing even with mod: **0.0687568187713623s**

Pretty nifty I think.