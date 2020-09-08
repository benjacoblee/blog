---
layout: post
title: "Count Negative Numbers in a Sorted Matrix"
date: 2020-09-08 09:45:08 +0800
categories: leetcode, matrix, arrays, negative numbers
---

The problem:

> Given a m \* n matrix grid which is sorted in non-increasing order both row-wise and column-wise.

> Return the number of negative numbers in grid.

**Example 1:**

    Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
    Output: 8
    Explanation: There are 8 negatives number in the matrix.

**Example 2:**

    Input: grid = [[3,2],[1,0]]
    Output: 0

**Example 3:**

    Input: grid = [[1,-1],[-1,-1]]
    Output: 3

**First Attempt**

An easy way to solve this problem would be to use a nested loop.

-   Initialize a counter
-   Loop through the main array
-   Loop through the subarrays
-   Check if the current element of the subarray is a negative number. If it is, increment the counter

        const countNegatives = (grid) => {
            let negatives = 0;

            grid.forEach(arr => {
                arr.forEach(el => {
                if (el < 0) negatives++;
                })
            })

            return negatives;

        };

Alternatively, we could flatten the array first. If we use the built-in .flat(), we can produce a single array that consists of all the elements in the subarrays. Here's what it would look like.

    let array = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]];
    array.flat();
    array = array.flat(); // [4, 3, 2, -1, 3, 2, 1, -1, 1, 1, -1, -2, -1, -1, -2, -3]

Let's also try Math.sign() for our alternative solution. Math.sign() requires a number as an argument. It then returns us either -1 or 1 (negative, positive).

    let num = 23;
    Math.sign(num); // 1
    num = -23;
    Math.sign(num); // -1

I also wanted to use .reduce() for this solution, mainly to get more practice.

**Second Attempt**

    const countNegatives = (grid) => {
        grid = grid.flat();

        return grid.reduce((acc, currVal) => {
            Math.sign(currVal) === -1 ? acc++ : null;

            return acc;
        }, 0);
    }

We pass the reduce function an accumulator - which, in this case, is a starting value of 0. When the current value is a negative one, we increment the accumulator. When everything is done, we return the accumulator, as well as the result of .reduce().

**Third Attempt**

    const countNegatives = (grid) => {
        let negatives = 0;
        grid = grid.flat();

        grid.forEach(el => Math.sign(el) === -1 ? negatives++ : null);
        return negatives;
    }

I didn't manage to get a good runtime with this one. Some posts in the discussion section suggest that a binary search would be faster. Something to keep in mind for the future!
