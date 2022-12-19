---
layout:	post
title:	"Learning C++"
description: Time to learn a low-level language 🤔
date:	2022-06-30
featured_image: '/images/posts/c-plus-plus.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

# The Idea Is
This is a place where I can record all stuff `c++` and how I'm progressing and learning. This includes everything from general syntax of the language, general problem solving and everything else.

## Classes
### Constructors
Today I learnt that you can't name initalisation variables as you would in Python:

```python
def __init__(self, a, b):
    self.a = a
    self.b = a
```

They have to be different. For example (refer to example [here](https://learn.microsoft.com/en-us/cpp/cpp/constructors-cpp?view=msvc-170)):

```c++
class myObject:
    private:
        int m_a{0}; // initialise to zero so we don't have garbage values.
        int m_b{0};

    public:
        myObject(int a, b): m_a(a), m_b(b) {}
```

## Standard Library 
### String Stream
Today I learnt about the `std::ssstream` object. This allows you to treat a string just like a stream for I/O operations.

```c++
// i/o stream
string name;
cout << "Please enter your name: ";
cin >> name;

string nums = "1,30,50,60";
sstream ss(nums);

vector<int> nums;
while (ss) {
    char buff;
    int num;

    cin >> num >> buff;
    nums.push_back(num);
    
}
```

The above is an example of reading in a comma separated list of integers in a string into a vector of integers using a stream like object. Similar to what you would do with I/O.

*note: the reason we can do `while (ss)` is because [here](https://cplusplus.com/reference/ios/ios/operator_bool/*) the boolean operator is overloaded, making the stream return `false` if there is any error in the stream.*

## Leetcode
### Guessing Game
Today I solved an easy question, that involved performing a binary search. This was the first time doing a problem like this in `c++` and naturally I got the dreaded integer overflow. 

#### Integers
The largest number that can fit into a 32 bit *unsigned (non negative)* integer is $$2^{32}$$. It follows that if we want to represnt a *signed* integer we half this space. The first bit will determine whether a value is positive or negative and then the rest will be the digits. 

So then we have $$-(2^{31})$$ for the negative portion and $$2^{31} - 1$$ for the positive portion.

#### The Problem
Back to the problem.

```c++
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
    int guessNumber(int n) {
        unsigned long int start = 1;
        unsigned long int end = n;
        unsigned long int res = 1;

        while (guess(res) != 0) {
            res = (start + end) / 2;
            
            if (guess(res) == -1) {
                end = res - 1;
            }

            else {
                start = res + 1;
            }
        }

        return res;
    }
};
```

This `res = (start + end) / 2;` was causing an overflow. The `start + end` portion was evaluating to a number that could not fit in a regular 32 bit integer (i.e $$2^{32}$$).

To avoid this you often see:

$$mid = start + \frac{(end - left)}{2}$$

#### Deriving the formula
Naturally I was curious. Where the hell this formula come from? Scrawling Google as developers do I find out it involved some simple algebra. To demonstrate let's say that the mid point is some arbitrary value $$x$$ away from $$l$$:

$$ mid = l + x\tag{1}$$

Substitute into our mid and perform some algebra:

$$ l + x = \frac{l + r}{2}$$

$$ x = \frac{l + r}{2} - l$$

$$ 2x = (l + r) -2l$$

$$ 2x = (r - l)$$

$$ x = \frac{r - l}{2}$$

Substitute $$x$$ back into $$1$$ and we get:

$$mid = l + \frac{r - l}{2}$$

There it is! We have that formula that you see everywhere when performing a binary search and you need to have `start + end` fit into a 32 bit integer. 

I think it's always nice to know where something is coming from when using it. It helps make sense of *how* and *why* I'm using something. 