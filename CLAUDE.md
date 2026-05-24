# CLAUDE.md

This file provides guidance to AI agents (OpenCode, Claude Code) when working with code in this repository.

## Project Overview

This is the **Residual Architecture Skill Set** — a comprehensive collection of OpenCode skills built on **Residuality Theory**, designed to build antifragile systems thinking and Solution Architect capabilities that compound over time.

## Architecture

### Project Structure

```
.
├── skills/                             # OpenCode/Claude Code layout: skills/<name>/SKILL.md
│   ├── adr/
│   │   └── SKILL.md                    # /adr
│   ├── solution-doc/
│   │   └── SKILL.md                    # /solution-doc
│   ├── tech-stack/
│   │   └── SKILL.md                    # /tech-stack
│   ├── design-review/
│   │   └── SKILL.md                    # /design-review
│   ├── stressor/
│   │   ├── SKILL.md                    # /stressor
│   │   └── compliance-packs/           # Regulatory stressor packs
│   │       ├── README.md
│   │       └── gdpr.md
│   ├── excel/
│   │   └── SKILL.md                    # /excel
│   ├── arch-learning/
│   │   └── SKILL.md                    # /arch-learning
│   ├── capability-assessor/
│   │   └── SKILL.md                    # /capability-assessor
│   ├── patterns/
│   │   └── SKILL.md                    # /patterns
│   ├── evolve/
│   │   └── SKILL.md                    # /evolve
│   ├── cloud/
│   │   └── SKILL.md                    # /cloud
│   ├── capacity/
│   │   └── SKILL.md                    # /capacity
│   ├── discover/
│   │   └── SKILL.md                    # /discover
│   └── journey/
│       └── SKILL.md                    # /journey
├── helpers/
│   └── read_spreadsheet.py             # Python helper for Excel reading
├── templates/                          # Document templates
│   ├── journey-state-template.md
│   ├── adr-template.md
│   ├── hld-template.md
│   ├── tech-comparison-template.md
│   ├── stressor-analysis-template.md
│   ├── capability-assessment-template.md
│   ├── pattern-template.md
│   ├── anti-pattern-template.md
│   └── fitness-function-template.md
├── examples/                           # Example outputs
├── requirements.txt                    # Python dependencies (openpyxl)
└── docs/
    ├── journey/                        # Journey state tracking (REQUIRED)
    │   ├── journey-state.md            # Current position, iteration log, artifacts
    │   ├── stressor-iteration-history.md   # Detailed stressor iteration log
    │   ├── decisions-log.md            # Lightweight decision log
    │   ├── assumptions-register.md     # Assumptions and validation status
    │   └── cadence-schedule.md         # Ongoing rhythm and triggers
    ├── adr/                            # ADRs documenting toolkit decisions
    │   ├── ADR-001-incorporate-residuality-theory.md
    │   ├── ADR-002-redesign-phase-2-for-capability-building.md
    │   ├── ADR-003-add-stressor-analysis-skill.md
    │   ├── ADR-004-add-excel-reading-utility.md
    │   ├── ADR-005-add-architecture-learning-analyzer.md
    │   ├── ADR-006-exclude-risk-assessor-skill.md
    │   └── ADR-007-compliance-via-stressor-packs.md
    └── ...                             # Generated documentation location
```

### Skill Development Pattern

Each skill follows this structure:
1. **Frontmatter** — YAML with `name` (required, matches folder name) and `description` (what it does AND when to trigger it)
2. **Role Definition** — clear statement of the skill's purpose
3. **Capability Being Built** — what thinking the skill transfers to the architect
4. **Residuality Goal** — what success looks like when the capability is internalised
5. **Core Concept** — the key idea and compound effect
6. **Commands** — slash commands with capability focus for each
7. **Templates/Reference** — frameworks, patterns, and output formats
8. **Workflow** — step-by-step process
9. **Reflection Prompts** — questions that build the capability

### Key Design Principle

Skills are **capability transfer tools**, not dependency-creating tools. Every skill should build thinking that architects carry forward independently. The measure of success is how rarely the skill needs to be invoked because the thinking has been internalised.

## Development Commands

### Testing Skills

```bash
# View skill content
cat skills/adr/SKILL.md

# Symlink for development (changes reflected immediately)
ln -s "$(pwd)/skills/adr" ~/.config/opencode/skills/adr

# Copy all for stable global use
cp -R skills/* ~/.config/opencode/skills/
```

### Adding New Skills

1. Create skill file at `skills/<name>/SKILL.md`
2. Use OpenCode frontmatter: `name: <folder-name>` and `description:` (do not include `model:`)
3. Description must state what the skill does AND when to trigger it — front-load keywords
4. Follow the Skill Development Pattern above
5. Document any significant design decisions as an ADR in `docs/adr/`
6. Update `README.md`, `QUICKREF.md`, `GETTING_STARTED.md`, and `CLAUDE.md`
7. If the skill warrants a slash command, add an entry to `opencode.json` under `"command"`

### Adding Compliance Packs

1. Create `skills/stressor/compliance-packs/<framework>.md`
2. Follow the pack structure defined in `skills/stressor/SKILL.md`
3. Each stressor must be a concrete scenario (not a control statement)
4. Include regulation reference and explanation of the real harm
5. List common residuals that emerge from the analysis

### Git Workflow

```bash
git checkout -b feature/new-skill-name
git commit -m "feat: add skill-name skill"
git push origin feature/new-skill-name
```

## Skill Usage

### Journey & Discovery (start here)

