## Handoff

```bash
Whenever I say "wrap up" or context is running low, create/update 
handoff.md in the project root with this exact structure:

## Goal
[High-level objective + current sub-task]

## Status
- What works right now (verified, not assumed)
- What's broken / incomplete

## Files in progress
- path/to/file.ext — what's being changed and why (not just "editing X")

## Failed attempts
For each: what I tried, the exact error/output, and WHY it failed 
(wrong assumption, missing dependency, etc.) — not just "didn't work"

## Environment state
- Branch, uncommitted changes, running services/processes, 
  relevant env vars (no secrets)

## Next step
The single most concrete next action, with the exact command if 
possible — not "investigate further" but "run X, check Y"

## Open questions
Decisions that need my input before continuing

Rules:
- If handoff.md already exists, overwrite it (don't append/duplicate)
- Be concise — bullet points, no narrative prose
- Don't guess at "what works" — only state what was actually verified
```

```bash
Before we end this session, write a handoff.md file that capture:

- the Goal we're working toward
- current state of the code
- files you're actively editing
- everything you've tried that failed
- the next step you'd tak
```


```bash
Read handoff.md and pick up exactly where it left off
```
