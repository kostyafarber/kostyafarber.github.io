---
layout:	post
title:	"Prefix Sum"
description: Cumulative to rescue 
date:	2022-12-04
featured_image: '/images/posts/prefix.jpeg'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## What are prefix sums?
Prefix sums are a data structure that allow use to solve some interesting problems. A ***prefix sum array*** is an array based on a cumulative sum of another array. So, the value at \\(prefix\\_sum[i]\\) is the sum of all elements of \\(array\\) up to the point of `i`

$$ prefix\\_sum[i] = a[0] + a[1] + a[2] + ... + a[i] $$

So for example for the array:

$$ array = [2, 7, 3, 1] $$

It's prefix sum will be:

$$ prefix\\_sum = [2, 9, 12, 13]$$

## How can we create prefix sums?
Notice how for any index `i`, to compute the value at `i`, we have to take the number at \\(array[i]\\) and add it to the value at \\(prefix[i - 1]\\).

$$prefix\\_sum[i] = prefix\\_sum[i - 1] + array[i]$$

One might notice that this definition demands attention for the very first element of the array. Technically at `i = 0` the prefix array is undefined. We have either two choices:
* Initiliase the prefix array with it's first value as zero.
* Initiliase the prefix array with the first value of the original array.

The choice of either will work, but have different names in terms of what the scan is called to produce the prefix array as well as the interpretation of `i` in the prefix array. The first option is produced by an ***exclusive scan*** and the latter by a ***inclusive scan***

### Inclusive and exclusive scans
If we go with the first option, then we produce an array with an ***exclusive scan***. What this means, is that at any position `i` in the prefix sum that is the sum **up to but not including** `i`.

For example, say we have an array:

$$ array = [5, 2, 6, 8] $$

We create a prefix sum array with zero as the seed value:

$$ prefix\\_sum = [0, 5, 7, 13, 21] $$

Let's say we take the index `i = 2`. The prefix_sum at that index is 7. However if we look at the original array we can see that the actual sum at `i = 2` is \\(5 + 2 + 6 = 13\\). This is what we mean by exclusive, we don't include that number at `i` in the original array at that position in the prefix array.

The converse, is a ***inclusive scan*** where we **include** `i` in the sum.

For example, removing the seed value of zero:

$$ prefix\\_sum = [5, 7, 13, 21] $$

For index `i = 2`, the sum is 7, which includes `i` since \\(5 + 2 + 6 = 13\\)

## Use case: Range Sum
A useful use case for prefix sums is it to calculate the sum of a range in \\(O(1)\\) time. If we have an array we can pre-compute the prefix sum and access any range sum in constant time.

We can use the formula, if we use an ***inclusive scan***:

$$ range\\_sum[i...j] = prefix\\_sum[j] - prefix\\_sum[i - 1] $$

For instance, if sum of the array in the previous example from index `1...3` the sum would be `prefix_sum[3] - prefix_sum[0] = 16` which is correct.

One gotcha is if `i = 0`. It's obvious that we would get an index error so if this is the case we would just return `j`, which coincidentally is just the sum up until `j`.

However if our prefix array generated using an ***exclusive scan***, the formula is:

$$ range\\_sum[i...j] = prefix\\_sum[j - 1] - prefix\\_sum[i] $$

The same gotcha applies here if `j = 0` in which case we return `i`.

## Wrap up
Hope you enjoyed reading this and have learnt something. There are many more use cases for prefix sums and they can be quite useful to solve a variety of problems. Thanks for reading. Happy coding.