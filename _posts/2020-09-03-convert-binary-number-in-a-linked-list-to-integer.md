---
layout: post
title: "Convert Binary Number in a Linked List to Integer"
date: 2020-09-02 15:57:08 +0800
categories: leetcode, bitwise, linked list, node
---

Remember how I brushed off binaries and bitwise operators? Well, I paid the price. Struggled with this one (I'm guessing due to a lack of prerequisite knowledge).

The problem:

> Given head which is a reference node to a singly-linked list. The value of each node in the linked list is either 0 or 1. The linked list holds the binary representation of a number.

> Return the decimal value of the number in the linked list.

**Example 1:**

    Input: head = [1,0,1]
    Output: 5
    Explanation: (101) in base 2 = (5) in base 10

**Example 2:**

    Input: head = [0]
    Output: 0

**Example 3:**

    Input: head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]
    Output: 18880

**Attempt**

-   Initialize an array
-   Traverse the linked list, remembering to fill up the array with each node's value
-   Iterate through the array and manipulate it somehow

        const getDecimalValue = (head) => {
              let node = head;
              let binaryValues = [];

              while (node) {
                  binaryValues.push(node.val);
                  node = node.next
              }

              // do something here
        }

The first two steps were easy enough. But what would I do with the array of values? I had no idea. Tried to apply a formula I found for converting binary values to integers but there was something faulty with my logic.

Eventually, I resorted to looking it up and found this gem:

    const parseArray = arr => {
        return arr.reduce((acc, val) => {
            return (acc << 1) | val;
        });
    };

If you're at all interested, you can view the article here: [Convert an array of binary numbers to corresponding integer in JavaScript](https://www.tutorialspoint.com/convert-an-array-of-binary-numbers-to-corresponding-integer-in-javascript)

Here's the full solution, where I adapted the snippet from above:

    const getDecimalValue = (head) => {
        let node = head;
        let binaryValues = [];

        while (node) {
            binaryValues.push(node.val);
            node = node.next
        }

        let convertedInteger = binaryValues.reduce((acc, currVal) => {
            return (acc << 1) | currVal;
        }, 0)

        return convertedInteger;
    };

That did the trick.

Still, what in the world is _acc << 1_?

I don't know enough to say. Haven't been able to find an explanation that I can comprehend.

In the meantime, I'll look into bitwise operators - I hope to find something of note. If I do, that'll be in my next post.

Peace!
