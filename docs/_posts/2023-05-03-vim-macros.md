---
layout:	post
title:	Vim Macros
description: What are they are and how they work and why are they amazing
date: 2023-05-03
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

Vim macros. They are awesome. But what are they?

## Vim Macros
According to [redhat](https://www.redhat.com/sysadmin/use-vim-macros) a vim macro is:

> a feature that allows you to record a sequence of commands that you use to perform a given task. You then execute that macro many times to repeat the same job in an automated way.

Simple and elegant, vim macros let you quickly automate tedious tasks.

## How to Record A Macro
Recording a macro involves saving a series of commands to a register (type: `:help registers` in vim to understand what they are).

To record a macro and save it to a register you enter (in command mode) `q` followed by any valid register. A popular register to save to is `q`. It's as easy as:

```vim
qq
```

Vim will record any key presses until you type `q` in command mode again.

Let's go through an example.
## Creating a List of Lists
I had the task of turning a list of commands and their descriptions into a list of lists so I could use them in a Python script. Tedious. Sounds like a job for vim macros.

I formatted the first entry and recorded a macro into register `q` with the following key presses:

```bash
0jddi<80>kb, ^[0i"^[<80><fd>af,i"^[wi"^[A"],^[0i[^[
```

Wow that's ugly. If you type `:registers` after recording your macros you can see what key presses correspond to that register. This was what was in my register after formatting the first item. A lot of these are escape characters, for instance `^]` represents escape. 

I'll leave it to the reader to map them back to what I pressed below.

Once I had done this first item, I selected everything below and typed:

```bash
:normal @q
```

This applies the macro to my selection.

![](../images/airflow_macro.gif)

Boom. The whole list is formatted how I need it to be.

This may seem like overkill, but if this were thousands of entries it would of saved me a lot of time.

## Permanent Macros
What I just showed you is ephemeral. The macro disappears once you close the window. What about if you wanted a macro to persist across sessions? Well you can. 

You can open up your `.vimrc` — wherever it lays — and define your macros there in the format 

```bash
let @register = 'macro contents'
```

Here are a couple I use and why.
## Navigating Quotes
I find myself on a certain type of line a lot. A line where I want to jump straight inside the quotes and delete everything in it. So I defined a macro to do this in register `q` (for quotes).

```bash
let @q = '0f"di"'
```

![](../images/quote_macro.gif)

## Navigating Ticks
The same for ticks saved to the conveniently lettered register `t` (for ticks).

```bash
let @t = "0f'di'"
```

![](../images/tick_macro.gif)

Once I started using these I could not go back to my inefficient ways! Be awesome. Use vim macros. 