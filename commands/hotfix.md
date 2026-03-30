---
description: Run urgent hotfix workflow with strict minimal-change policy
agent: orchestrator
---
Treat this as a production hotfix request:

$ARGUMENTS

Hotfix goals:
- Ship the smallest safe fix.
- Minimize blast radius and regression risk.
- Produce rollback and verification steps.

Required workflow:
1. docs-researcher performs a fast docs pass only for touched frameworks/APIs.
2. architect produces a reviewable mini-TDD: bug statement, likely root cause, affected surfaces, acceptance test, rollback plan.
3. Present the mini-TDD to me for review and wait for approval before implementation.
4. Assign the owning lane:
   - frontend-coder, backend-coder, or both only if the issue truly spans both.
5. tester reproduces the bug before the fix, verifies the fix after changes, then runs targeted tests and a short smoke check.
6. reviewer validates minimality of diff, contract compliance, and regression risk.
7. security-expert runs final security gate. Escalate to full security review if auth, authorization, validation, secrets, payments, or external calls are touched.

Failure loop:
- Any failure from tester/reviewer/security-expert must return to the owning coder with explicit findings.
- Re-run tester and reviewer after each fix cycle until all checks pass.

Hotfix constraints:
- No opportunistic refactors.
- No broad dependency upgrades unless required for the fix.
- No API contract changes unless unavoidable; if unavoidable, document impact.

Final output must include:
1. Root cause summary
2. Files changed and why
3. Verification evidence
4. Residual risk
5. Rollback procedure
