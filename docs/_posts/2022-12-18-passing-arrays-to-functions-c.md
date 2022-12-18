---
layout:	post
title:	"TIL: Passing arrays to functions in c"
description: What is the size... 
date:	2022-12-18
featured_image: '/images/posts/c-logo.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Arrays
To define an array in `c` we can do things like:
* `char name[] = "Kostya";`
* `int nums[5] = {1, 2, 3, 4, 5};`

and so forth. We also know that arrays are really just _pointers_ to the first element in the array. For example, `'K'` and `1` in the previous examples.

## Arrays as parameters to functions
We can pass in an array to a function, such as this one that prints the letters of a name:

```c
void print_letters_of_name(char name[]) {
	while (*name) {
		printf("%c \n", *name);
		name++;
	}
}
```

This works because all `c` style strings have the null terminating character `\0` at the end of the array of characters. In practice the array `name` actually looks like `{'K', 'o', 's', 't', 'y', 'a', '\0'}`.

This is why `while (*name)` works. Because once we reach the end and dereference `\0` (which is the number 0 in ASCII) the while loopbreaks because `false` is `0` by definition.

We could also write `while (*name != '\0')`, which is the same but more explicit.

But what about `nums`?

## What is the size of the array?
We know that arrays are just pointers to the first element. So when we define the parameters to an array we can just write:

```c
void print_nums_of_array(int *nums)
```

Thinking in this way, when we pass in the array (pointer) to the function, we lose any notion of the size of the array **_because we can access elements outside of it_**. How do we know when to stop the function?

## Size or terminating element
We really have two options:
* The programmer and users can decide on a null terminating value such as `-1` which will mark the end of the array.

```c
void iterate_over_nums_array(int* nums) {
    while (*nums != -1) {
        printf("%d ", *nums);
        nums++;
    }
    printf("\n");
}
```
* You can pass in the size of the array to the function beforehand.
```c
void iterate_over_nums_array(size_t size, int* nums) {
    int i = 0;
		while (i < size - 1) {
        printf("%d ", *nums);
        nums++;
				i++;
    }
    printf("\n");
}
```

Each have their pros and cons. 

But TIL that mostly, you have to either pass in the size to a function that loops over an array as a parameter, or agree on a terminal value.