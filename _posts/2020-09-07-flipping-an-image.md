---
layout: post
title: "Flipping An Image"
date: 2020-09-07 13:15:08 +0800
categories: leetcode, bitwise, binary
---

The problem:

> Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.

> To flip an image horizontally means that each row of the image is reversed. For example, flipping [1, 1, 0] horizontally results in [0, 1, 1].

> To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [0, 1, 1] results in [1, 0, 0].

**Example 1:**

    Input: [[1,1,0],[1,0,1],[0,0,0]]
    Output: [[1,0,0],[0,1,0],[1,1,1]]
    Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
    Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]

**Example 2:**

    Input: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
    Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
    Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
    Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]

**Solution**

-   Iterate through the array. For each element in the array (which is also an array), reverse that array.
-   Then, we just need to flip the zeroes and ones!

        const flipAndInvertImage = (A) => {
            const reversed = A.map(arr => arr.reverse());
            const inverted = A.map(arr => {
                return arr.map(el => {
                    return el === 0 ? el = 1 : el = 0;
                })
            })

            return inverted;
        };

Or, we could use XOR logic gates:

    const flipAndInvertImage = (A) => {
        const reversed = A.map(arr => arr.reverse());
        const inverted = A.map(arr => {
            return arr.map(el => {
                return el ^ 1;
            })
        })

        return inverted;
    };

Remember: XOR will return 1 only if one of the bits is 1. If not, it returns 0. Since we're dealing with binary, the element we're looking at will only ever be 1, or 0. Thus, every time we make the comparison el ^ 1, we're essentially doing this check:

    0 ^ 1 // 1
    1 ^ 1 // 0

Which is a nice, slightly different way to reverse the values.

Condensed into a one-liner:

    const flipAndInvertImage = (A) => A.map(arr => arr.reverse().map(el => el ^ 1));
