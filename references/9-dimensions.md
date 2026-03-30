# 9 Dimensions of Intent

Extract these before writing any brief. Every dimension that's missing is a potential failure point.

---

## 1. Task
**What is the agent being asked to DO?**
- One verb, one outcome
- "Implement X", "Fix Y", "Research Z", "Review W"
- If there are multiple tasks: split into multiple briefs

**Bad:** "Work on the translation system"
**Good:** "Fix the formSchemaTranslated field not being populated for the target locale"

---

## 2. Input
**What does the agent need to start?**
- Files, repos, URLs, data, credentials
- Which machine or server?
- Which branch, directory, service?

**Example:** `ssh user@host 'cd /path/to/repo'` — not just "in the repo"

---

## 3. Output
**What should exist when the agent is done?**
- Files created/modified
- Services restarted?
- DB records updated?
- Git commit pushed?
- Status updated?

---

## 4. Constraints
**What must NOT break?**
- Existing functionality (specify which features/sprints)
- Files that must not be overwritten
- DB records that must not be deleted
- Services that must stay running

---

## 5. Context
**What does the agent need to understand about the broader situation?**
- Why this task exists
- What failed before
- What was tried already
- Architecture decisions that affect this task

Keep this SHORT. Only context that changes what the agent does.

---

## 6. Audience / Role
**Who is this brief for?**
- Dev/build agent (complex implementation)
- Junior dev agent (smaller scope, guided)
- Code review agent (verdict only — NOT implementation)
- Acceptance test agent (testing only — NOT review)
- Research agent (information gathering)
- Analysis agent (data interpretation)
- Orchestrator cron job (automated recurring task)

Role determines: tone, expected tools, level of autonomy, what they should ask vs decide.

---

## 7. Memory / Prior Context
**What should the agent read before starting?**
- Relevant context files
- Prior commits or decisions
- The spec.md if this is a proof-loop task
- Code dependency/blast radius analysis

---

## 8. Success Criteria
**How does the agent (and you) know it's done?**
- AC1, AC2, AC3 — explicit, testable, specific
- Regression suite must pass?
- Visual verification required?
- DB state expected?

If you can't write a testable AC, the task isn't defined well enough yet.

---

## 9. Examples
**Are there examples that clarify the expected behaviour?**
- Before/after screenshots
- Expected output format
- Similar completed tasks to reference
- Known-good code patterns to follow

---

## Quick Extraction Prompt

When someone asks for help writing a brief, ask:

> "Before I write this brief, let me extract the key dimensions:
> 1. What exactly should be done? (one sentence)
> 2. What does the agent need access to? (files, machines, branches)
> 3. What should exist when it's done?
> 4. What must not break?
> 5. Any critical context the agent needs?
> 6. Which agent/role is this for?
> 7. Which files/docs should the agent read first?
> 8. What are the acceptance criteria? (AC1, AC2, AC3)
> 9. Any examples or reference points?"

Ask only the questions where the answer isn't already obvious from context.
Max 3 questions per round.
