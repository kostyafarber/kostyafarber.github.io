---
layout:	post
title:	"Static variables in c"
description: "What are they are and how they work" 
date:	2023-03-12
featured_image: '/images/posts/til.webp'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Static variables
In the c programming language we can use the keyword `static` to define a static variable. This keyword is part of the *storage class specifiers*, one of which you may know as `extern` and maybe the lesser known `auto` and `register`.

```c
int
main()
{
    static int x = 5;
    printf("My cool static variable... %d", x);
}
```
```bash
$ My cool static variable... 5
```

These keywords define how a variable is stored.

According to [C programming language standard](https://en.cppreference.com/w/c/language/storage_duration#:~:text=The%20storage%2Dclass%20specifiers%20determine%20two%20independent%20properties%20of%20the%20names%20they%20declare%3A%20storage%20duration%20and%20linkage)
> The storage-class specifiers determine two independent properties of the names they declare: storage duration and linkage.

## Storage and Linkage
### Storage
All variables have the notion of storage. They may be allocated on the stack (come in and out of existence as functions are called and returned) or on the heap - dynamically.

When we declare an object (variable or function) with the `static` keyword it's storage duration is that of the entire program. It is [allocated once before the main function.](https://en.cppreference.com/w/c/language/storage_duration#:~:text=and%20the%20value%20stored%20in%20the%20object%20is%20initialized%20only%20once%2C%20prior%20to%20main%20function.)

#### Implication
All variables without a storage class specifier use the `auto` keyword, meaning that it is allocated in the block in which it is entered and de-allocated when it leaves that block.

```c
void f1()
{
    int x = 5; /* x goes into scope */
    
    /* do some stuff */

    return; /* x goes out of scope and is de-allocated and ceases to exist */
}

int 
main()
{
    f1() /* We have no notion of x in main() */
}
```

In the previous example, if we declared `x` as a `static` variable after `f1()` exits we could still access, use and modify `x` even after it exits `f1()` scope.

### Linkage
Linkage refers to an object (variable or function) that can be referenced in different scopes. All variables have *external linkage* by default. This means that they are visible to other *translation units* in the same program. However when we use the `static` keyword in the global scope, that variable is *internally linked* meaning it is only visible to that translation unit.

#### Implication
This means that any objects defined are only visible to that translation unit. For instance if we had a variable called `buffer` in `file.c` and we want to contain this variable in `file.c` because it will conflict with other definitions we can name it like so:

```c
/* file.c */
static char[SIZE] buffer;

int
main()
{
    /* do stuff with buff here */
}
```

```c
/* file2.c */
char[SIZE] buffer; /* refers to a different buff than file.c buff */

int
main()
{
    /* do stuff with buff here */
}
```

Hope you enjoyed the read!