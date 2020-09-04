---
layout: post
title: 'A "bit" about Binary and Bitwise Operators'
date: 2020-09-04 16:07:08 +0800
categories: leetcode, bitwise, binary
---

I used to think programming was all ones and zeroes.

Which is why I never took an interest in it. "If I'm already bad at math - I probably won't be able to program", I reasoned.

After some research (and much to my surprise!), modern programming languages read a lot like English. So began my foray into the web development world.

Why then, has it taken me this long to try and understand binary? Well, again it came down to pre-conceived notions.

Recently, I struggled with a binary-related Leetcode question and decided enough is enough.

Below are some of my notes about binary and bitwise operators.

Before we delve into binary and why it's used in computers, we need to talk about base-10.

#### **Base-10 Positional Notation (Decimal)**

Used by ancient civilizations till present day. Its widespread prevalence is possibly due to the fact that humans have 10 fingers.

There are only really 10 symbols in a base-10 system: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9.

How then, do we represent a number that is greater than 9?

    000 ... 009 // we reset the right most digit and increment the digit to its left
    010 ... 019 ...
    099 ... // reset the rightmost two digits and increase the next digit

#### **Base-2 Positional Notation (Binary)**

Only has two symbols, 0 and 1 (or, off and on). Counting in binary looks like this:

    0, 1, 10, 11, 100, 101, 110, 111, 1000.. // 0 to 8

In a binary system, each digit represents an increasing power of 2, with the rightmost digit representing 2(0).

    101010
    [1 * 2(5)] + [0 * 2(4)] + [1 * 2(3)] + [0 * 2(2)] + [1 * 2(1)] + [0 * 2(0)]
    [1 * 32]   + [0 * 16]   + [1 * 8]    + [0 * 4]    + [1 * 2]    + [0 * 1]
    32 + 0 + 8 + 0 + 2 + 0 = 42
    (101010)10 = (42)2

**Why do computers use binary?**

Early computers used binary due to physical limitations. Everything that is done by a computer consists of electrical charges produced by micro-transistors - switching from off to on, and vice versa. Since the earliest computers were made for counting, a binary system proved to be efficient for these purposes. For example, with only eight switches turned on, it was possible to represent a number as high as 255!

    11111111

Additionally, binary electronics either have a current, or they don't. Assuming we used a base-3 system - each transistor would need to be able to interpret a range of values representing "some" (or, 0, 1 and 2). At some point, electronics degrade; a component may be unable to transmit the required modulation to produce a "2", and our logic gates stop working as intended. And that's what we don't use base-10 - a base-10 system would need to be able to reflect 10 different states!

**Binary and ASCII**

If binary consists only of numbers, how do computers represent letters, or strings?

ASCII (American Standard for Information Interchange) is a character encoding standard for electronic communication. Since computers only understand numbers, each character must be represented as a number. ASCII, then, is a mapping of each character to a corresponding number.

    1000001 = 65 = A
    1100001 = 97 = a

**Converting decimals to binary**

Take a number and keep dividing it by 2. We'll use the quotient for the next iteration and keep track of the remainder (important: this will end up being our binary representation!)

Example:

| 37 / 2 | Quotient: 18| Remainder: 1|
| 18 / 2 | Quotient: 9 | Remainder: 0|
| 9 / 2 | Quotient: 4 | Remainder: 1|
| 4 / 2 | Quotient: 2 | Remainder: 0|
| 2 / 2 | Quotient: 1 | Remainder: 0|
| 1 / 2 | Quotient: 0 | Remainder: 1|

We need to look at the remainder from bottom to top i.e. 100101.

And there's our binary number!

Here's another one for good measure:

| 22 / 2 | Quotient: 11 | Remainder: 0|
| 11 / 2 | Quotient: 5 | Remainder: 1|
| 5 / 2 | Quotient: 2 | Remainder: 1|
| 2 / 2 | Quotient: 1 | Remainder: 0|
| 1 / 2 | Quotient: 0 | Remainder: 1|

#### **Bitwise Operators**

| Bitwise OR | \ |
| Bitwise AND| & |
| Bitwise XOR| ^ |
| Bitwise NOT| ~ |
| Shift left | <<|
| Shift right| >>|

Some _Javascript-specific_ tips:

You can convert an integer into its stringified binary equivalent by using a .toString() and passing it the argument 2.

    let myNum = 23;
    myNum.toString(2); // "10111"

You can also take a binary string and convert it back to a decimal number by using .parseInt(), passing 2 as the second argument.

    let myBinaryString = "1100";
    parseInt(myBinaryString, 2); // 12

There's also an ES6 way to write binary:

    let myBinary = 0b1100; // 12

**Bitwise OR**

> Bitwise OR returns 1 if either bit is 1, and 0 if both are not.

I kept seeing this definition on the Internet but what exactly does it mean?

Let's take two numbers, 55 and 47.

    let a = 55;
    let b = 47;
    console.log(a.toString(2)); // "110111"
    console.log(b.toString(2)); // "101111"

