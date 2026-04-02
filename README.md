# deliberate-coder

```bash
npx skills add BeLazy167/deliberate-coder
```

An [agent skill](https://agentskills.io) that forces AI coding agents to analyze assumptions, edge cases, and failure modes **before** writing code.

## What it does

Instead of jumping straight to implementation, the agent will:

1. State assumptions about input and environment
2. Enumerate failure modes and adversarial scenarios
3. Identify maintenance hazards
4. **Then** write minimal, correct code
5. Self-validate against its own analysis

Rigor scales automatically — a 5-line utility gets a couple of inline assumptions, while payment processing gets the full treatment.

## Install

```bash
npx skills add BeLazy167/deliberate-coder
```

## Compatibility

Works with any agent that supports the [Agent Skills](https://agentskills.io) format:

Claude Code, Cursor, Codex, Gemini CLI, Windsurf, Goose, OpenCode, Roo Code, and [40+ others](https://agentskills.io/home).

## When it activates

- Implementing business logic, parsers, auth, payments, rate limiters, data validation
- User asks for "bulletproof", "correct", or "rigorous" code
- Any task where correctness matters more than speed

## When it stays out of the way

- Quick prototyping and idea validation
- Boilerplate and config changes
- Refactoring existing tested code
- User explicitly wants "quick and dirty"

## Example output

When you ask the agent to implement something non-trivial, it produces:

```
## Assumptions
- Input is a UTF-8 string, max 10KB
- Called from a single-threaded context

## Edge Cases
- Empty string → return early with default
- Malformed unicode → reject with descriptive error

## Failure Modes
- Network timeout → retry with exponential backoff, max 3 attempts
- OOM on large input → enforced size limit at entry point

## Implementation
[minimal, correct code]

## What This Doesn't Handle
- Concurrent access (caller's responsibility)
- Inputs > 10KB (rejected at validation layer)
```

## License

MIT
