---
layout:	post
title:	"TIL: replacing characters in an array"
description: "String literals are untouchable" 
date:	2022-12-20
featured_image: '/images/posts/til.webp'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

I was getting an error if I tried to initialise an array as so, and change values in it.

## Wrong
```c
char* text = "Kostya";
```


```c
#include <stdio.h>

int replace(char* text) {
    int num_space_replacements = 0;

    while (*text != '\0') {
        if (*text == ' ') {
            char dash = '-';
            *text = dash;
            num_space_replacements++;

        }

        text++;
    }

    return num_space_replacements;
}

int main() {
    char test[] = "The cat sat";
    int n = replace(test);

    printf("%s\n", test);
    printf("The number of replacements is: %d\n", n);

    return 0;
}
```
## Oh, string literals
I found my answer. The key is to understand [string literals](https://en.cppreference.com/w/c/language/string_literal#:~:text=String%20literals%20are%20not%20modifiable%20(and%20in%20fact%20may%20be%20placed%20in%20read%2Donly%20memory%20such%20as%20.rodata).%20If%20a%20program%20attempts%20to%20modify%20the%20static%20array%20formed%20by%20a%20string%20literal%2C%20the%20behavior%20is%20undefined.) in c. 

Specifically, is that they are **not modifiable** and in fact are usually placed into read-only memory. Thus doing something like:

```c
#include <stdio.h>

int replace(char* text) {
    int num_space_replacements = 0;

    while (*text != '\0') {
        if (*text == ' ') {
            char dash = '-';
            *text = dash;
            num_space_replacements++;

        }

        text++;
    }

    return num_space_replacements;
}

int main() {
    char* test = "The cat sat";
    int n = replace(test);

    printf("%s\n", test);
    printf("The number of replacements is: %d\n", n);

    return 0;
}
```

Would fail, because this is a string literal.

```c
char* test = "The cat sat"
``` 

And especially on line 9 when:

```c
*text = dash;
```

This is a memory access error, im not allowed to touch it. This will be undefined behaviour causing my program to crash.

## What to do instead
We have to initiliase an array of chars:

```c
char string[] = "Kostya";
```

This way the string literal is copied into an array of characters (into modifiable memory) and I can change the characters in it.

Hope whoever comes across this now understands it a bit better. Thanks folks!