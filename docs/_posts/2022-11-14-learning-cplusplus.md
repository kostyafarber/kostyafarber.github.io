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
