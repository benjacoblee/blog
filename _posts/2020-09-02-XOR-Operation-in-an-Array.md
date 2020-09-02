---
layout: post
title: "XOR Operation in an Array"
date: 2020-09-02 11:46:08 +0800
categories: leetcode, bitwise, operators, bitwise operators, operand
---

Managed to solve this problem without knowing the theory behind it, but.. I think we should talk a little about bitwise operations.

A bitwise operation is an action performed on integers that have been converted into binary. Operations are performed _bit by bit_.

**Bitwise XOR Operator**

> Returns 1 if one of the bits is 1 and the other is 0. Otherwise, if both are 0 or both are 1, returns 0

That doesn't really explain a lot, and I'm not going to pretend that I understand binary or bits - we'll bookmark this and come back to it in the future.

For now, let's just get on with it.

The problem:

> Given an integer n and an integer start.

> Define an array nums where nums[i] = start + 2\*i (0-indexed) and n == nums.length.

> Return the bitwise XOR of all elements of nums.

**Example 1:**

    Input: n = 5, start = 0
    Output: 8
    Explanation: Array nums is equal to [0, 2, 4, 6, 8] where (0 ^ 2 ^ 4 ^ 6    ^ 8) = 8.
    Where "^" corresponds to bitwise XOR operator.

**Example 2:**

    Input: n = 4, start = 3
    Output: 8
    Explanation: Array nums is equal to [3, 5, 7, 9] where (3 ^ 5 ^ 7 ^ 9) = 8.

**Example 3:**

    Input: n = 1, start = 7
    Output: 7

**Solution**

I didn't try to optimize my solution (can't say I'm particularly interested in this subject) but my thinking is this:

-   Initialize an array
-   Initialize an output value
-   While its length is less than n (n being the number of elements), fill it with values (where each value is start + 2 \* i)
-   Loop over the array, continually performing the XOR operations on each element in the array
-   Return the output value

I definitely had to fiddle around with _foo ^ bar_ amongst various examples to see what the operations were doing, but it made sense eventually.

Here's the code:

    const xorOperation = (n, start) => {
        const arr = [start];
        let index = 1;
        let output = arr[start];

        while (index < n) {
            arr.push(start + (2 * index));
            index++;
        }

        for (let i = 0; i < arr.length; i++) {
            output = output ^ arr[i];
        }

        return output;
    }

Drawing upon the examples provided, we know that the first element of the array is going to be the start value passed to the argument - thus, we can begin our loop at index 1.

Given the formula _start + 2 \* i_, push each corresponding value into the array, incrementing the index each time.

From that point on, all we need to do is reassign the output value to be the previous _output value ^ the current element_ we're looping over.

I arrived at this solution after cleaning up some logic. Initially, I tried doing this:

    let output = 0;
    if(!output) {
        output = arr[i] ^ arr[i + 1];
    } else {
        output = output ^ arr[i];
    }

But we don't necessarily know what the output value is going to start with. What we do know is that we want to perform each operation beginning from the first element in the array and the next. That value is captured, and we perform it on the next, etc.

Since the runtime was decent, I was pretty happy with my solution until I saw this:

    let xorOperation = (n, x) => n == 1 ? x : x ^ xorOperation(n - 1, x + 2);

Oh well. Despite the subject matter, this was a pretty fun one.

Until next time.

Peace!
