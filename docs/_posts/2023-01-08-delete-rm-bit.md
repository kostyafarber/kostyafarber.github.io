---
layout:	post
title:	"TIL: x &= (x - 1) deletes the rightmost 1 bit in x"
description: What is this magic 
date:	2023-01-08
featured_image: '/images/posts/til.webp'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Why does this happen?
The a-ha moment is to see what happens when we add \\(1\\) to \\((x - 1)\\) which equals \\(x\\). Say we have the number 10 in decimal as our \\((x - 1)\\), and add one to it, this would look like:

```bash
1010 + 
0001
```

The result would be (11 = x):

```bash
1011
```

The astute observer would notice that in \\((x - 1)\\) there is a zero at the first one bit in \\(x\\). This is because, what adding 1 to \\((x - 1)\\) will do is place a 1 bit into the first open position (the first 0). This means that first zero in \\((x - 1)\\) will correspond to the first 1 bit in \\(x\\). So if we bitwise & this with the original number this will drop that bit (the rightmost 1 bit) in \\(x\\).


```bash
1010 & 
1011
----
1010
```

## Why does this even matter?
Well, with this interesting fact counting bits in an integer becomes *slighly* faster than just right shifting the integer and checking if the bitwise & of 1 and x is equal to 1. The primitive `countbits` may look like this:

```c
int o_countbits(unsigned x) {
    int count = 0;
    for (; x != 0; x >>= 1) {
        if ((x & 1) == 1) {
            ++count;
        }
    }
    return count;
}
```

Which will have to right shift for every position in x. But with our new found knowledge we can re-write this as:

```c
int n_countbits(unsigned x) {
    int count = 0;
    for (; x != 0; x &= (x - 1)) { /* deletes the right most 1 bit every iteration*/
        ++count;
    }
    return count;
}
```

This way we don't have to count any of the zeroes in the integer. Awesome! +1 for micro optimisations.