```bash
/journey start           # Begin any engagement — assess terrain, map the route
/journey where           # Mid-project: where am I, what comes next?
/journey iterate         # Iterate stressor loop or proceed?
/journey review          # Journey health check
/journey cadence         # Establish an ongoing rhythm

/discover paths                  # Map paths through an existing system
/discover actor <name>           # Investigate what an actor actually does
/discover intentions             # Trace how an intention propagates
/discover gaps                   # Identify and prioritise confidence gaps
/discover organisation           # Map organisational resistance as stressors
/discover confidence             # Assess readiness to proceed to stressor analysis
```

### Individual Capabilities

```bash
/adr create <title>              # Architecture Decision Records
/solution-doc hld                # Solution Documentation
/tech-stack recommend            # Technology Stack Advisor
/design-review complete          # Design Review
/stressor walk [path-name]       # Walk a path, evaluating each actor in sequence
/stressor analyze                # Stressor Analysis — build impact matrix
/stressor compliance <pack>      # Inject compliance stressor pack
```

### Organisational Capabilities

```bash
/arch-learning analyze           # Architecture Learning Analyzer
/capability-assessor assess      # Team Capability Assessor
/patterns extract                # Pattern Extractor
/evolve assess                   # Evolutionary Architecture Coach
```

### Specialised Tools

```bash
/cloud design <architecture>     # Cloud Architect
/cloud iac <provider>
/cloud review
/cloud cost
/cloud migrate <to-cloud>
/cloud dr

/capacity estimate               # Capacity Planner
/capacity scale <strategy>
/capacity bottleneck
/capacity load-test
/capacity forecast
/capacity right-size

/excel read <file> [sheet]       # Excel/CSV Reader
```

## Journey Memory Management

**CRITICAL REQUIREMENT:** Journey progress MUST be persisted to file at every significant step.

### Journey State Files

When executing `/journey` commands, you MUST maintain these files in `docs/journey/`:

1. **`journey-state.md`** — current position, aspiration, terrain type, iteration log, artifacts, gaps
   - Update after EVERY `/journey` command
   - Update after executing skills within the journey (discover, stressor, adr, etc.)
   - This is the single source of truth for journey progress

2. **`stressor-iteration-history.md`** — detailed log of each stressor iteration with impact matrices
   - Update after every `/stressor analyze` and `/journey iterate`

3. **`decisions-log.md`** — lightweight log of decision points (supplement to formal ADRs)
   - Update whenever a significant decision is made

4. **`assumptions-register.md`** — assumptions being carried forward with validation status
   - Update when assumptions are identified or validated

### When to Update

**ALWAYS update journey state when:**
- Starting a journey (`/journey start`)
- Checking position (`/journey where`)
- Making iteration decisions (`/journey iterate`)
- Reviewing journey health (`/journey review`)
- Establishing cadence (`/journey cadence`)
- Completing discovery commands
- Completing stressor analysis iterations
- Creating ADRs
- Generating solution documentation
- Completing design reviews

**Before executing a journey command:** Read `docs/journey/journey-state.md` to understand context.

**After executing a journey command:** Update `docs/journey/journey-state.md` with outcomes.

### Rationale

Built-in AI session memory is insufficient for long-running architectural journeys that may:
- Span weeks or months
- Resume after breaks
- Involve multiple architects
- Require audit trails
- Need iteration history for learning

File-based persistence ensures journey continuity, enables handoffs, and creates an audit trail of architectural thinking.

---

## Key Principles

### Residuality Theory Foundation

1. **Design for unknown unknowns** — not just known risks
2. **Antifragility over robustness** — systems that benefit from stress
3. **Residuals over mitigations** — architectural improvements that protect against classes of stressors
4. **Compliance as byproduct** — regulatory requirements addressed structurally, not procedurally
5. **Risk assessment replaced** — stressor analysis covers risk and more

### For Skill Development

1. **Capability first** — every command should build a thinking skill, not just produce output
2. **Clear residuality goal** — state what success looks like when the skill is no longer needed
3. **Reflection prompts** — include questions that deepen the thinking
4. **Consistent philosophy** — new skills must align with Residuality Theory; if a skill would train architects to think in checklists or registers, reconsider the approach

## Installation

```bash
# Option A — open this repo in OpenCode (skills load automatically via opencode.json)
pip install -r requirements.txt   # only needed for /excel

# Option B — install skills globally for OpenCode
cp -R skills/* ~/.config/opencode/skills/

# Option C — Claude Code / OpenCode auto-load path
cp -R skills/* ~/.claude/skills/
pip install -r requirements.txt

# Development (symlinks — changes reflected immediately)
ln -s "$(pwd)/skills/adr" ~/.config/opencode/skills/adr   # repeat per skill
```

## Skills

| Skill | Command | Category |
|-------|---------|----------|
| Architect's Journey | `/journey` | Orchestration |
| Environment Discovery | `/discover` | Discovery |
| Architecture Decision Records | `/adr` | Individual |
| Solution Documentation | `/solution-doc` | Individual |
| Technology Stack Advisor | `/tech-stack` | Individual |
| Design Review | `/design-review` | Individual |
| Stressor Analysis | `/stressor` | Individual |
| Architecture Learning Analyzer | `/arch-learning` | Organisational |
| Team Capability Assessor | `/capability-assessor` | Organisational |
| Pattern Extractor | `/patterns` | Organisational |
| Evolutionary Coach | `/evolve` | Organisational |
| Cloud Architect | `/cloud` | Specialised |
| Capacity Planner | `/capacity` | Specialised |
| Excel Reader | `/excel` | Utility |

## Contributing

When adding new skills:
1. Follow existing skill patterns — especially the Capability Being Built and Residuality Goal sections
2. Create an ADR in `docs/adr/` for any significant design decision (including decisions *not* to build something)
3. Update all documentation files: README.md, QUICKREF.md, GETTING_STARTED.md, CLAUDE.md
4. Test thoroughly before committing
