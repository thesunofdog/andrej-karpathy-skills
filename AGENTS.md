# AGENTS.md

Behavioral guidelines for AI coding agents working in this codebase. Derived from Andrej Karpathy's observations on LLM coding failures, customized for Jordan's workspace.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

---

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask — don't run with an interpretation and hope it was right.
- If multiple interpretations exist, present them. Don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

**In this workspace:** Never silently pick an interpretation on ops scripts, briefing logic, or vault writes. These touch production. A clarifying question before implementation is always cheaper than a rewrite after.

---

## 2. Simplicity First

**Minimum code that solves the stated problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

**The test:** Would a senior engineer say this is overcomplicated? If yes, simplify.

**In this workspace:** Ops scripts must stay readable by a non-expert. Flat beats clever. If a function requires understanding a class hierarchy to follow, it's too complex.

---

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting — even if you'd do it differently.
- Don't refactor things that aren't broken.
- Match existing style, even if it's ugly.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports, variables, and functions that **your changes** made unused.
- Don't remove pre-existing dead code unless asked.

**The test:** Every changed line should trace directly to the user's request. If a line changed and you can't explain why the request required it, undo it.

**In this workspace:** This applies especially to the briefing pipeline, vault writes, and cron scripts. An unsolicited "improvement" to adjacent logic can break something quietly. Do the stated task. Nothing else.

---

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform imperative tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Workspace Conventions

**Do only the stated task.** Jordan's instruction is explicit: "Do ONLY stated task." If you notice adjacent improvements, mention them — don't implement them.

**Atomic commits.** One logical change per commit. Commit message format: `type(scope): description`. No bundling unrelated changes.

**Plan before multi-file changes.** For any task touching 3+ files or introducing a new module, state a brief plan and get confirmation before writing code.

**Frontier review gate.** Code review uses Claude Opus or GPT-5.1-Codex. Never mid-tier models. For major audits: Opus review before any shared-state writes.

**Tests are mandatory.** New code ships with tests. Touch it, test it. No exceptions without explicit instruction.

**TDD.** Write the failing test first. Watch it fail. Write minimal code to pass. See Goal-Driven Execution above.

---

## Cross-References (Hermes Skill Suite)

If you have access to the Hermes skill suite, the full elaboration of these principles lives in:

- `code-craft-principles` — Think Before Coding, Simplicity First, Surgical Changes (with Jordan-specific extensions)
- `test-driven-development` — RED/GREEN/REFACTOR cycle, Iron Law, common rationalizations
- `writing-plans` — implementation plan structure, bite-sized tasks, verifiable success criteria
- `requesting-code-review` — automated pre-commit pipeline (static scan + subagent reviewer + fix loop)
- `code-review` — what to look for: security, error handling, logic, quality, surgical changes, testing
- `ops-code-review-workflow` — multi-pass review for Express Tire ops scripts (Opus + Codex, institutional findings log)

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.
