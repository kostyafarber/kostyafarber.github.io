---
layout:	post
title:	"Finding Data Structures and Algorithms in Art"
description: Discovering a popular algorithm displayed in art at the Copenhagen Contemporary. 
date:	2022-06-30
featured_image: '/images/posts/cc-contemporary.jpeg'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

## Art and Science
The **intersection** of art and science has always been an area that is of great interest to me. Finding both, in unfamiliar and unsuspecting places, can be a delightful experience. For the past couple of weeks I have been travelling around Europe and stopped over in Copenhagen, Denmark.
Being both big fans of contemporary art, my partner and I decided to take ourselves to København to visit Copenhagen Contemporary and see the [Light and Space](https://copenhagencontemporary.org/light-space/) 🔦 exhibit.

> Light & Space features both historical and new works from the American light and installation art movement that emerged in Los Angeles in the 1960s. At the time, a number of young artists were experimenting with making art out of light and new materials inspired by Los Angeles’ mix of sun, surf culture, Hollywood glamour, spirituality, and endless traffic jams.

## Moving into Tech
In June of 2022 I decided I wanted to move to London from Sydney to have more oppurtunities in tech. An inauguration, as part of this search, involves being able to solve *data structure and algorithm* (DSA) problems. Quickly and efficiently. Anyone in my position can relate to the struggle. Having a keen intuition for these concepts is key.

### Breadth Fist Search
One of the popular algorithms used to solve graph or tree based problems is the *Breadth First Search* (BFS) algorithm. This involves traversing a tree type structure using a queue, starting at some node. There are many problems that can be solved using a BFS algorithm. 

Say we have some data structure, perhaps a 2D grid. We have two nodes on this grid and we are interested in finding the shortest path between these two nodes. How can we determine this path? We can use BFS. The concept goes (we won't go into proving this) is that any time we reach a node using BFS that is one the shortest paths to that node.

Somewhere online somebody explained how to visualise this best, in my opinion. Imagine being at the starting node. It catches fire and this fire spreads to all the reachable nodes from this node and does the same for every other node. It plays out like the below animation. Whenever I think of BFS I think of this animation and the analogy of the 🔥.

![breadth-first-search algorithm animation](/images/posts/bfs.gif)
<figcaption align = "center"><b>Figure 1. Finding the shortest path using Breadth First Search</b></figcaption>

## Algorithms and Art
The brain is a *remarkable* pattern recognition machine. The sense of familiarity that we get when we look at something for a second and we don't know why. I think the name for this is intuition. I had one of these experiences at the exhibit. As we made our way through the diffferent rooms we entered into a space full of different installations and a wall of framed drawings. I make my way around the walls and stumble upon a frame that seems familiar in an unknown way, at first.

![BFS in art](/images/posts/bfs-art.jpg)
<figcaption align = "center"><b>Figure 2. BFS on 2D Grid with the Tally System representing distance from the top left corner.</b></figcaption>
<br>
I realise this is nothing but the BFS catching fire animation! It's represented using the Tally System to numerate the distance from the top left corner. It's a simple and beautiful way to represent a BFS. As we move further from the top left corner the tally's become inelligable. These areas represent a longer path (distance) from the top left corner. The drawing almost becomes like a heat map, with darker areas representing further distances.

 It was quite a suprise to bump shoulders with a concept from my software engineering studies in a contemporary art musuem. These are the moments I cherish and will remember forever. I believe great things happen at the intersection of <span style="color:#364ce3">**science**</span> and <span style="color:#364ce3">**art**</span>.

 I am writing this while on the bus to Gothenburg, taking in the picturesque landscapes. I hope to find some more of these momments in 🇸🇪
