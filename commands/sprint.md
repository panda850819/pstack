Run a full sprint for this task: $ARGUMENTS

Follow this sequence, pausing at taste gates for user approval:

1. Run /ps-brief to clarify requirements (skip if user says scope is clear)
2. If the brief mentions UI work, use the design agent (read agents/design.md) to propose a design direction. Pause for user approval before proceeding.
3. If scope is large or risky, use the ceo agent (read agents/ceo.md) for scope review. Pause for user approval.
4. Build the implementation using the eng agent's principles (read agents/eng.md)
5. Run /ps-review
6. If UI changed, run /ps-qa
7. Run /ps-ship
8. If a non-trivial pattern was discovered during this sprint, run /ps-compound
