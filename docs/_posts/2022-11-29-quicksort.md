---
layout:	post
title:	"Quicksort and Partition Algorithms"
description: Sorting Algorithms 
date:	2022-11-29
featured_image: '/images/posts/quick.gif'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## What is Quicksort?
Quicksort is a fundamental *in-place* sorting algorithm used to sort arrays. It uses the *divide and conquer* approach, a famous method in tackling programming problems. It is a recursive algorithm that continually operates on sub-arrays of the original list to sort the array.

## How does Quicksort work?
Quicksort works by using something called a ***pivot value*** which is used to ***partition*** the array into left and right sub-arrays. Everything on the left is less than the pivot and everything to the right is greater than the pivot. Subsequently, recursive calls are made to the sort function on the left and right sub arrays until the list is sorted. At each stage the ***pivot value*** is placed in it's correct place, so once we get to an array of size one we are done.

This is what it looks like visually:

![quick-sort-animation](../images/posts/quicksort-anim.gif)
<figcaption align = "center"><b>Fig.1 - Quicksort algorithm animation</b></figcaption>

## Time Complexity
On average the time complexity for this sorting algorithm is \\(O(nlogn)\\), when the array is divided in half every time. In the worst case the time complexity is \\(O(n^2)\\) when the pivot is the largest or smallest value or there are lots of duplicate values. This makes sense if we think about it:

* If the pivot is the largest or smallest, the subarray array will be \\(n - 1\\) (all values are less or greater than the pivot) in size and we will only be reducing the size by one each time, culminating in a bunch of \\((n - i)\\) calls.


$$\sum_{i=0}^n(n-i) = O(n^2)$$

* If the array has lots of duplicate values and we pick this duplicate as the pivot the same thing will happen and it may return a size of subarray close to the original, with the consequence similar to the above.

Obviously it is important to try create equal partitions in each step, which is important to remember when comparing partition functions.

## The partition functions
Something that has not been specified, which is quite important, is how to partition the data. The choice of the partition algorithm and choices of *where* to pick the pivot are important points to consider and affect the performance of the algorithm considerably.

> As a result quicksort can be thought of, *really*, as a family of algorithms that are composed by picking a partition function and specifying it's parameters. To be honest I found this quite confusing as there wasn't a great deal about this online that explained it well.

There are two main partition functions that are used to implement quicksort:

* The Lomuto Partition function
* The Hoare Partition function

Let's go through both of these functions and how they pick pivots and partition the data.

## Lomuto Partition function
The Lomuto partition function is the slightly simpler one to understand. Essentially it works like this:

* We pick the last value as the pivot and set a pivot index to the beginning of the array minus one `i = low - 1`
* We start from the beginning of the array up until `high - 1` and scan through it checking if `A[j] <= pivot`. If it is then we increment `i` and swap the values that are at `A[j]` and `A[i]`.
* At the end `i + 1` is the pivot index and we swap this with the value at `A[high]` (the pivot value).

### The conceptual idea
The idea is we are building the left sub-array by swapping any values into this portion of the array. If we perform a swap it means the pivot point should be moved forward hence the increment to `i` (i.e put the partition point to the right of any values less than or equal to the pivot).

We increment `i` *again* at the end of the loop because we have `<=` checks. This means values equal to the pivot will appear in the left part of partition and the first value larger than the pivot will be next to this point (i.e `i + 1`) which will be where we want to swap our pivot value at `A[high]`.

Note that it is not a requirement here to have the left or right portions sorted. Only that everything to the left is less than or equal to the pivot and everything to the right is greater than or equal to the pivot.

The correct pivot index is returned, which is important to note for the next algorithm. Notice too, that the bounds checking here is `<=`. Keep these two points in mind.

### Psuedocode and implementation
Below is the psuedocode for the algorithm:

```
// Divides array into two partitions
algorithm partition(A, lo, hi) is 
  pivot := A[hi] // Choose the last element as the pivot

  // Temporary pivot index
  i := lo - 1

  for j := lo to hi - 1 do 
    // If the current element is less than or equal to the pivot
    if A[j] <= pivot then 
      // Move the temporary pivot index forward
      i := i + 1
      // Swap the current element with the element at the temporary pivot index
      swap A[i] with A[j]

  // Move the pivot element to the correct pivot position (between the smaller and larger elements)
  i := i + 1
  swap A[i] with A[hi]
  return i // the pivot index
```

Here is an implementation in `c++` on an array.

```c++
#include <iostream>
#include <vector>

using namespace std;

int lomuto_partition(int start, int end, vector<int>& vec) {
    int i = start - 1;
    int pivot = vec.at(end);

    for (int j = start; j < end - 1; j++) {
        if (vec.at(j) <= pivot) {
            i++;
            swap(vec.at(j), vec.at(i));
        }
    }
    i++;
    swap(vec.at(i), vec.at(end));
    return i;
}

void print(vector<int>& vec) {
    for (auto &num: vec) {
        cout << num << " ";
    }

    cout << endl;
}

int main() {
    vector<int> example = {5, 2, 0, 1, 3};

    print(example); // 5, 2, 0, 1, 3

    int p = lomuto_partition(0, example.size() - 1, example);

    cout << "Partition point is: " << p << endl; // Partition point is: 2
    print(example); // 2 0 3 1 5 
    return 0;
}
```

