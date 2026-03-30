# Brief Formats by Agent Type

## Dev / Build Agent — Sprint Brief

```markdown
# Brief: [TASK_ID] — [One-line task description]

## Before doing anything else
Update your team's status dashboard:
- Set your status to "working"
- Set your task to "[one line describing what you're about to do]"

Before starting ANY work: ask clarifying questions until you are 95% confident
you can complete this task successfully. Do not start until you have that confidence.

## Task
[One clear sentence describing what needs to be built/fixed]

## Context
[Only what changes what the agent does — 2-5 sentences max]

## Acceptance Criteria
AC1: [specific, testable condition]
     Verify: [how to check]
AC2: [specific, testable condition]
     Verify: [how to check]
AC3: [specific, testable condition]
     Verify: [how to check]

## Constraints
- [What must not break]
- [Files/services that must not be touched]

## Non-Goals
- [Explicitly out of scope]

## Read First
- [relevant context files]
- [spec.md if this is a proof-loop task]

## Environment
- Repo: [path or SSH command]
- Branch: [branch name]
- Service: [restart command if needed]

## When completely finished
Update your team's status dashboard:
- Set your status to "done"
- Set your task to "[summary of what shipped]"

Then notify the orchestrator:
[your system's completion notification command]
```

---

## Code Review Agent Brief

```markdown
# Review Brief: [TASK_ID]

Before reviewing, ask clarifying questions if anything is unclear (95% confidence rule).

## Your Role
You are the verifier. You DO NOT write production code. You DO NOT propose fixes inline.
You verdict each AC and document problems precisely so the dev agent can fix them.

## Read First
- .agent/tasks/[TASK_ID]/spec.md — the frozen ACs
- Any existing verdict.json

## Live Test Required
This is NOT a static code review. You must:
1. Connect to the running app at [URL]
2. Log in with test credentials
3. Verify each AC by actually using the feature

## Acceptance Criteria to Verify
[Copy ACs from spec.md]

## Output
Write to .agent/tasks/[TASK_ID]/verdict.json:
{
  "task_id": "[TASK_ID]",
  "phase": "review",
  "agent": "reviewer",
  "timestamp": "[ISO]",
  "overall": "PASS|FAIL",
  "criteria": [
    { "id": "AC1", "status": "PASS|FAIL|UNKNOWN", "note": "[evidence]" }
  ]
}

If any AC is FAIL or UNKNOWN, write .agent/tasks/[TASK_ID]/problems.md with
specific file/line references.
```

---

## Acceptance Test Agent Brief

```markdown
# Test Brief: [TASK_ID]

Before starting, verify:
1. [migration/schema check if applicable]
   → Must show no pending changes. If pending: STOP.

## Read First
- .agent/tasks/[TASK_ID]/spec.md
- .agent/tasks/[TASK_ID]/verdict.json (reviewer's findings)
- .agent/tasks/[TASK_ID]/problems.md (if exists)

## Run Full Suite
[test command — must run ALL previous tests, not just new ones]

Report format: "Sprint 1 ✅ · Sprint 2 ✅ · Sprint N ⚠️"
ALL previous tests must pass before new results mean anything.

## Update Verdict
Update .agent/tasks/[TASK_ID]/verdict.json with test findings.
If FAIL: update problems.md with specific test failures.
```

---

## Research Agent Brief (Cron)

```markdown
Research [specific topic] and report findings.

Read first:
- [relevant observations/memory files]
- [context files for this domain]

Focus: [specific angle or question]
Depth: [surface overview / deep dive / comparison]
Output: [where and how to deliver — message, file, etc.]
Source quality: every source needs URL + publication date.
```

---

## Orchestrator Cron Job

```markdown
You are [role]. [Specific automated task description].

[Exact steps with file paths, commands, or API calls]

If everything is as expected: reply NO_REPLY.
If [condition]: [specific action — send message, restart service, etc].
```

---

## Token Efficiency Checklist

Before delivering any brief, check:
- [ ] Can any sentence be removed without changing what the agent does?
- [ ] Are all file paths absolute (not relative or vague)?
- [ ] Are all machine/environment references explicit?
- [ ] Are ACs testable by a third party who didn't write them?
- [ ] Is the 95% confidence gate included (for dev agents)?
- [ ] Are status update blocks included (start + end)?
