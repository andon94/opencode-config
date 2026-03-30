---
description: Run full orchestrated feature workflow
agent: orchestrator
---
Execute the global delivery workflow for this feature request:

$ARGUMENTS

Required sequence:
1. docs-researcher gathers latest docs and constraints
2. architect creates a reviewable TDD/implementation contract
3. present the TDD to me for review and wait for approval
4. frontend-coder and backend-coder implement in parallel when needed
5. tester validates
6. reviewer performs quality review
7. security-expert performs final security gate

If any stage fails, route findings back to the relevant coder, apply fixes, and re-run downstream validation until all checks pass.
