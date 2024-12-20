+++
date = '2024-12-19T09:19:05+01:00'
draft = true
title = 'Optimized Shower Order'
math = true
+++

## Introduction
The idea of this post comes from a shower thought (literally), it's about finding the most optimized order of people taking a shower, such that the total amount of 'waiting to take a shower' time is as small as possible (if you share a shower you can relate).

Of course this is a very trivial problem to solve, but I just wanted to try out using LaTeX in a post.

Note: I'm not a qualified mathematician, so take this with a grain of salt.

## First idea
The first idea that I had was that the order of people taking the shower should be from fastest to slowest, because as the 'fastest showerers' finish earlier, they effectively eliminate people from the set of people currently 'waiting to take a shower'.

For example, take 3 people: 

\[\text{x (10 minutes), y (15 minutes), z (20 minutes):}\]

\[\text{By increasing order we have: }
2 \cdot x + y = 2\cdot10 + 15 = 35 \text{ minutes of total waiting}
\]

\[\text{By decreasing order we have: }
2 \cdot z + y = 2\cdot20 + 15 = 55 \text{ minutes of total waiting}
\]


## Mathematical representation
The smallest amount of time wasted waiting to take a shower is given by the following:
\[
\text{Let the ordered set be } S = \{ x_1, x_2, \dots, x_n \} \text{, where } x_1 \leq x_2 \leq \dots \leq x_n.
\]
\[
\text{The sum can be expressed as:}\\
\sum_{i=1}^{n} x_i \cdot (n - i)
\]
## Quick references

### Links
-