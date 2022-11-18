---
layout:	post
title:	"2. Add Two Numbers"
description: Leetcode problem 
date:	2022-11-18
featured_image: '/images/posts/leetcode.png'
tags: data-structures algorithms breadth-first-search art copenhagen contemporary
author: Kostya Farber
---

# Problem Description
## Difficulty: <span style="color:orange">Medium</span>
Today I solved another leetcode problem. This one involved adding two numbers which are represented as two `linked lists`.

> You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. 
> 
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Inital Stab
I went for a *hacky* method. I decided to process the linked lists into a `list` cast them to `strings` reverse it and created a linked list based on that list.

It works. But it wasn't pretty.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        """
        1. Traverse l1 and l2, store them in a list.
        2. reverse the lists and add them up.
        3. Create a linked list out of the list in step 2.
        4. Return the head.
        """
        def process_ll(head, digit_list):
            while head is not None:
                digit_list.append(str(head.val))
                head = head.next

            return digit_list

        integers = []

        head1, head2 = l1, l2

        integers.append(process_ll(head1, []))
        integers.append(process_ll(head2, []))

        int1 = "".join(integers[0])[::-1]
        int2 = "".join(integers[1])[::-1]

        summation = int(int1) + int(int2)
        node_str = str(summation)[::-1]

        dummy = ListNode()
        head = ListNode(node_str[0])
        dummy.next = head

        for i in range(1, len(node_str)):
            next_node = ListNode(node_str[i])
            head.next = next_node
            head = head.next

        return dummy.next

```

## The *better* method
The trick here was to imagine that you are performing the addition as you would with pen and paper.

The idea is you can process each digit column wise:

```python
[1, 2]
[2, 4]

2 + 4 = 6
```

As when we do it on pen and paper, we have to account for carry on. To do this we can just extract the last digit in the summation with:

```python
summation % 10
```

And then if there is a carry we can extract that with:

```python
carry = summation // 10
```

*note: carry can only either be 0 or 1, because the maximum that summation can be is 9 + 9 + 1*

Armed with my new knowledge I decided to implement a similar solution but with arrays instead. You can check it out.

## Array Solution
```python
class Solution:
    def multiply(self, arr1, arr2):
        """Multiply two arrays using paper and pen method

        Args:
            arr1: first operand
            arr2: second operand
        """

        ptr1, ptr2 = len(arr1) - 1, len(arr2) - 1
        res = []
        carry = 0

        while ptr1 >= 0 or ptr2 >= 0:
            _sum = 0 + carry
            
            if ptr1 >= 0:
                _sum += arr1[ptr1]
                ptr1 -= 1
                
            if ptr2 >= 0:
                _sum += arr2[ptr2]
                ptr2 -= 1

            # take the first digit
            res.append(_sum % 10)

            # determine carry (can only either be 1 or 0)
            # because largest digits can be is 9 + 9 + 1 (carry) = 19
            carry = _sum // 10

        # edge case
        if carry > 0:
            res.append(1)

        res.reverse()
        return res

s = Solution()
test = [[1, 2, 3],
        [9, 9, 9]]

print(s.multiply(test[0], test[1]))
```
