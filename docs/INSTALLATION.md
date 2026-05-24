# Installation Guide

This guide explains how to install the Residual Architecture Skill Set for OpenCode.

---

## Option A: Open this repo in OpenCode (Recommended)

The simplest approach. When you open this repository in OpenCode, `opencode.json` configures all 14 skills and 9 slash commands automatically — no copying required.

```bash
git clone <repository-url> residual-architect
cd residual-architect

# Only required for the /excel skill:
pip install -r requirements.txt
```

Open the `residual-architect` directory in OpenCode. Type `/` to confirm skills are loaded.

---

## Option B: Install globally for OpenCode

Copy skills to the OpenCode global skills directory so they are available in any project.

**Linux/macOS:**
```bash
mkdir -p ~/.config/opencode/skills
cp -R skills/* ~/.config/opencode/skills/
pip install -r requirements.txt
```

**Windows (PowerShell):**
```powershell
$dest = "$env:APPDATA\..\Local\opencode\skills"
New-Item -ItemType Directory -Force -Path $dest
Copy-Item -Recurse -Path "skills\*" -Destination $dest
pip install -r requirements.txt
```

---

## Option C: Development (Symlinks)

Symlinks let edits to the repo reflect immediately without re-copying.

**Linux/macOS:**
```bash
mkdir -p ~/.config/opencode/skills
ln -s "$(pwd)/skills/adr"                ~/.config/opencode/skills/adr
ln -s "$(pwd)/skills/solution-doc"        ~/.config/opencode/skills/solution-doc
ln -s "$(pwd)/skills/tech-stack"          ~/.config/opencode/skills/tech-stack
ln -s "$(pwd)/skills/design-review"       ~/.config/opencode/skills/design-review
ln -s "$(pwd)/skills/stressor"            ~/.config/opencode/skills/stressor
ln -s "$(pwd)/skills/excel"               ~/.config/opencode/skills/excel
ln -s "$(pwd)/skills/arch-learning"       ~/.config/opencode/skills/arch-learning
ln -s "$(pwd)/skills/capability-assessor" ~/.config/opencode/skills/capability-assessor
ln -s "$(pwd)/skills/patterns"            ~/.config/opencode/skills/patterns
ln -s "$(pwd)/skills/evolve"              ~/.config/opencode/skills/evolve
ln -s "$(pwd)/skills/cloud"               ~/.config/opencode/skills/cloud
ln -s "$(pwd)/skills/capacity"            ~/.config/opencode/skills/capacity
ln -s "$(pwd)/skills/discover"            ~/.config/opencode/skills/discover
ln -s "$(pwd)/skills/journey"             ~/.config/opencode/skills/journey
```

---

## Option D: Auto-load via Claude Code path

OpenCode also auto-loads skills from `~/.claude/skills/` — so the same install works for both tools.

```bash
mkdir -p ~/.claude/skills
cp -R skills/* ~/.claude/skills/
```

---

## Verification

After **Option A** (repo opened in OpenCode): type `/` — you should see the 9 registered slash commands (`/journey`, `/stressor`, `/discover`, etc.).

After **Options B/C/D** (global install): open OpenCode in any project. Type `/` or ask an architectural question — skills load automatically when their description matches the task.

---

## Restart required

OpenCode reads config and skills only at startup. After any install or config change, **quit and restart OpenCode**.

---

## Python dependency (excel skill only)

The `/excel` skill uses `helpers/read_spreadsheet.py` which requires Python and openpyxl:

```bash
pip install -r requirements.txt
```

If `/excel` commands fail, verify Python is in your PATH and openpyxl is installed.

---

## Updating

```bash
cd residual-architect
git pull origin main

# If using Option B (direct copy):
cp -R skills/* ~/.config/opencode/skills/
```

Symlink installations (Option C) update automatically on `git pull`.

---

## Uninstall

**Linux/macOS:**
```bash
rm -rf ~/.config/opencode/skills/adr
rm -rf ~/.config/opencode/skills/solution-doc
rm -rf ~/.config/opencode/skills/tech-stack
rm -rf ~/.config/opencode/skills/design-review
rm -rf ~/.config/opencode/skills/stressor
rm -rf ~/.config/opencode/skills/excel
rm -rf ~/.config/opencode/skills/arch-learning
rm -rf ~/.config/opencode/skills/capability-assessor
rm -rf ~/.config/opencode/skills/patterns
rm -rf ~/.config/opencode/skills/evolve
rm -rf ~/.config/opencode/skills/cloud
rm -rf ~/.config/opencode/skills/capacity
rm -rf ~/.config/opencode/skills/discover
rm -rf ~/.config/opencode/skills/journey
```

**Windows (PowerShell):**
```powershell
$base = "$env:APPDATA\..\Local\opencode\skills"
"adr","solution-doc","tech-stack","design-review","stressor","excel",
"arch-learning","capability-assessor","patterns","evolve","cloud",
"capacity","discover","journey" | ForEach-Object {
    Remove-Item -Recurse -Force "$base\$_"
}
```

---

## Troubleshooting

### Skills don't appear in OpenCode

1. Confirm the skills directory exists and contains `<name>/SKILL.md` entries.
2. Check that each `SKILL.md` has valid YAML frontmatter with `name:` and `description:`.
3. **Restart OpenCode** — skills are loaded at startup only.

### Skill not triggered automatically

OpenCode surfaces skills based on how well the task description matches the skill's `description:` field. If a skill isn't being loaded, try phrasing your request to include the skill's trigger keywords (e.g. "run stressor analysis", "create an ADR", "discover paths in this system").

### /excel skill fails

Verify Python is available and openpyxl is installed:
```bash
python --version
python -c "import openpyxl; print('ok')"
```

If `import openpyxl` fails: `pip install openpyxl`

---

## Next Steps

- [Getting Started Guide](../GETTING_STARTED.md) — first journey in 5 minutes
- [Quick Reference](../QUICKREF.md) — all commands at a glance
- [Usage Guide](USAGE.md) — detailed examples for every skill
