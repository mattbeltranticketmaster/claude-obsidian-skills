# Claude Obsidian Skills

A collection of Claude Code skills for seamless Obsidian integration. Capture notes, track action items, and manage your knowledge base directly from Claude conversations.

## Features

### `/note` - Smart Note Capture
Save notes to your Obsidian vault with intelligent session tracking:
- **Session-based workflow**: Notes append to the active session automatically
- **Smart organization**: Content is structured with proper headers and formatting
- **YAML frontmatter**: Auto-generates metadata, tags, and timestamps
- **Multiple folders**: Organize notes into Dailies, Tasks, Planning, etc.

### `/whatamidoing` - Action Item Scanner
Scan your entire Obsidian vault for uncompleted action items:
- **Comprehensive scanning**: Finds all `- [ ]` checkboxes across your vault
- **Hierarchical display**: Groups by date → note → section
- **Context-aware**: Shows file paths and note titles for easy reference
- **Smart filtering**: Skips completed items, sorts by date

### `/actionitem` - Quick Capture
Instantly add action items without friction:
- **Zero friction**: Just type the item and go
- **Auto-appears in scanner**: Items show up when you run `/whatamidoing`
- **Quick Capture file**: All items saved to a central capture list
- **No interruptions**: No confirmation prompts, just fast capture

### `/saveforlater` - Context Preservation
Save the current conversation context to resume later:
- **Automatic extraction**: Analyzes conversation and extracts key points
- **Comprehensive capture**: Files, decisions, status, next steps
- **Resume-ready**: Everything you need to pick up where you left off
- **Structured format**: Organized sections for easy scanning

## Installation

### Prerequisites

- [Claude Code CLI](https://code.claude.com/) installed
- An Obsidian vault

### Quick Setup

1. **Clone this repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/claude-obsidian-skills.git
   cd claude-obsidian-skills
   ```

2. **Update vault path** in each skill file:
   - Edit `skills/note/SKILL.md` and update the vault location (line 11)
   - Edit `skills/whatamidoing/SKILL.md` and update the vault location (line 11)
   - Edit `skills/actionitem/SKILL.md` and update the vault location (line 11)
   - Edit `skills/saveforlater/SKILL.md` and update the vault location (line 6)

   Change from:
   ```
   `/Users/matthew.beltran/Documents/Obsidian Vault`
   ```

   To your vault path:
   ```
   `/Users/your-username/path/to/your/Obsidian Vault`
   ```

3. **Install the plugin**:
   ```bash
   claude plugin install ~/path/to/claude-obsidian-skills
   ```

4. **Verify installation**:
   ```bash
   claude
   # In Claude, type: /obsidian-notes:
   # You should see autocomplete suggestions for all skills
   ```

### Alternative: Local Development Mode

Test without installing:
```bash
claude --plugin-dir ~/path/to/claude-obsidian-skills
```

## Usage

### Taking Notes

**Start a new note session**:
```
/obsidian-notes:note new
```

**Add content to active session**:
```
/obsidian-notes:note Here are my thoughts on the API design...
```

**End the current session**:
```
/obsidian-notes:note end
```

### Managing Action Items

**Add a quick action item**:
```
/obsidian-notes:actionitem Review the pull request feedback
```

**See all uncompleted action items**:
```
/obsidian-notes:whatamidoing
```

### Saving Context

**Save conversation to resume later**:
```
/obsidian-notes:saveforlater
```

## Customization

### Adding Custom Folders

Edit `skills/note/SKILL.md` and add your folder to the "Available Folders" section:

```markdown
## Available Folders
- Dailies (for daily notes)
- Tasks (for task-related notes)
- YourNewFolder (for your custom notes)
```

### Changing Note Format

Modify the "Example Note Format" section in `skills/note/SKILL.md` to customize the YAML frontmatter and structure.

### Adjusting Action Item Format

Edit `skills/actionitem/SKILL.md` to change the capture file name or checkbox format.

## Plugin Structure

```
claude-obsidian-skills/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── skills/
│   ├── note/
│   │   └── SKILL.md         # Note capture skill
│   ├── actionitem/
│   │   └── SKILL.md         # Quick capture skill
│   ├── whatamidoing/
│   │   └── SKILL.md         # Action item scanner
│   └── saveforlater/
│       └── SKILL.md         # Context preservation
├── README.md                # This file
├── CONTRIBUTING.md          # Contribution guide
└── LICENSE                  # MIT License
```

## Troubleshooting

### Skills not showing up

1. Check plugin is installed:
   ```bash
   claude plugin list
   ```

2. Verify plugin structure:
   ```bash
   ls -la ~/path/to/claude-obsidian-skills/.claude-plugin/
   # Should see: plugin.json
   ```

3. Reinstall:
   ```bash
   claude plugin uninstall obsidian-notes
   claude plugin install ~/path/to/claude-obsidian-skills
   ```

### "File not found" errors

Make sure you updated the vault path in all skill files to match your actual Obsidian vault location.

### Action items not appearing

- Check that items are formatted as `- [ ]` (space between brackets)
- Verify the files are markdown (`.md`)
- Run `/whatamidoing` again after adding items with `/actionitem`

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Version

- **Version**: 1.0.0
- **Last Updated**: January 2026
- **Claude Code Compatibility**: v0.1.0+

## License

MIT License - See [LICENSE](LICENSE) for details.

## Support

- **Issues**: [GitHub Issues](https://github.com/YOUR_USERNAME/claude-obsidian-skills/issues)
- **Discussions**: [GitHub Discussions](https://github.com/YOUR_USERNAME/claude-obsidian-skills/discussions)

## Changelog

### v1.0.0 (January 2026)
- Initial release
- Note capture with session tracking
- Action item scanner
- Quick capture skill
- Context preservation skill
