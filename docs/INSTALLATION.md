# Installation Guide

This guide explains how to install the Residual Architecture Skill Set for OpenCode.

---

## Option A: Open this repo in OpenCode (Recommended)

The simplest approach. When you open this repository in OpenCode, `opencode.json` configures all 14 slash commands automatically — no copying required.

```bash
git clone <repository-url> residual-architect
cd residual-architect

# Only required for the /excel command:
pip install -r requirements.txt
```

Open the `residual-architect` directory in OpenCode. Type `/` to confirm commands are loaded.

---

## Option B: Install globally for OpenCode

Copy command files to the OpenCode global commands directory so they are available in any project.

**Linux/macOS:**
```bash
mkdir -p ~/.config/opencode/commands
cp commands/* ~/.config/opencode/commands/
pip install -r requirements.txt
```

**Windows (PowerShell):**
```powershell
$dest = "$env:USERPROFILE\.config\opencode\commands"
New-Item -ItemType Directory -Force -Path $dest
Copy-Item -Path "commands\*" -Destination $dest
pip install -r requirements.txt
```

---

## Verification

After **Option A** (repo opened in OpenCode): type `/` — you should see all 14 registered slash commands (`/journey`, `/stressor`, `/discover`, `/adr`, `/design-review`, `/solution-doc`, `/tech-stack`, `/cloud`, `/capacity`, `/arch-learning`, `/capability-assessor`, `/patterns`, `/evolve`, `/excel`).

After **Option B** (global install): open OpenCode in any project. Type `/` to see the commands in the picker.

---

## Restart required

OpenCode reads config and commands only at startup. After any install or config change, **quit and restart OpenCode**.

---

## Python dependency (excel command only)

The `/excel` command uses `helpers/read_spreadsheet.py` which requires Python and openpyxl:

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
cp commands/* ~/.config/opencode/commands/
```

---

## Uninstall

**Linux/macOS:**
```bash
for cmd in adr solution-doc tech-stack design-review stressor excel \
           arch-learning capability-assessor patterns evolve cloud \
           capacity discover journey; do
    rm -f ~/.config/opencode/commands/${cmd}.md
done
```

**Windows (PowerShell):**
```powershell
$base = "$env:USERPROFILE\.config\opencode\commands"
"adr","solution-doc","tech-stack","design-review","stressor","excel",
"arch-learning","capability-assessor","patterns","evolve","cloud",
"capacity","discover","journey" | ForEach-Object {
    Remove-Item -Force "$base\$_.md" -ErrorAction SilentlyContinue
}
```

---

## Troubleshooting

### Commands don't appear in OpenCode

1. Confirm `opencode.json` is in the project root (Option A) or command files are in `~/.config/opencode/commands/` (Option B).
2. Check that each `commands/<name>.md` file has valid YAML frontmatter with `description:`.
3. **Restart OpenCode** — commands are loaded at startup only.

### /excel command fails

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
- [Usage Guide](USAGE.md) — detailed examples for every command
