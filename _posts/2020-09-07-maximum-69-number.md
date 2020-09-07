---
layout: post
title: "Maximum 69 Number"
date: 2020-09-04 12:38:00 +0800
categories: leetcode, string manipulation, number manipulation
---

The problem:

> Given a positive integer num consisting only of digits 6 and 9.

> Return the maximum number you can get by changing at most one digit (6 becomes 9, and 9 becomes 6).

**Example 1:**

    Input: num = 9669
    Output: 9969
    Explanation:
    Changing the first digit results in 6669.
    Changing the second digit results in 9969.
    Changing the third digit results in 9699.
    Changing the fourth digit results in 9666.
    The maximum number is 9969.

**Example 2:**

    Input: num = 9996
    Output: 9999
    Explanation: Changing the last digit 6 to 9 results in the maximum number.

**Example 3:**

    Input: num = 9999
    Output: 9999
    Explanation: It is better not to apply any change.

**Solution**

-   Convert the number into a string
-   Split the string into an array
-   If there's no "6" in the array, we don't have to do any work. Join the the array, turn it back into a number and return it
-   If not, we'll find the _first_ "6" we come across and turn it into a "9", ensuring we always have the biggest possible number. Return the number.

          const maximum69Number  = (num) => {
              let numArr = num.toString().split("");
              let changed = false;
              let i = 0;

              if(!numArr.includes("6")) return parseInt(numArr.join(""));

              while(!changed) {
                  if(numArr[i] === "6") {
                      numArr[i] = "9"
                      changed = true;
                  }
                  i++;
              }

              return parseInt(numArr.join(""))
          };
