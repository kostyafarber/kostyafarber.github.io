---
layout:	post
title:	"Learning C++"
description: Time to learn a low-level language 🤔
date:	2022-06-30
featured_image: '/images/posts/kadinsky-c.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

# What I want to do here
This is a place where I can record all stuff `c++` and how I'm progressing and learning.

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



