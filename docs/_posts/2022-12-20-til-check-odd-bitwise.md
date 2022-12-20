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

`01001001`

`00101000`

If we take the example above and `&` it we get:

= `00001000` as only the 5th element had both 1s. 

## What does this have to do with even and odd numbers? 
We can use this operator to check if an integer is odd. We do this by `&` any integer with 1. 

The idea is if the least significant bit (the right most bit) is 'on' (equal to 1) then we are just adding one to powers of two which is odd. Otherwise it's even.

## Odd
For example the number 17 in binary is:

`10001`

If we `&` this with one:

`10001 &`

`00001`

= `00001`

We get a `1`, meaning it is odd. 

## Even
Contrast that with 12:

`1100 &`

`0001`

= `0000`

We get `0`, which means the number is even. 

Next time you want to check even and odd numbers, this may be a quicker way then using `n % 2 == 0`.