---
name: karpathy-guidelines
description: >
  Reference documentation for the four Karpathy coding principles. In a
  Hermes workspace context, these principles are absorbed into the skill
  suite — load code-craft-principles instead. This file exists for
  documentation and AGENTS.md generation purposes.
license: MIT
---

# Karpathy Guidelines — Reference

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on LLM coding pitfalls.

**If you are running in a Hermes Agent workspace:** These principles are absorbed into the workspace skill suite. Do not load this skill separately. Load the following atoms instead:

- `code-craft-principles` — Think Before Coding, Simplicity First, Surgical Changes
- `test-driven-development` — Goal-Driven Execution (RED/GREEN/REFACTOR cycle)
- `writing-plans` — verifiable success criteria, bite-sized tasks

The `AGENTS.md` in this repo is the synthesized drop-in for projects that don't have the Hermes skill suite available.

---

## The Four Principles (Reference)

### 1. Think Before Coding
Don't assume. Don't hide confusion. Surface tradeoffs. State assumptions explicitly, present multiple interpretations, push back when warranted, stop when confused.

### 2. Simplicity First
Minimum code that solves the problem. Nothing speculative. No features beyond what was asked, no abstractions for single-use code, no flexibility that wasn't requested. If 200 lines could be 50, rewrite it. **The test:** Would a senior engineer say this is overcomplicated?

### 3. Surgical Changes
Touch only what you must. Clean up only your own mess. Don't improve adjacent code. Don't refactor things that aren't broken. Match existing style. **The test:** Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution
Define success criteria. Loop until verified. Transform imperative tasks into verifiable goals. For multi-step tasks, state a brief plan with explicit verify steps. Strong success criteria let the agent loop independently.

---

## Tradeoff Note

These guidelines bias toward **caution over speed**. For trivial tasks, use judgment — not every change needs the full rigor. The goal is reducing costly mistakes on non-trivial work.
