---
title: Funny sounding math and computing concepts
created: 2024-07-23
updated: 2025-11-27
tags: [catalog, concepts, math, computing]
status: draft
summary: A growing list of mathematically or computationally serious ideas that happen to have names that sound funny.
---

# Context
This note collects concepts from mathematics, computer science, and related fields that sound funny, but that describe serious and important ideas.

# Content

## Busy Beaver Function
- Domain: computability theory, theoretical computer science.
- Rough idea: for each natural number \(n\), consider all halting Turing machines with \(n\) states and a fixed alphabet. Among them, take the machine that writes the largest number of 1s on the tape before halting. The busy beaver function \( \Sigma(n) \) is that maximum number of 1s.
- Key property: the function grows faster than any computable function. There is no general algorithm that can compute all values of the busy beaver function.
- Relation to undecidability: if we could compute the busy beaver function for all inputs, we could solve the halting problem. This is impossible, so the busy beaver function is non-computable.

## Multi-Armed Bandit Problem
- Domain: probability, statistics, reinforcement learning, decision theory.
- Setup: imagine a row of slot machines (the “arms”), each with an unknown payout distribution. You repeatedly choose one arm to pull to obtain rewards over time.
- Core challenge: balance exploration (trying different arms to learn their payouts) with exploitation (choosing the best-known arm to maximize reward).
- Typical goals: maximize cumulative reward or minimize regret (the difference between your accumulated reward and the reward you would have obtained by always playing the best arm).
- Relevance: the problem models real-world settings such as online ad selection, clinical trials, and adaptive experimentation in software and product design.

## Pancake Sorting
- Domain: algorithms, combinatorics.
- Setup: you have a stack of pancakes of different sizes. You can insert a spatula under some prefix of the stack and flip that whole prefix. The goal is to sort the stack by size using as few prefix flips as possible.
- Operation: a move is defined as choosing a position \(k\) and reversing the order of the top \(k\) items in the stack.
- Complexity questions: for a stack of \(n\) pancakes, the pancake number asks for the maximum number of prefix flips needed to sort any arrangement of \(n\) items. Exact values are only known for relatively small \(n\).
- Variants: burnt pancake sorting adds an orientation (burnt side up or down) to each pancake, and flips reverse both order and orientation, leading to related but different bounds.