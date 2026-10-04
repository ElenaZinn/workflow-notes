# Engineering Workflow Notes

> Process notes for engineering workflows: **bug fixing**, **code/language migration**, and **scheduled polling with multi-condition decisions**. Each one has steps, artifacts, a failure-mode checklist, and fill-in-the-blank templates.

[中文](README.md)

---

## The problems these solve

- **A bug you can't fix.** You can locate it but not correct it; the fix doesn't work; it comes back after being fixed; it's intermittent and won't reproduce.
- **Migration out of control.** A full rewrite blows up the schedule and loses the original contracts and behavior; piecemeal edits break everything around them.
- **Polling incidents.** Duplicate triggers causing duplicate charges; upstream data lagging; decision logic missing its default fallback.

What these have in common: **the happy path is easy to write — failures live in the exception paths and in skipped steps.**

## Shared principles

These notes follow the same rules:

1. **Locate the root cause before touching code.** Without evidence, any change is a guess.
2. **Every step produces an artifact.** Something the next person — or your future self — can pick up.
3. **Make rules executable.** Anything that must not happen goes into a CI gate or a checklist, not into memory.
4. **Design the failure path first.** Most production incidents live on a path nobody wrote down.
5. **Keep a record.** The "where I got stuck" line is the most valuable one.

## What's inside

| Workflow | Use it when | Key artifacts |
| --- | --- | --- |
| [bugfix-diagnosis-flow](bugfix-diagnosis-flow/SKILL.md) | A bug is hard to reproduce, you can locate it but not fix it, or a fix keeps coming back | time-sequence / call chain, change point, bug record |
| [language-migration-flow](language-migration-flow/SKILL.md) | Migrating code across languages (e.g. Kotlin/Java → Rust), or any incremental refactor | migration spec, CI gates and forbidden rules, phase plan, change log |
| [scheduled-polling-flow](scheduled-polling-flow/SKILL.md) | Scheduled polling or multi-condition decisions (price checks, inventory sync, recurring validation) | task table, check-valid rules, decision matrix, fallback map |

## Structure

```text
.
├── LICENSE
├── README.md
├── README.en.md
├── bugfix-diagnosis-flow/
│   ├── SKILL.md
│   └── references/bug-record-template.md
├── language-migration-flow/
│   ├── SKILL.md
│   └── references/migration-checklist.md
└── scheduled-polling-flow/
    └── SKILL.md
```

## How to use

- **As an agent skill.** Each folder is a `SKILL.md`-based skill with YAML frontmatter (`name` / `description`). Drop a folder into your agent's skills directory and it triggers on the matching scenario.
- **As a personal or team checklist.** Read it as a "what should happen next" checklist.
- **As templates.** `references/` holds fill-in-the-blank templates: migration spec, CI gates and forbidden rules, phase checklist, change log, and bug record.

## Overview

### bugfix-diagnosis-flow

1. Frame the issue and set priority
2. Collect evidence, locate the root cause
3. Draw the time sequence and call chain
4. Pinpoint the change point
5. Design the fix
6. If the fix doesn't work: a debugging order
7. Retrospective and record

### language-migration-flow

1. Inventory the current state
2. Write the migration spec
3. Lock the immovable contracts
4. Set up CI gates and forbidden rules
5. Split into phases
6. Log every change
7. Build the test baseline before restructuring
8. Phase acceptance and rework

### scheduled-polling-flow

1. Define the task table
2. Set trigger points and check-valid gates
3. Centralize scheduling and de-duplicate
4. Multi-condition decision matrix
5. Three hard constraints: idempotency, deadline, precision
6. Failure modes and fallbacks
7. Retrospective

## Roadmap

- [ ] Code review workflow
- [ ] Incident response workflow
- [ ] Release and rollback checklist

## License

[MIT](LICENSE)

## Feedback

Issues and suggestions are welcome.
