# Contributing to Residual Architecture Skill Set

Thank you for your interest in contributing! This toolkit is designed to evolve with the needs of Solution Architects using OpenCode.

## How to Contribute

### Types of Contributions

1. **New Commands** - Add new architecture commands
2. **Command Improvements** - Enhance existing commands
3. **Templates** - Add or improve document templates
4. **Examples** - Provide real-world examples
5. **Documentation** - Improve guides and docs
6. **Bug Fixes** - Fix issues in commands or docs

## Development Setup

### Prerequisites

- Git installed
- OpenCode installed and configured
- Text editor (VS Code, Vim, etc.)
- Basic understanding of Markdown

### Getting Started

```bash
# Fork and clone the repository
git clone <your-fork-url>
cd residual-architect

# Create a feature branch
git checkout -b feature/your-feature-name

# Open the project directory in OpenCode — all commands load automatically
# No install step needed for development (Option A)

# For global availability during development, copy command files:
cp commands/* ~/.config/opencode/commands/
```

## Command Development Guidelines

### Command Structure

Every command should follow this structure:

```markdown
---
name: command-name
description: What this command does and when to trigger it. Front-load trigger keywords.
---

# Command Name

You are an expert [role description]...

## Your Role
[Clear description of the command's purpose]

## Commands
[Available workflows and sub-commands]

## Templates
[Document templates and formats]

## Best Practices
[Guidelines for effective use]

## Workflow
[Step-by-step process]
```

### Command Best Practices

1. **Clear Commands**: Define explicit slash commands
2. **Ask Questions**: Gather context before generating
3. **Use Templates**: Provide consistent output formats
4. **Include Examples**: Show users what good looks like
5. **Be Thorough**: Cover edge cases and alternatives
6. **Consider Workflow**: Follow natural work patterns

### Testing Your Command

Before submitting:

1. **Test the command in OpenCode**
   ```
   /your-command-name [test with various inputs]
   ```

2. **Verify output quality**
   - Does it generate useful output?
   - Is the format consistent?
   - Are templates properly structured?

3. **Test edge cases**
   - Empty inputs
   - Complex scenarios
   - Error conditions

4. **Get feedback**
   - Use it yourself for real work
   - Ask colleagues to try it

## Contribution Process

### 1. Create an Issue

Before starting work, create an issue describing:
- What you want to add/change
- Why it's needed
- Proposed approach

### 2. Develop Your Contribution

**For New Commands:**

```bash
# Create the command file
touch commands/command-name.md
# Follow the command structure template above
# Include frontmatter (name + description), commands, templates, etc.
# Register in opencode.json under "command" with description and template path

# Add example output
mkdir examples/command-name
touch examples/command-name/example-output.md

# Update README.md, QUICKREF.md, GETTING_STARTED.md, and CLAUDE.md to list the new command
```

**For Improvements:**

- Clearly document what changed and why
- Maintain backward compatibility when possible
- Update related documentation

### 3. Document Your Changes

- Update `README.md` if adding new command
- Update `CLAUDE.md` with any architectural changes
- Add/update examples in `examples/`
- Update `docs/USAGE.md` with usage instructions

### 4. Create an ADR for Significant Changes

For major decisions, create an ADR:

```bash
# Use the ADR template
cp templates/adr-template.md docs/adr/ADR-XXX-your-decision.md

# Fill in the template
# Document context, decision, consequences, alternatives
```

### 5. Test Thoroughly

- Test the skill with OpenCode
- Verify all commands work
- Check output quality
- Test edge cases

### 6. Submit a Pull Request

```bash
# Commit your changes
git add .
git commit -m "feat(phase-X): add skill-name skill

Detailed description of what was added and why.

Closes #issue-number"

# Push to your fork
git push origin feature/your-feature-name

# Create PR on GitHub
```

## Commit Message Guidelines

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): subject

body

footer
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples:**

```bash
feat(phase-1): add api-designer skill

Add comprehensive API design skill for REST and GraphQL API design,
validation, and documentation generation.

Closes #42

---

fix(adr): correct ADR numbering logic

ADR numbers were not sequential when ADRs were deleted. Updated to
find the highest existing number and increment.

Fixes #38

---

docs(usage): add tech-stack advisor examples

Add detailed examples showing how to use tech-stack advisor for
common scenarios like technology comparison and migration planning.
```

## Code Review Process

1. **Automated Checks**: PR must pass basic checks
2. **Peer Review**: At least one maintainer review
3. **Testing**: Changes must be tested
4. **Documentation**: Updates must include docs

### Review Criteria

- ✅ Follows command structure guidelines
- ✅ Includes proper documentation
- ✅ Tested with OpenCode
- ✅ Examples provided (for new commands)
- ✅ Templates are well-formatted
- ✅ Commit messages follow convention

## Command Guidelines

When contributing a new command, consider where it fits:

- **Widely applicable** — useful to any architect on any engagement (e.g. stressor analysis, ADRs)
- **Deep analysis** — requires multiple steps or integrates with existing artefacts (e.g. capability assessment, pattern extraction)
- **Specialised** — domain-specific or scenario-specific (e.g. cloud architecture, compliance packs)

## Documentation Standards

### README Updates

When adding a command, update README.md:

```markdown
### Phase X: Category Name
- ✅ `command-name` - Brief description
```

### CLAUDE.md Updates

Document architectural decisions and patterns:

```markdown
## Skill Development Pattern

[Describe any new patterns or approaches]
```

### Usage Guide Updates

Add to `docs/USAGE.md`:

```markdown
## Skill Name

### Using the Skill

[Detailed usage instructions]

### Examples

[Real-world examples]

### Best Practices

[Guidelines for effective use]
```

## Template Guidelines

When creating templates:

1. **Use Standard Formats**: Follow industry standards
2. **Be Comprehensive**: Cover all necessary sections
3. **Include Comments**: Guide users on what to fill in
4. **Show Examples**: Provide example content
5. **Keep Consistent**: Match existing template style

## Example Guidelines

When adding examples:

1. **Use Realistic Scenarios**: Base on real-world situations
2. **Show Best Practices**: Demonstrate proper usage
3. **Be Complete**: Full examples, not fragments
4. **Add Context**: Explain why the example is good
5. **Vary Complexity**: Include simple and complex examples

## Getting Help

- 💬 **Questions**: Open an issue with the `question` label
- 🐛 **Bugs**: Open an issue with the `bug` label
- 💡 **Ideas**: Open an issue with the `enhancement` label
- 📖 **Documentation**: Check `docs/` directory

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in release notes
- Thanked in the community

## License

By contributing, you agree that your contributions will be licensed under the same license as the project (MIT).

## Questions?

Feel free to:
- Open an issue for questions
- Start a discussion
- Reach out to maintainers

Thank you for helping make this toolkit better for all Solution Architects!
