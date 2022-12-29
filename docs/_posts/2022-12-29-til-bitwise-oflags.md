---
layout:	post
title:	"TIL: bitwise & to check odd number"
description: "0b110" 
date:	2022-12-29
featured_image: '/images/posts/til.webp'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Open flags
Open flags are specified as macros provided to pass to the system call `open()`, to define what permissions and types we want to open a file with.

They can look like

```bash
#define O_RDONLY        00000000
#define O_CREAT         00000100
#define O_TRUNC         00001000
```

We can define a combination of these flags using the logical `|` like so 

```bash
O_RDONLY | O_CREAT | O_TRUC
```
which in binary looks like
```bash
00001100
```

How does `open()` use this to intepret what flags we have set?

Well it uses the `&` operator.

## Bitmasks
A bitmask is data used in bitwise operations. The `&` bitwise operator will set the bit only if both bits are 'on' (i.e 1 and 1).

Using our example above if we `&` O_CREATE with our flags

```bash
00000100 &
00001100
```

It results in
```bash
00000100
```

The idea is, if we `&` any of the flags with the [_oflag_](https://linux.die.net/man/3/open#:~:text=Values%20for-,oflag,-are%20constructed%20by) above and the result is non-zero then we know that flag is set.

This is how we can `open()` checks for which flags have been set

```c
if (flags & O_CREAT) {
	// do something
}
```

In practice, we can use binary numbers like this to set states and check for states in any system, look boolean flags.