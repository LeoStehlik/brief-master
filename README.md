# brief-master

Write sharp, precise agent briefs for OpenClaw. Zero wasted tokens. Zero vague instructions.

Every bad brief costs you a rework cycle. brief-master extracts 9 dimensions of intent, asks max 3 clarifying questions, applies the right format for your target agent, runs a token efficiency audit, and delivers one clean brief ready to fire.

Built for OpenClaw's multi-agent workflow: dev agents, code reviewers, testers, researchers, and cron jobs.

Inspired by [prompt-master](https://github.com/nidhinjs/prompt-master). Built as our own OpenClaw-native implementation.

---

## The Problem

Every wasted token is a wasted API call.
Every vague word is a future bug.
Every missing acceptance criterion is a future rework cycle.

"Improve the translation system" is not a brief.
"Fix formSchemaTranslated being NULL for German locale — AC1: all 50 prompt rows have formSchemaTranslated populated after running translate/de endpoint" is a brief.

---

## The Pipeline

1. Detect the target agent and runtime
2. Extract 9 dimensions of intent
3. Ask max 3 clarifying questions (only if critical info is missing)
4. Apply the right format for the target agent
5. Run token efficiency audit
6. Deliver one clean, ready-to-use brief

---

## The 9 Dimensions

1. **Task** - what exactly should be done (one verb, one outcome)
2. **Input** - what does the agent need to start (files, machines, branches)
3. **Output** - what should exist when done
4. **Constraints** - what must not break
5. **Context** - only what changes what the agent does
6. **Audience/Role** - which agent, what runtime
7. **Memory** - what files to read first
8. **Success Criteria** - AC1, AC2, AC3 (testable, specific)
9. **Examples** - reference points that clarify expected behaviour

---

## Installation

### OpenClaw

```json
{
  "skills": {
    "load": {
      "extraDirs": ["/path/to/your/skills"]
    }
  }
}
```

```bash
git clone https://github.com/LeoStehlik/brief-master.git /path/to/your/skills/brief-master
```

### Claude Code / Codex

Copy into `.agents/skills/brief-master/` or `.claude/skills/brief-master/`.

---

## Usage

```
Write me a brief for my dev agent to fix the translation timeout issue
```

```
Help me write a cron job prompt for overnight research
```

```
I need a code review brief for Sprint 5
```

---

## What's Inside

```
brief-master/
├── SKILL.md                           Core pipeline + quality rules
└── references/
    ├── 9-dimensions.md                Intent extraction framework
    └── brief-formats.md               Ready-to-use templates per agent type
```

---

## License

MIT - see [LICENSE](LICENSE)
