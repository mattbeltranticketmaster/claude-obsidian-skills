# Contributing to Claude Obsidian Skills

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing.

## How to Contribute

### Reporting Bugs

If you find a bug, please open an issue with:
- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Your Claude Code version (`claude --version`)
- Your Obsidian version

### Suggesting Features

Feature suggestions are welcome! Please open an issue with:
- Clear description of the feature
- Use case and benefits
- Example of how it would work
- Any related skills or features

### Submitting Changes

1. **Fork the repository**
2. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Test thoroughly** (see Testing section below)
5. **Commit with clear messages**:
   ```bash
   git commit -m "Add feature: description of what you added"
   ```
6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Open a Pull Request**

## Development Setup

### Prerequisites

- Claude Code CLI installed
- An Obsidian vault for testing
- Git

### Local Testing

1. **Clone your fork**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/claude-obsidian-skills.git
   cd claude-obsidian-skills
   ```

2. **Update vault paths** in skill files to your test vault

3. **Test in development mode**:
   ```bash
   claude --plugin-dir ~/path/to/claude-obsidian-skills
   ```

4. **Try each skill**:
   - `/note` - Test note creation, session tracking, and Box sync
   - `/actionitem` - Test quick capture with metadata
   - `/whatamidoing` - Test scanning with filters
   - `/meeting-notes` - Test meeting transcript parsing
   - `/digest` - Test digest generation with analytics
   - `/tutorial` - Test interactive tutorial flow

### Testing Checklist

When making changes, test:

- [ ] Skill loads without errors
- [ ] Skill description is clear
- [ ] Instructions are followed correctly
- [ ] Error handling works (missing folders, invalid paths, etc.)
- [ ] Edge cases are handled (empty notes, special characters, etc.)
- [ ] Works with different vault structures
- [ ] YAML frontmatter is valid
- [ ] File paths are absolute
- [ ] Created folders have proper permissions

## Skill Development Guidelines

### Skill Structure

Each skill should have:

```markdown
---
name: skill-name
description: Brief one-line description
---

# Skill Title

Brief overview of what the skill does.

## Instructions

Clear, numbered steps for Claude to follow.

## Important Notes
- Key rules and constraints
- Edge cases to handle
```

### Best Practices

1. **Be specific**: Give Claude explicit instructions, not vague guidance
2. **Use absolute paths**: Always specify full file paths
3. **Handle errors**: Include error handling instructions
4. **Be frictionless**: Minimize user prompts for simple operations
5. **Test edge cases**: Empty files, special characters, missing folders
6. **Clear descriptions**: Users should understand what the skill does at a glance

### Writing Good Instructions

**Good**:
```markdown
1. Use Bash to check if the file exists:
   ```bash
   cat ~/.claude/session.txt 2>/dev/null || echo "NO_SESSION"
   ```
2. If the output is "NO_SESSION", proceed to create a new file.
```

**Bad**:
```markdown
1. Check if a session exists
2. If not, create one
```

### Obsidian-Specific Considerations

- Use YAML frontmatter for metadata
- Follow markdown best practices
- Respect user's folder structure
- Handle special characters in filenames
- Create folders with `mkdir -p` to avoid errors
- Always use `.md` extension
- Preserve existing content when editing

## Code Style

### Markdown

- Use ATX-style headers (`#`)
- Use hyphens for unordered lists (`-`)
- Use backticks for inline code
- Use fenced code blocks with language tags

### Instructions

- Number steps sequentially
- Use bold for emphasis (`**important**`)
- Use inline code for file paths and commands
- Include examples where helpful

### File Naming

- Skill folders: lowercase with hyphens (`action-item`)
- Skill files: `SKILL.md` (all caps)
- Documentation: `README.md`, `CONTRIBUTING.md`, etc.

## Versioning

We follow [Semantic Versioning](https://semver.org/):
- MAJOR: Breaking changes
- MINOR: New features (backward compatible)
- PATCH: Bug fixes

When releasing a new version, update:
- `plugins/obsidian-notes/.claude-plugin/plugin.json` - version field
- `README.md` - Version section at top
- `plugins/obsidian-notes/README.md` - Version section and changelog
- `CHANGELOG.md` - Add new version entry with all changes
- Create a git tag: `git tag v2.1.0 && git push origin v2.1.0`

## Pull Request Guidelines

### PR Title Format

- `feat: Add new skill for X`
- `fix: Resolve issue with Y`
- `docs: Update README with Z`
- `refactor: Improve W skill performance`

### PR Description

Include:
- **What**: What does this PR do?
- **Why**: Why is this change needed?
- **How**: How was it implemented?
- **Testing**: How was it tested?
- **Screenshots**: If applicable

### Review Process

1. Maintainer reviews code and tests locally
2. Feedback provided or PR approved
3. Address feedback if needed
4. Merge when approved

## Community Guidelines

- Be respectful and constructive
- Help others learn and grow
- Share knowledge and best practices
- Celebrate contributions of all sizes

## Questions?

- Open an issue for questions
- Join discussions in GitHub Discussions
- Tag maintainers if urgent

## Recognition

All contributors will be recognized in:
- GitHub contributors list
- Release notes for their contributions

Thank you for contributing!
