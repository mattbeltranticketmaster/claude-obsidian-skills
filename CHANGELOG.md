# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.0] - 2026-02-04

### Added
- Box vault support for cloud backup and sync
- Optional Box sync when ending note sessions with `/note end`
- Dual-vault architecture with identical folder structures
- Local-first workflow with on-demand cloud backup
- Tutorial Level 5 for note sessions & Box sync

### Changed
- `/note` skill now prompts for Box sync on session end
- Documentation updated with Box vault setup instructions
- Version bump in plugin.json to 2.1.0

### Documentation
- Added Box vault section to READMEs
- Updated WALKTHROUGH with Technique 6 for cloud backup
- Generic folder examples instead of personal folders
- Generic usernames in examples for privacy

## [2.0.0] - 2026-02-03

### Added
- `/meeting-notes` skill for meeting transcript parsing
- `/digest` skill for action item summaries and analytics
- `/tutorial` skill with 6 interactive hands-on levels
- Enhanced `/actionitem` with owner, due date, and metadata support
- Enhanced `/whatamidoing` with filtering and stale detection
- Status indicators: 🔴 overdue, 🟡 due soon, 🟢 future, ⚠️ stale
- Smart tagging and auto-categorization for meetings
- Comprehensive analytics and insights in digests
- Weekly, daily, and filtered digest options

### Changed
- `/actionitem` now supports rich metadata format: `@owner #YYYY-MM-DD {{key:value}}`
- `/whatamidoing` supports multiple filter combinations
- Complete documentation overhaul with QUICK_START, README, and WALKTHROUGH

### Features
- Meeting intelligence parsing from Confluence, Teams, or raw text
- Automatic extraction of decisions, discussions, and action items
- Auto-assignment of owners and due dates from context
- Project-based and owner-based filtering
- Stale item detection (>14 days old)
- Analytics by project, priority, and owner

## [1.0.0] - 2026-01-30

### Added
- Initial release of Claude Obsidian Skills
- `/note` skill for smart note capture with session tracking
- `/actionitem` skill for quick action item capture
- `/whatamidoing` skill to scan vault for uncompleted action items
- `/saveforlater` skill to preserve conversation context
- Comprehensive README with installation and usage instructions
- Contributing guidelines
- MIT License

### Features
- Session-based note workflow (automatically append to active note)
- YAML frontmatter generation with metadata and tags
- Hierarchical action item display grouped by date and note
- Context preservation for resuming conversations
- Support for multiple Obsidian folders

[2.1.0]: https://github.com/mattbeltranticketmaster/claude-obsidian-skills/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/mattbeltranticketmaster/claude-obsidian-skills/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/mattbeltranticketmaster/claude-obsidian-skills/releases/tag/v1.0.0
