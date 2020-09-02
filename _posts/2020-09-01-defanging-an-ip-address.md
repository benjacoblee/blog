---
layout: post
title: "Defanging an IP Address"
date: 2020-09-01 16:05:08 +0800
categories: leetcode, one-liners
---

Went for an interview today. I still have a lot to work on; for example, I was able to normalize an array of objects to produce a singular object, but ultimately had to resort to a .forEach - I wasn't confident in writing out a .reduce by hand (what's the syntax again?).

Also, I come to realize how _nothing_ is a given, be it in the web development world / an interview setting. Sometime during the interview, I was asked: "What browsers have you used for development?" Chrome being the only one, I was thrown off - Chrome may be the "standard" for web dev, but it was unwise to assume that the standard holds true for a common user. All told, a fair question.

> There are so many unknown variables - it's impossible to ever be fully prepared. You can only prepare to the best of what you know

...is something I'm coming to learn.

Anyway.

Today we're defanging an IP address!

The problem:

> Given a valid (IPv4) IP address, return a defanged version of that IP address.

> A defanged IP address replaces every period "." with "[.]".

**Example 1:**

    Input: address = "1.1.1.1"
    Output: "1[.]1[.]1[.]1"

**Example 2:**

    Input: address = "255.100.50.0"
    Output: "255[.]100[.]50[.]0"

**First Attempt**

Javascript has many native methods to help us solve this problem.

First, I split the strings by characters, which returns an array. Then, I map over the array, and for each character, I return the character _unless_ the character is a period - in which case, I'll return a concatenated string with the character sandwiched in-between.

    const defangIPaddr = (address) => {
        return address.split("").map(char=> {
            if(char === ".") return "[" + char +"]"
                return char;
        }).join("")
    }

This had a poor runtime.

**Second Attempt**

I suspected the overreliance on built-in methods was slowing down the runtime, so I decided to try and approach it in a different manner (conventional concatenation via a loop).

    const defangIPaddr = (address) => {
        let word = "";
        let arr = address.split("");

        for (let i = 0; i < arr.length; i++) {
            if(arr[i] === ".") {
                word += "[.]";
            } else {
            word += arr[i];
            }
        }

        return word;
    };

Not making much progress, I decided to check out the discussion section and discovered this one-liner:

    return address.split(".").join("[.]")

Simple and easy to understand, but pretty bad in terms of runtime (only faster than _13.18%_ of all Javascript submissions!).

Looking at other code examples, I also realized that I splitting the word into an array for seemingly no reason. Could've just looped over the word, like so:

    const defangIPaddr = (address) => {
        let word = "";

        for (let i = 0; i < address.length; i++) {
            if(address[i] === ".") {
                word += "[.]";
            } else {
                word += address[i];
            }
        }

        return word;
    };

This was actually decent in terms of runtime.

Anyway, that's all for now. Gonna take some time to decompress.

Peace!
