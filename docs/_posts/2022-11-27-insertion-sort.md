---
layout:	post
title:	"Insertion Sort"
description: "Another fundamental sorting algorithm" 
date:	2022-11-27
featured_image: '/images/posts/insert-coin.gif'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## What is insertion sort?
This is another post in the sortring algorithms series. Insertion sort is yet another sorting algorithm, similar to selection sort. The concept is that you build the sorted part of the array one element at a time, by inserting it into it's correct place. 

## How do we do it?
The idea is:

* You start with the first element and assume it is sorted.
* Compare the next element with the element before it. If it is less than that element, swap them. 
* Do this until either the element is at the beginning of the array or at it's correct place (the element before it is no longer larger than it)
* Perform the above until we reach the end of the array.

Visually this looks like this:

![insertion-sort-animation](/images/posts/insertion-sort.gif)

<figcaption align = "center"><b>Fig.1 - Insertion sort in action</b></figcaption>

## Time Complexity
Let's think through this for the worst case. We are always comparing the element before the one we are currently processing. What would suck is if at every stage we would have to move the element all the way to the start of the array. This would be the case if the array was sorted in reverse order, like so for example:

$$ array = [5,4,3,2,1] $$

In this case we would have to travese the array \\(n - 1\\) + \\(n - 2\\) + \\(n - 3\\) + ... + 1, which is \\(O(n^2)\\). 

Carrying on with this logic we see that when the array is *sorted* we get the best case time complexity \\(O(n)\\), in which case all we do is compare every adjacent element once and we are done. Obviously this isn't the best sorting algorithm out there but it is still good to know about.

## Implementation
Below is an implementaion in `c++`.

```c++
#include <iostream>
#include <vector>

using namespace std;

void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

void print(const vector<int> &vec) {
    for (auto &num: vec) {
        cout << num << " ";
    }
    cout << endl;
}

vector<int> insertion_sort(vector<int> &vec) {
    for (int i = 0; i < vec.size() - 1; i++) {
        int j = i + 1;

        // use vec.at(j) so you get an out of bounds error
        while (j > 0 && vec.at(j - 1) > vec.at(j)) {
            swap(vec.at(j - 1), vec.at(j));
            j--;
        }
    }
    return vec;
}

int main() {
    vector<int> test = {7, 5, 4, 3, -1, 5, 4, 2, 0};
    print(test);
    insertion_sort(test);
    print(test);
    return 0;
}
```

