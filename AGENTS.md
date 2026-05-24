# AGENTS.md

Authoritative instruction source is `CLAUDE.md` — read it before working on skills or docs.

## Repo layout

```
residual-architect/          ← git root (git@github.com:pmelander/residual-architect.git)
├── opencode.json            ← OpenCode config: skills path, slash commands, instructions
├── skills/<name>/SKILL.md  ← 14 OpenCode/Claude Code skills (dual-compatible)
├── skills/stressor/compliance-packs/
├── templates/               ← Markdown document templates
├── helpers/read_spreadsheet.py
├── docs/adr/                ← 7 ADRs documenting toolkit design decisions
├── docs/journey/            ← runtime-generated journey state files (never delete)
└── requirements.txt         ← openpyxl only; needed for the excel skill
```

No build system, no test runner, no linter, no CI. "Testing" a skill means installing it and exercising it in OpenCode or Claude Code.

## OpenCode install / setup

```bash
# Option A — open this repo directly in OpenCode
# opencode.json configures skills automatically; no copy needed.
# Only required for the excel skill:
pip install -r requirements.txt

# Option B — install skills globally (available in any project)
# Linux / macOS
cp -R skills/* ~/.config/opencode/skills/

# Windows PowerShell
Copy-Item -Recurse -Path "skills\*" -Destination "$env:APPDATA\..\Local\opencode\skills\"

# Option C — OpenCode also auto-loads from the Claude Code path
cp -R skills/* ~/.claude/skills/
```

After any config change, restart OpenCode — it reads config only at startup.

## Slash commands (defined in opencode.json)

These commands are available when the project is open in OpenCode:

| Command | Purpose |
|---------|---------|
| `/journey` | Start, resume, or review an architectural journey |
| `/discover` | Map paths, actors, and intentions in an existing system |
| `/stressor` | Run stressor analysis or apply a compliance pack |
| `/adr` | Create an Architecture Decision Record |
| `/design-review` | Run a systematic pre-production design review |
| `/solution-doc` | Generate HLD, LLD, runbook, or deployment guide |
| `/tech-stack` | Evaluate and recommend a technology stack |
| `/cloud` | Design cloud architecture or generate IaC |
| `/capacity` | Estimate capacity or design a scaling strategy |

The remaining skills (`arch-learning`, `capability-assessor`, `patterns`, `evolve`, `excel`) are loaded automatically when their descriptions match the task — invoke them with natural language.

## Skill frontmatter (OpenCode format)

```yaml
---
name: skill-name          # required; lowercase hyphen-separated; matches folder name
description: ...          # required; cover what AND when; front-load trigger keywords
---
```

Do not include `model:` in skill frontmatter — model selection is an OpenCode agent-level concern, not a skill-level one.

## Adding a new skill — checklist

Skills live at `skills/<name>/SKILL.md`. A new skill MUST:

1. Use OpenCode frontmatter: `name:` and `description:` (no `model:` field)
2. Description must state both what the skill does AND when to trigger it (start with trigger keywords or "Use when...")
3. Follow the 9-part body structure: Role Definition → Capability Being Built → Residuality Goal → Core Concept → Commands → Templates/Reference → Workflow → Reflection Prompts
4. Have an ADR in `docs/adr/` for any significant design decision (including decisions *not* to build something)
5. Update all four docs: `README.md`, `QUICKREF.md`, `GETTING_STARTED.md`, `CLAUDE.md`
6. If it warrants a slash command, add an entry to `opencode.json` under `"command"`

Skills must build transferable thinking, not tool dependency.

## Adding a compliance pack

Create `skills/stressor/compliance-packs/<framework>.md`. Each stressor must be a concrete harm scenario (not a control statement). Include the regulation reference, explain the real harm, and list common residuals. See `gdpr.md` for the expected shape.

## Hard constraints (backed by ADRs)

- **No Risk Assessor skill** (ADR-006): stressor analysis is the superset of risk assessment; traditional probability × impact registers conflict with Residuality Theory.
- **No standalone Compliance Checker skill** (ADR-007): compliance is injected as stressor packs into the stressor skill, not a separate checklist skill.

## Vocabulary — use these terms consistently

`aspirations`, `actors`, `intentions`, `paths`, `stressors`, `residuals`, `walks`

Using different synonyms in skills or docs creates confusion. These are defined terms in Residuality Theory.

## Journey state persistence — CRITICAL

When journey workflows are active, you MUST read and write these files in `docs/journey/`:

| File | When to update |
|------|---------------|
| `journey-state.md` | After EVERY journey command and after each nested skill execution |
| `stressor-iteration-history.md` | After every stressor analysis or journey iteration |
| `decisions-log.md` | When significant decisions are made |
| `assumptions-register.md` | When assumptions are identified or validated |

**Before any journey command:** read `docs/journey/journey-state.md`.  
**After any journey command:** update `docs/journey/journey-state.md`.

`templates/journey-state-template.md` provides the expected file structure.

## Git conventions

Branch: `main`  
Commit format: Conventional Commits — `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`

```bash
git checkout -b feature/skill-name
git commit -m "feat: add skill-name skill"
git push origin feature/skill-name
```
