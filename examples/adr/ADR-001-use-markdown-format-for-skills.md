# ADR-001: Use Markdown Format for OpenCode Skills

**Status:** Accepted

**Date:** 2026-05-17

**Deciders:** Solution Architect Team

**Technical Story:** Phase 1 Implementation - Skill Development

## Context

We need to create a set of Solution Architect skills for OpenCode. OpenCode supports skills written in Markdown format with YAML frontmatter. We must decide on the format and structure for our skills to ensure consistency, maintainability, and ease of use.

Key considerations:
- Skills need to be editable by any text editor
- Must integrate seamlessly with OpenCode
- Should be version-controllable
- Need to provide clear guidance to the model
- Must support templates and structured output

## Decision

We will use **Markdown (.md) format** for all OpenCode skills with the following structure:

1. **YAML Frontmatter**: Contains `name:` and `description:` (no `model:` field — model selection is agent-level in OpenCode)
2. **Role Definition**: Clear description of skill purpose
3. **Commands Section**: Available workflows and sub-commands
4. **Templates Section**: Document formats and examples
5. **Best Practices**: Guidelines for usage
6. **Workflow Section**: Step-by-step processes

Example structure:
```markdown
---
name: skill-name
description: What this skill does and when to trigger it. Use when...
---

# Skill Name

You are an expert...

## Commands
/command-name - Description

## Templates
[Template content]

## Best Practices
[Guidelines]
```

## Consequences

### Positive
- **Simple and Accessible**: Plain text format editable in any editor
- **Version Control**: Easy to track changes in Git
- **Portable**: Can be easily shared and distributed
- **Flexible**: Supports rich formatting for templates and examples
- **OpenCode-Native**: Direct integration with OpenCode skill system
- **Documentable**: Self-documenting format with clear sections
- **No Build Step**: No compilation or processing required

### Negative
- **Limited Validation**: No compile-time checking of skill correctness
- **Manual Testing Required**: Must test skills manually with OpenCode
- **No Type Safety**: Can't enforce skill contract at development time
- **Potential Inconsistency**: Developers might deviate from standard structure

### Neutral
- Skills are loaded dynamically by OpenCode at runtime based on description matching
- Updates require replacing the skill file and restarting OpenCode
- Large skills can become lengthy documents

## Alternatives Considered

### Alternative 1: JSON/YAML Configuration Files
- **Pros:** 
  - Machine-readable format
  - Could add schema validation
  - Structured data easier to parse programmatically
- **Cons:** 
  - Less human-readable
  - Poor for long-form templates and instructions
  - Doesn't match OpenCode's native format
  - Would require custom tooling
- **Why rejected:** OpenCode uses Markdown natively; JSON/YAML doesn't support rich content well

### Alternative 2: Python/JavaScript Scripts
- **Pros:**
  - Full programming capabilities
  - Type checking and validation
  - Could include logic and helpers
- **Cons:**
  - OpenCode doesn't execute scripts
  - More complex development process
  - Requires runtime environment
  - Higher barrier to contribution
- **Why rejected:** OpenCode skills are prompt-based, not executable code

### Alternative 3: Custom DSL (Domain-Specific Language)
- **Pros:**
  - Tailored exactly to our needs
  - Could enforce structure
  - Potential for advanced features
- **Cons:**
  - Significant development effort
  - Learning curve for contributors
  - Maintenance burden
  - Tooling development required
- **Why rejected:** Overkill for current needs; Markdown is sufficient and widely understood

## References

- [OpenCode Documentation](https://opencode.ai/docs)
- [Markdown Specification](https://commonmark.org/)
- [YAML Frontmatter Convention](https://jekyllrb.com/docs/front-matter/)
- Project README.md
