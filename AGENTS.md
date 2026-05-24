# AGENTS.md

Authoritative instruction source is `CLAUDE.md` — read it before working on skills or docs.

## Repo layout

```
open-architect/              ← git root (git@github.com:pmelander/open-architect.git)
├── opencode.json            ← OpenCode config: 14 custom slash commands
├── commands/<name>.md       ← 14 command templates (one per slash command)
├── commands/compliance-packs/ ← Regulatory stressor packs (gdpr.md etc.)
├── templates/               ← Markdown document templates
├── helpers/read_spreadsheet.py
├── docs/adr/                ← 7 ADRs documenting toolkit design decisions
├── docs/journey/            ← runtime-generated journey state files (never delete)
└── requirements.txt         ← openpyxl only; needed for the /excel command
```

No build system, no test runner, no linter, no CI. "Testing" a command means opening the project in OpenCode and exercising the slash command.

## OpenCode install / setup

```bash
# Option A — open this repo directly in OpenCode (recommended)
# opencode.json configures all 14 commands automatically; no copy needed.
# Only required for the /excel command:
pip install -r requirements.txt

# Option B — install commands globally (available in any project)
# Linux / macOS
cp commands/* ~/.config/opencode/commands/

# Windows PowerShell
Copy-Item -Path "commands\*" -Destination "$env:USERPROFILE\.config\opencode\commands\"
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
| `/arch-learning` | Analyze ADRs and architectural decisions for patterns |
| `/capability-assessor` | Assess team architectural capability maturity |
| `/patterns` | Extract and catalog architectural patterns |
| `/evolve` | Coach teams in evolutionary architecture |
| `/excel` | Read Excel/CSV files for architecture analysis |

## Command file frontmatter (OpenCode format)

Each `commands/<name>.md` file begins with YAML frontmatter. Recognized fields for command files:

```yaml
---
name: command-name        # informational; the filename determines the command name
description: ...          # shown in the TUI command picker; cover what AND when
---
```

Optional fields supported by OpenCode command markdown files: `agent`, `model`, `subtask`. Do not include `model:` unless you want to pin a specific model for that command.

## Adding a new command — checklist

Commands live at `commands/<name>.md` and must be registered in `opencode.json`. A new command MUST:

1. Create `commands/<name>.md` with YAML frontmatter (`name:` and `description:`) and a detailed prompt body
2. Description must state both what the command does AND when to trigger it (start with trigger keywords or "Use when...")
3. Follow the 9-part body structure: Role Definition → Capability Being Built → Residuality Goal → Core Concept → Commands → Templates/Reference → Workflow → Reflection Prompts
4. Register it in `opencode.json` under `"command"` with `"description"` and `"template": "{file:commands/<name>.md}"`
5. Have an ADR in `docs/adr/` for any significant design decision (including decisions *not* to build something)
6. Update all four docs: `README.md`, `QUICKREF.md`, `GETTING_STARTED.md`, `CLAUDE.md`

Commands must build transferable thinking, not tool dependency.

## Adding a compliance pack

Create `commands/compliance-packs/<framework>.md`. Each stressor must be a concrete harm scenario (not a control statement). Include the regulation reference, explain the real harm, and list common residuals. See `gdpr.md` for the expected shape.

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
git checkout -b feature/command-name
git commit -m "feat: add command-name command"
git push origin feature/command-name
```
