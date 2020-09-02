---
layout: post
title: "Shuffle String"
date: 2020-09-02 09:05:08 +0800
categories: leetcode, string manipulation
---

Note: _I was unable to solve this problem on my own_.

The code below are adaptations of examples provided in Leetcode's discussion section.

The problem:

> Given a string s and an integer array indices of the same length.

> The string s will be shuffled such that the character at the ith position moves to indices[i] in the shuffled string.

> Return the shuffled string.

**Example 1:**

    Input: s = "codeleet", indices = [4,5,6,7,0,2,1,3]
    Output: "leetcode"
    Explanation: As shown, "codeleet" becomes "leetcode" after shuffling.

**Example 2:**

    Input: s = "abc", indices = [0,1,2]
    Output: "abc"
    Explanation: After shuffling, each character remains in its position

**Example 3:**

    Input: s = "aiohn", indices = [3,1,4,2,0]
    Output: "nihao"

**Solution 1**

Create an array that we'll output at the end. Fill that array with values (the values themselves don't matter - we just need an array that's the same length as the string).

Loop through the indices array - find the appropriate position of the array we constructed and insert the current value being accessed in the loop.

Join the array back together to become a string.

    const restoreString = (s, indices) => {

        let output = [];

        for (let i = 0; i < indices.length; i++) {
            output[i] = indices[i];
        }

        for (let i = 0; i < indices.length; i++){
            output[indices[i]] = s[i];
        }

        return output.join("");
    }

Let's take a look at the first example input.

    Input: s = "codeleet", indices = [4,5,6,7,0,2,1,3]

On the first pass through the loop, we need to insert "c" at position 4 of the output array. We access the output array's position:

    // output = [4,5,6,7,0,2,1,3]
    // output[indices[i]]
    output[indices[i]] = s[i];
    // output = [4,5,6,7,"c",2,1,3]

Where indices[i] is 4, essentially accessing output[4].

Let's take a look at another solution, perhaps a more exciting one:

**Solution 2**

    const restoreString = (s, indices) => {
        let map = {};
        let output = "";

        for (let i = 0; i < indices.length; i++) {
            map[indices[i]] = s[i];
        }

        for (let char in map) {
            output += map[char];
        }

        return output;
    }

The interesting thing about this is that, although we are assigning key value pairs to the map, it _preserves the order of the indexes_! If we console.log the first loop and look at the output:

    {4: "c"}
    {4: "c", 5: "o"}
    {4: "c", 5: "o", 6: "d"}
    {4: "c", 5: "o", 6: "d", 7: "e"}
    {0: "l", 4: "c", 5: "o", 6: "d", 7: "e"}
    {0: "l", 2: "e", 4: "c", 5: "o", 6: "d", 7: "e"}
    {0: "l", 1: "e", 2: "e", 4: "c", 5: "o", 6: "d", 7: "e"}
    {0: "l", 1: "e", 2: "e", 3: "t", 4: "c", 5: "o", 6: "d", 7: "e"}

I certainly did not know that Javascript behaves like this - previously assuming that the object would be constructed according to order of insertion. I decided to experiment a little:

    const obj = {};
    obj.zz; = 123;
    obj.aa; = 321;
    obj; // returns {zz: 123, aa: 231}

    const obj2 = {};
    obj2[3] = 1;
    obj2[2] = 2;
    obj2[1] = 3;
    obj2; // returns {1: 3, 2: 2, 3: 1}

Odd!

I'm _guessing_ that when an object's keys are strings, Javascript doesn't care. But when keys are numbers, order is preserved. I cannot substantiate this - again, it's the first time I'm made aware of this behavior.

Back to the solution: after we construct the map, we just need to loop through it again, concatenate to the output string and return it.

Anyway, that's all for now. Hope this was helpful!

Peace
