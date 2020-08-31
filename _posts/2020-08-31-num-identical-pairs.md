---
layout: post
title: "Number of Good Pairs"
date: 2020-08-31 16:52:08 +0800
categories: leetcode, hash tables
---

The problem:

> Given an array of integers nums.

> A pair (i,j) is called good if nums[i] == nums[j] and i < j.

> Return the number of good pairs.

**Example 1:**

    Input: nums = [1,2,3,1,1,3]
    Output: 4
    Explanation: There are 4 good pairs (0,3), (0,4), (3,4), (2,5) 0-indexed.

**Example 2:**

    Input: nums = [1,1,1,1]
    Output: 6
    Explanation: Each pair in the array are good.

**Example 3:**

    Input: nums = [1,2,3]
    Output: 0

I immediately decided to use a hash map for this problem - but was getting tripped up in the weirdest places. Something's just not clicking today.

But here's the logic:

First, we need an empty map and a counter to keep track of the number of good pairs. Next, we loop thruogh the nums array - for every number in the array, if it _doesn't_ exist, we assign it as a key to the hash table, with a value of 1. If it exists, we increment its value as well as the counter's value.

**Hash Table Solution**

    function numIdenticalPairs(nums) {
        const map = {};
        let goodPairs = 0;

        for (num of nums) {
            if(map[num]) {
                goodPairs += map[num];
                map[num]++;
            } else {
                map[num] = 1;
            }
        }

        return goodPairs;
    }

I don't quite know what tripped me up; at first, I wanted to save the value as a key, and the index as the key's value (maybe because of example 1's explanation). That would be a problem since there would be identical keys - so I thought maybe I'd reverse the key to be the array's index, and the key's value to be the actual value... by that point, everything got real confusing, real quick.

Anyway, hope that made some sense. Mind's just not working right now.

Might as well go off for a skate.

Peace!