What the bitwise \| operator does is it looks through both of the binary numbers, bit by bit:

    110111
    101111

    // column visualisation
    |1|1|0|1|1|1| // first row
    |1|0|1|1|1|1| // second row

Is there a 1 in the first position of the first column in either the first or second row? Yes, so we'll output a 1 in that position. Is there a 1 in the second position of the second column in either the first or second row? Also yes. Keep going until we reach the last digit, and we'll end up with something like this:

    111111
    55 | 47 // 63

**Bitwise AND**

> Bitwise AND returns 1 only if both bits are 1. Otherwise, it returns 0.

Let's use another example.

    let a = 5;
    let b = 17;
    console.log(a.toString(2)); // "00101"
    console.log(b.toString(2)); // "10001"

    |0|0|1|0|1|
    |1|0|0|0|1|

Is there 1 in the first position of the first column in the first row AND the second row? No. It only exists in the second row. _Both_ rows have to be 1 to return 1. After going through each value, we'll get something like this:

    00001;
    5 & 17; // 1

**Bitwise XOR**

> Bitwise XOR (eXclusive OR) returns 1 only if one bit is 1. Otherwise, it returns 0.

    let a = 33;
    let b = 41;
    console.log(a.toString(2)); // "100001"
    console.log(b.toString(2)); // "101001"

    001000;
    33 ^ 41; // 8

**Bitwise NOT**

> Bitwise NOT flips the bits. It also flips the sign.

To be perfectly honest, I still don't fully understand this one. Let's see what Wikipedia has to say:

> Bitwise NOT, or complement, is a unary operation that performs logical negation on each bit, forming the ones' complement of the given binary value. Bits that are 0 become 1, and those that are 1 become 0. For example:

    NOT 10101011  (decimal 171)
    = 01010100  (decimal 84)

But when I ran it in my console, I got -172 instead.

What we do know:

    n = -(n + 1)

So, given any number, if we ~ the number, we receive the negative number + 1.

**Bitwise Left Shift**

> Bitwise left shift - left operand specifies the number and the right operand specifies the number to be shifted left. Zero bits are added to the right and excess bits from the left are discarded.

What does this mean? Well, take the number 33.

    let a = 33;
    a.toString(2); // "100001"

Let's say we want to shift 1 bit to the left, we'll end up with:

    let b = a << 1;
    b.toString(2); // "1000010"
    b; // 66
    b = a << 2;
    b; // 132

    let c = 21;
    c.toString(2); "10101"
    let d = c << 3;
    d.toString(2); "10101000"
    d; // 168

You'll notice a pattern here: it seems that the left shift can be used to multiply an integer by powers of 2.

**Bitwise Right Shift**

> Bitwise right shift - number is shifted to the right by filling the left side with zeroes. Excess bits on the right are discarded.

    let a = 12;
    a.toString(2); "1100"
    let b = a >> 1;
    b.toString(2); "110"
    b; // 6

    let c = 44;
    c.toString(2); "101100"
    let d = c >> 2;
    d.toString(2); "1011"
    d; //

Similarly, the right shift can be used to divide a bit pattern by 2.

---

Phew! That was a lot. If you've read this far, thanks for accompanying me on my journey into binary. I think we'll leave off here - maybe next time we'll talk about hexadecimal systems(lol).

Peace!

**Credits and Miscellaneous Resources**

-   [Binary Numbers and Base Systems as Fast as Possible (Video)](https://www.youtube.com/watch?v=LpuPe81bc2w&t=181s)
-   [Why Do Computers Use 1s and 0s? Binary and Transistors Explained (Video)](https://www.youtube.com/watch?v=Xpk67YzOn5w&t=201s)
-   [Binary Number (Wikipedia)](https://en.wikipedia.org/wiki/Binary_number)
-   [How to Read and Write Binary In 5 Minutes (Video)](https://www.youtube.com/watch?v=Ieq8AR8krrA&t=197s)
-   [Javascript Bitwise Operators (Article)](https://www.programiz.com/javascript/bitwise-operators)
-   [JS Bitwise Operators and Binary (Video)](https://www.youtube.com/watch?v=RRyxCmLX_ag)
-   [Decimal to Binary Converter](https://www.rapidtables.com/convert/number/decimal-to-binary.html)
-   [What is ASCII code, where is it used, and why? (Quora)](https://www.quora.com/What-is-ASCII-code-where-is-it-used-and-why?share=1)
-   [Why do computers still use Binary instead of a Base 5, 10, 12 system? (Reddit thread)](https://www.reddit.com/r/askscience/comments/254wpp/why_do_computers_still_use_binary_instead_of_a/?utm_source=amp&utm_medium=&utm_content=post_title)
-   [How important are binary numbers to a prgrammer (Quora)](https://www.quora.com/How-important-are-binary-numbers-to-a-programmer#:~:text=You%20should%20absolutely%20learn%20binary,and%20*that*%20is%20important.)
-   [Bitwise Operations in C (Wikipedia)](https://en.wikipedia.org/wiki/Bitwise_operations_in_C)
