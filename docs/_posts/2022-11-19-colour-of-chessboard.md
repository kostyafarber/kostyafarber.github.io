---
layout:	post
title:	"1812. Determine Color of a Chessboard Square"
description: Leetcode problem 
date:	2022-11-19
featured_image: '/images/posts/leetcode.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Problem
Today I solved another problem in both `python` and `c++`. 

> You are given coordinates, a string that represents the coordinates of a square of the chessboard. 
>
> Return true if the square is white, and false if the square is black. 
> 
> The coordinate will always represent a valid chessboard square. The coordinate will always have the letter first, and the number second.

## Inital Stab
This one wasn't very hard when you have a picture of a chessboard in front of you. You just had to determine the pattern in terms of whether the combination of letter and number are in even/odd positions.

I decided to try solve this one in `c++`. I wanted to use a `vector` to store all the numbers and then try find the position of the coordinate in the vector to determine if the letter was 'odd'.

This simple task proved to cumbersone which was, in fact, a good thing because it led me to think of characters as integers (i.e their `ascii` representation).

## Overcomplicating
I then just had a series of `if/else` statements to determine whether the position was black or white. It looked something ugly like this:

```c++
class Solution {
public:
    bool squareIsWhite(string coordinates) {
        // if letter is odd (black if number is odd and white if even)
        // if letter is even (white if number is odd and black if even)
        
        // a = 97, 98
        int chess_char = coordinates[0];
        int i = coordinates[1];

        if (chess_char % 2 != 0) {
            if (i % 2 != 0) {
                return false;
            }

            else {
                return true;
            }
        }

        else {
            if (i % 2 != 0) {
                return true;
            }

            else {
                return false;
            }
        }
    return false;    
    }
};
```

## The better solution
After checking the other solutions it became obvious that I could just add both integers together and then simply check if they were odd/even. That's it. 

> *The obvious fact here is that if you add an odd number to an odd number you get an even number, which in this case meant white chess board colour*

The much more pretty `python` solution:

```python
class Solution:
    def squareIsWhite(self, coordinates: str) -> bool:
        letter = ord(coordinates[0])
        number = int(coordinates[1])

        if ((letter + number) % 2 == 0):
            return False

        return True
```

Another one in the books.