## Hoares partition function
Now for the fun part. Hoares partition function. This algorithm is slightly different to Lomuto and works better for duplicate values and already sorted arrays. You will find out why in a few minutes, but if you want learn more in-depth check out [this great cs stack exchange answer](https://cs.stackexchange.com/questions/11458/quicksort-partitioning-hoare-vs-lomuto) on the topic, which also explains a popular reason why Hoares is better: 

> because it performs ***three times less swaps*** (again check out the link above to find out why).

I think it's best to just dive in with the description of the algorithm and implementation and I'll outline what I found confusing and how I reasoned about it to understand it.

### Description, pseudocode, implementation
This algorithm uses two pointers. Let's call them `i` and `j`, both pointing to the start and end of the array respectively. We move them towards each other until:

* We increment `i` as long as it is, and this is important, ***less than the pivot*** (i.e `A[i] < pivot`)
* We decrement `j` as long as it is, and this is important ***greater than the pivot*** (i.e `A[j] > pivot`)
* Once both conditions are met we swap both the values at these points.
* We do this until `i >= j` at which point we return `j`.

Essentially this is just swapping values that are not in the correct *relative* position to the pivot. Values that are greater than the pivot should be on the right and vice versa. So we find a pair that are in the wrong place, swap and move forward. Okay no big deal.

Here is the psuedocode:
```
// Divides array into two partitions
algorithm partition(A, lo, hi) is 
  // Pivot value
  pivot := A[ floor((hi + lo) / 2) ] // The value in the middle of the array

  // Left index
  i := lo - 1 

  // Right index
  j := hi + 1

  loop forever 
    // Move the left index to the right at least once and while the element at
    // the left index is less than the pivot
    do i := i + 1 while A[i] < pivot
    
    // Move the right index to the left at least once and while the element at
    // the right index is greater than the pivot
    do j := j - 1 while A[j] > pivot

    // If the indices crossed, return
    if i >= j then return j
    
    // Swap the elements at the left and right indices
    swap A[i] with A[j]
```

and it's implementation in `c++` (I use the start of the array as the pivot in this version)

```c++
int h_partition(int start, int end, vector<int>& vec) {
    int pivot = vec.at(start);
    int i = start - 1;
    int j = end + 1;

    while (1) {
        do {
            i++;
        } while (vec.at(i) < pivot);

        do {
            j--;
        } while (vec.at(j) > pivot);
        

        if (i >= j) {
            return j;
        }

        swap(vec.at(i), vec.at(j));
    }  
}
```

Now check out what we pass to our parition function:

```
// Sorts a (portion of an) array, divides it into partitions, then sorts those
algorithm quicksort(A, lo, hi) is 
  if lo >= 0 && hi >= 0 && lo < hi then
    p := partition(A, lo, hi) 
    quicksort(A, lo, p) // Note: the pivot is now included
    quicksort(A, p + 1, hi) 
```

One thing that struck me immediately when I looked at this is:

> why do we pass in `p` to the first recursive call. 

Intuitively, in Lomuto we left out the pivot (we pass `(low...p - 1) and (p + 1...high)`) as it was in it's correct place and now here we don't? This lead me down the rabbit hole of quicksort which opened up more questions, which I've actually quite enjoyed and hoped I've come to a better understanding of as a result of the rabbit hole. They ain't so bad!

### More questions
* Why do we use `<` and `>` here instead of `>=` like Lomuto?
* Why do we include `p`?
* Why do we return `j`?
* Why does wikipedia say we can't use `high` as the pivot in some cases and we can't use `low` in other cases?
* Why have I seen implementations that return `i`?

This left me with more questions than answers and me being me I wanted to fully understand *why* we are making all these choices. I will try tackle these to the best of my understanding and try learn something along the way.

### Why do we use `<` and `>` here instead of `>=` like Lomuto?
This one was one of the more simple ones. Per [wikipedia](https://en.wikipedia.org/wiki/Quicksort#Hoare_partition_scheme:~:text=With%20respect%20to,the%20first%20inversion), I found the explanation a bit hard to follow, but the gist is we do this so we don't have to run any bounds checks on our pointers. Why? Let me demonstrate with a simple example.

Say we have a simple array:

$$ a = [0, 0]$$
<br>
We set our `pivot = 0`. If we perform `>= and <=` following the pseudocode:

* We increment `i` first as this is a `do while` loop
*  We enter the `while loop` and since `a[i] <= 0` is always true, we increment `i` until it hits 2 and check `a[2] <= 0` and get an out of bounds exception.

Okay we can't have that happen. I will leave it up to the reader to see what happens if we use `> and <` instead (it's nothing phenomenal, we do a useless swap and return `j` because we increment both pointers after the swap because of the nature of a `do while` loop, by which I mean we always run the code before the check).

### We do we include `p`?
Okay this is an interesting one. Best demonstrated through an example. Let's say we have an array:

$$ array = [5, 2, 3, 1, 0] $$

and from this array we pick the pivot `p=3`. 

If we run Hoares partition function on this array we get back this:

$$ array = [0, 2, 1, 3, 5] $$

and the pivot index returned is `2`. 

> Huh? Isn't the pivot value at index `3`? If we used Lomuto (i.e `p + 1, p - 1`) we would be skippping `1` which isn't correct

By the way, to be super clear this is happening because in this function we are actively swapping the pivot value and we can't know where it will end up in the [great dividing range](https://en.wikipedia.org/wiki/Great_Dividing_Range).

Okay... so it seems in this case we should include the pivot. But wait. There are two options now, why? becuase the [pivot can be in either sub array](https://en.wikipedia.org/wiki/Quicksort#:~:text=elements%20that%20are%20equal%20to%20the%20pivot%20can%20go%20either%20way):

```c++
quicksort(a, low, p) // [0, 2, 1]
quicksort(a, p + 1, high) // [3, 5]
```

or

```c++
quicksort(a, low, p - 1) // [0, 2]
quicksort(a, p, high) // [1, 3, 5]
```

Great. Now which one do we choose? Well it depends. What does it depend on? It depends on the whether we return `i` or `j` as the pivot index and whether we choose to use the last or first value of the array as our pivot. I will try to address the last three points of [questions](#more-questions) with the decisions we have to take above.

### Last three points
#### Why do we return `j`?
Okay let's tackle returning `i` or `j`. Again, I think these are best explained through an example. Say we have an array:

$$ a = [0, 0] $$

And we go for the `low, p` variant. We run Hoares on that thing and we get: 
* `i = 1`   
* `j = 0`

Alright good so far. I wanna return `i`, because why not? Let's just pass this into our sorting function. 

```c++
quicksort(a, 0, 1) // [0, 0]
```

Oh shit. That's the exact same array. We are now going to go down a ***not very good rabbit hole*** of infinite recursion. There is [this](https://en.wikipedia.org/wiki/Quicksort#:~:text=It%20is%20therefore%20obvious,returned%20instead%20of%20i) mouthful which boils down to:

> pick `j` as the returned index, as the pivot is in the left sub array. It is our job (partition function) to exclude the "tail" (end) of the array in scenarios where infinite recursion can happen. 

Yeah okay that makes sense. Let's use `j` to trim this array and avoid infinite recursion, because you don't want to hear the words infinite and recursion together.

In the wiki link above the terms "former" and "latter" are used to describe indices `i` and `j` which I believe is easier to think about as the indices that point to the "start" or "end" of the array initially. These descriptions are important when considering the next point.

#### Why does wikipedia say we can't use `high` as the pivot in some cases?
You can probably guess what I'm going to say by this point. Let's walk through an example again to illustrate the point. Let's say we've got an array. But this time (plot twist) it is sorted.

$$ a = [0, 1] $$

Let's perform blashpemy and pick the last value as the pivot value and go with the `(low, p)` variant. We run Hoares on the thing and get:
* `i = 1`
* `j = 1`
* becuase `i <= j` we return `j`

I think you can see where this is going... pass that to our sort function:

```c++
quicksort(a, 0, 1) // [0, 1]
```

Same array again. Damn this isn't easy. So it is obvious now that in this case `(low, p), (p + 1, high)` we can't use the last value as the pivot. What we want to happen is that the *end* index actually crosses the *start* index and we return `j = 0` (we want the former to cross the latter in wikipedia parlance).

#### Why have I seen implementations that return `i`?
Because this article is getting too long, I will leave it up to the reader as an exercise to see when this can become the case. 

*Hint: see what happens when you use `(low, p + 1), (p, high)`* using `i` and `j` etc. 

Pretty much it's the reverse of the above. We have to return `i` and never pick the first element as the pivot to avoid infinite recursion.

## Bonus points
Okay that was a lot. As an added bonus I just want to show why Hoares performs better than Lomuto for arrays with duplicate values. Remember how I said that if we don't partition the function evenly then our performace degrades? Well Hoare's deals with this pretty well.

Say we have an array 😏

$$ a = [1,1,1,1,1,1,1,1] $$

With Lomuto the pivot `p`, leads to, `a[i] <= p` always evaluating to true, so we perform useless swaps and move `i` to the `n - 1` position, creating a **very** unbalanced array.

On the other hand, with Hoare's `a[i] < p` is always false, so perform useless swaps **but** the pointers always move toward each other and will cross at the mid point, creating a balanced split. 

This is the exact behaviour we want to avoid unbalanced splits.

## Conclusion
There is a lot going on with quicksort! I hope I've helped with understanding it a little better. Thanks for reading folks, that's all for today.



