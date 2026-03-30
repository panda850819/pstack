Debug and fix this issue: $ARGUMENTS

Follow this sequence:

1. Use the eng agent (read agents/eng.md) to investigate:
   - Search learnings for related past issues
   - Trace the data flow to find root cause
   - Iron Law: no fix without root cause
   - Iron Law: 3 failed attempts = stop and escalate
2. Implement the fix (minimal diff)
3. Run /ps-review
4. Run /ps-ship
5. If the debug took > 10 minutes or the solution was non-obvious, run /ps-compound
