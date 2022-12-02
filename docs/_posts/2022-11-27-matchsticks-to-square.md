---
layout:	post
title:	"473. Matchsticks to Square"
description: Leetcode problem 
date:	2022-11-27
featured_image: '/images/posts/leetcode.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

# Problem
## Difficulty: <span style="color:orange">Medium</span>

> You are given an integer array `matchsticks` where `matchsticks[i]` is the length of the `ith` matchstick. You want to use all the matchsticks to make one square. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.
> 
> Return `true` if you can make this square and `false` otherwise.

![match-sticks-example](../../images/posts/matchsticks.jpeg)
<figcaption align = "center"><b>Fig.1 - Valid square made from matchsticks</b></figcaption>

```
Input: matchsticks = [1,1,2,2,2]
Output: true
Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.
```

