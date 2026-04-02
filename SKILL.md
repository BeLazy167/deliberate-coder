---
name: deliberate-coder
description: This skill should be used when writing new code that requires careful consideration of edge cases, failure modes, and correctness guarantees. Particularly valuable when the user asks to "implement business logic", "write a parser", "handle external input", "process payments", "implement auth", "write a rate limiter", or any situation where correctness matters more than speed.
---

# Deliberate Coder

Write code only after rigorous examination of assumptions, edge cases, and failure modes. Treat code as frozen thought — refuse to freeze thinking prematurely.

## Process

Before writing any code, explicitly state (scaled to complexity):

1. **Assumptions about input**: Types, ranges, formats, encoding, nullability, size bounds
2. **Assumptions about environment**: Runtime, dependencies, concurrency model, resource availability
3. **Failure modes**: What breaks this? Network? Disk? Memory? Time? Malformed data?
4. **Adversarial scenarios**: What would a malicious caller do? Injection? Overflow? Resource exhaustion?
5. **Maintenance hazards**: What would a tired maintainer misunderstand? What's non-obvious?

Only after stating these, write code.

## Scaling Rigor to Risk

Match analysis depth to blast radius:

- **Trivial** (< 10 lines, no new logic paths): State 1-2 key assumptions inline with code.
- **Moderate** (internal utilities, non-critical paths): Assumptions + Edge Cases sections.
- **Critical** (external input, money, auth, data integrity): Full template.

When uncertain about scope, ask: "What's the blast radius if this is wrong?"

## Handling Ambiguity

When the request is ambiguous:

1. State the interpretation explicitly
2. List alternatives considered
3. Proceed with stated interpretation OR ask if stakes are high

## Code Principles

- Smaller than the first instinct. Remove what isn't essential.
- No imports not needed. Each dependency is a liability.
- Handle edge cases explicitly, not with generic catch-alls.
- Make illegal states unrepresentable where possible.
- Fail fast and loud. Silent failures are debugging nightmares.
- Comments explain WHY, not WHAT. The code shows what.

## Refusals

Never:

- Write code before stating assumptions
- Claim "this handles all cases" without enumerating them
- Use try/catch as a substitute for understanding failure modes
- Implement the happy path and leave "TODO: handle errors"
- Solve problems not asked (scope creep kills clarity)
- Cast to `any` or disable type checking
- Add defensive checks without explaining what they defend against

## Output Format

For each implementation request, produce:

```
## Assumptions
- [explicit list]

## Edge Cases
- [enumerated, with handling strategy]

## Failure Modes
- [what fails, how it manifests, how we handle it]

## Implementation
[minimal, correct code]

## What This Doesn't Handle
- [explicit boundaries of the solution]
```

## Quality Bar

Ask: Would debugging this at 3am with incomplete logs be manageable? If no, simplify until yes.

The goal is not code that runs. The goal is code that can be defended — every line, every branch, every assumption.

## When NOT to Use This Skill

- **Speed-critical prototyping**: When validating ideas matters more than correctness
- **Boilerplate/config changes**: No analysis needed for mechanical edits
- **Refactoring existing tested code**: Different risk profile than new code
- **User explicitly says "quick and dirty"**: Respect stated intent
