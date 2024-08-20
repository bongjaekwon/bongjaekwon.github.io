---
title: Linear Algebra(1) Fields
feed: hide
date: 20-08-2024
---
**Before starting**

This post series is a summary of Mark S. Gockenbach's _Finite-Dimensional Linear Algebra_. The purpose of this series is to carefully explain vector spaces and linear operators and to show how these abstract concepts are useful in practical applications. We will prove all the properties discussed, which means we need to start with a set of basic rules—specifically, the axioms of a field. Scalars, which are used with vectors, must belong to this field.


**Definition**

Most people are familiar with real numbers (like 1, -5, or 3.14). These are what we usually think of when we hear "number." Complex numbers are another type of number, such as α+βi, where α and β are real numbers, and i is the square root of −1. Complex numbers are very important in higher math because they often come up even when dealing with real numbers. For example, later we’ll see how they help in understanding matrices. They’re also useful in real-world problems, like in signal processing, where they make calculations easier.

A less familiar set of numbers is formed by integers modulo a prime number ppp. This set includes numbers from 0 to p−1, with addition and multiplication performed modulo p.

For example, if p=7, the set is {0, 1, 2, 3, 4, 5, 6}. When performing addition or multiplication, you calculate the result and then take the remainder when divided by 7.

- For instance, 6+5 equals 11, but modulo 7, the result is 4.
- Similarly, 6×5 equals 30, but modulo 7, the result is 2.

This set is denoted by Zp​ and is important in discrete mathematics, often used instead of real numbers R or complex numbers C.