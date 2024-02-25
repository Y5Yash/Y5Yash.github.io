---
layout: note
title: MoonMath manual
date: 2023-12-24
categories: []
---

# Chapter 3

# 3.2
**Integer factorization problem** is a hard problem. Naive approach - just divide the given number by all prime numbers in some (ascending) order. No known method much faster than the naive approach exists. As multiplication is fast, this is a *one-way function*. Complexity is not polynomial in the number of bits *b* for integer *n*. Note that Shor's algorithm takes *O(b^3)* time and *O(b)* space - polynomial time in bits on a quantum computer.

Methods to compute Euclidean Division for integers are called **integer division algorithms**. Probably the best-known algorithm is the so-called *long division*.

**Extended Euclidean Algorithm**: $$r_0 = a; s_0 = 1; t_0 = 0 ;; r_1 = b; s_1 = 0; t_1 = 1 ;; r_{i+1} = r_{i-1} - q_i r_i; s_{i+1} = s_{i-1} - q_i s_i; t_{i+1} = t_{i-1} - q_i t_i$$. Stop computation when $r_{k+1} = 0$ Here, the $gcd(a,b) = r_k = a s_k + b t_k$.

Bit length $k$ of integer $n$ notation: $k := |n|_2$.

**Hamming weight** of an integer is the number of 1s in its binary representation.

**Fermat's Little Theorem** states that if $k \in Z$ and $p \in P$ are coprime, then $k^p \congruent k (mod\ p)$

**Lagrange Interpolating Polynomial** is the unique polynomial of the lowest degree that interpolates a give set of data.