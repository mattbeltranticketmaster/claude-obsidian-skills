# Obsidian Notes - Meeting Intelligence System

Transform your Obsidian vault into a powerful meeting intelligence system with structured notes, smart action tracking, automated digests, and optional cloud sync.

## Version 2.1.0

Latest update: Box vault support for cloud backup and cross-device access!

---

## 🎯 What's New in 2.1

- **☁️ Box vault support** - Optional cloud backup and sync
- **⚡ Local-first workflow** - Fast, reliable note-taking
- **🔄 On-demand sync** - Choose what to back up when ending sessions
- **📂 Dual-vault architecture** - Identical folder structure in local and cloud

## 🎯 What's New in 2.0

- **🎤 Meeting transcript parsing** - Convert messy meeting notes into structured summaries
- **📊 Smart action tracking** - Track action items with owners, due dates, and metadata
- **🔍 Advanced filtering** - Filter action items by owner, project, or due date
- **📈 Weekly digests** - Automated summaries with analytics and insights
- **⚠️ Stale detection** - Identify items that need attention
- **🏷️ Auto-tagging** - Automatic meeting type and project tagging

---

## 📚 Available Skills

### 1. `/meeting-notes` - Meeting Intelligence Parser

Parse meeting transcripts from any source and generate structured summaries.

**What it does:**
- Extracts decisions, discussions, and action items automatically
- Auto-assigns owners and due dates from context
- Smart tagging by meeting type and project
- Supports Confluence, Teams, or raw text input

**Example:**
```
/meeting-notes
[paste your messy meeting notes]
```

**Output:**
```markdown
---
created: 2026-02-03
tags: [meeting, weekly-sync, gco, aunz]
attendees: [JohnSmith, JaneSmith]
---

# AU/NZ GCO Weekly Sync - 2026-02-03

## Decisions
- Approved Exchange/Upgrade solution for Q4

## Action Items
- [ ] Complete sign-off @JohnSmith #2026-02-10 {{project:gco, priority:high}}
- [ ] Update docs @JaneSmith #2026-02-05 {{project:gco}}
```

---

### 2. `/actionitem` - Quick Action Capture

Quickly add action items with rich metadata.

**Simple format:**
```
/actionitem Review the API documentation
```

**Enhanced format:**
```
/actionitem Review API docs @JohnSmith #2026-02-10 {{project:gco, priority:high}}
```

**Components:**
- `@owner` - Person responsible
- `#YYYY-MM-DD` - Due date
- `{{key:value}}` - Metadata tags (project, priority, etc.)

All components are optional and backward compatible.

---

### 3. `/whatamidoing` - Smart Action Scanner

Scan your vault for action items with powerful filtering.

**Basic usage:**
```
/whatamidoing
```

**Filter by owner:**
```
/whatamidoing @JohnSmith
/whatamidoing @me
```

**Filter by project:**
```
/whatamidoing project:gco
```

**Filter by due date:**
```
/whatamidoing overdue
/whatamidoing this-week
```

**Combine filters:**
```
/whatamidoing @me overdue project:gco
```

**Features:**
- 🔴 Overdue items
- 🟡 Due within 3 days
- 🟢 Due later / no due date
- ⚠️ Stale items (>14 days old)

---

### 4. `/digest` - Weekly Action Digest

Generate comprehensive action item summaries with analytics.

**Weekly digest:**
```
/digest
/digest weekly
```

**Daily digest:**
```
/digest daily
```

**Filtered digests:**
```
/digest @me
/digest project:gco
/digest overdue
```

**What you get:**
- 📊 Summary statistics
- 🎯 Items grouped by status and owner
- 💡 Actionable insights
- ⚠️ Attention-needed items
- 📈 Analytics by project and priority

---

### 5. `/note` - Save Structured Notes

Save notes to your Obsidian vault with session tracking and optional cloud sync.

**Start a new note:**
```
/note
[your notes]
```

**Append to active note:**
```
/note
[additional content]
```

**End session with optional Box sync:**
```
/note end
```

**Features:**
- Session-based note tracking
- Auto-organization and formatting
- Smart folder suggestions
- YAML frontmatter with metadata
- **Local-first workflow** - Fast, reliable note-taking
- **Optional Box sync** - Copy to cloud on session end

---

## 🚀 Quick Start

### Basic Workflow

1. **After a meeting:**
   ```
   /meeting-notes
   [paste your meeting notes or transcript]
   ```

2. **Quick action capture:**
   ```
   /actionitem Follow up with John @me #2026-02-10 {{project:gco}}
   ```

3. **Check what you need to do:**
   ```
   /whatamidoing @me
   ```

4. **Weekly review:**
   ```
   /digest weekly
   ```

### Advanced Workflow

**For project managers:**
```
# Monday morning - check team status
/digest project:gco

# During the week - track your items
/whatamidoing @me

# Friday - weekly review with team
/digest weekly
```

**For individual contributors:**
```
# Daily standup prep
/whatamidoing @me today

# Check overdue items
/whatamidoing @me overdue

# Weekly planning
/digest @me this-week
```

---

## 📋 Action Item Format Reference

### Standard Format
```markdown
- [ ] Task description @Owner #YYYY-MM-DD {{key:value, key:value}}
```

### Components

**Owner (`@username`):**
- `@JohnSmith` - Specific person
- `@me` - Yourself
- Optional - can be omitted

**Due Date (`#YYYY-MM-DD`):**
- `#2026-02-10` - Specific date
- Format must be: `#YYYY-MM-DD`
- Optional - can be omitted

**Metadata (`{{key:value}}`):**
- `{{project:gco}}` - Project tag
- `{{priority:high}}` - Priority level
- `{{project:gco, priority:high}}` - Multiple tags
- Optional - can be omitted

### Examples

```markdown
- [ ] Simple task with no metadata
- [ ] Task with owner @JohnSmith
- [ ] Task with due date #2026-02-10
- [ ] Task with project tag {{project:gco}}
- [ ] Complete task @JohnSmith #2026-02-10 {{project:gco, priority:high}}
```

---

## 🏷️ Recommended Tags

### Meeting Types
- `weekly-sync` - Regular team syncs
- `1v1` - One-on-one meetings
- `standup` - Daily standups
- `planning` - Planning sessions
- `retro` - Retrospectives
- `design-review` - Design reviews
- `all-hands` - Company/team all-hands

### Project Tags
- `project:gco` - Global Checkout
- `project:payments` - Payments work
- `project:fraud` - Fraud prevention
- `project:aunz` - Australia/New Zealand

### Priority Levels
- `priority:high` - Urgent/critical
- `priority:medium` - Important but not urgent
- `priority:low` - Nice to have

---

## 💡 Pro Tips

### 1. Use Consistent Naming
Use consistent names for owners across all notes:
- ✅ `@JohnSmith`
- ❌ `@John`, `@jsmith`, `@JohnS`

### 2. Set Realistic Due Dates
Use due dates sparingly for truly time-sensitive items:
- High-priority deliverables
- External dependencies
- Hard deadlines

### 3. Review Regularly
Schedule regular reviews:
- **Daily**: Check `@me overdue`
- **Weekly**: Run `/digest weekly`
- **Monthly**: Clean up stale items

### 4. Tag Projects Consistently
Use the same project tags across meetings and action items to enable powerful filtering.

### 5. Leverage Digests
Use digests for different audiences:
- **Personal**: `/digest @me`
- **Project**: `/digest project:gco`
- **Team**: `/digest weekly` (all items)

---

## 🔧 Configuration

### Vault Locations

**Local Vault (Primary):**
`/Users/your-username/Documents/Obsidian Vault`

All notes are saved here first for fast, reliable access. Update the vault path in the skill configuration to match your actual location.

**Box Vault (Optional Backup/Sync):**
`~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

When ending a note session with `/note end`, you'll be prompted to optionally copy the note to Box for cloud backup and sync.

### Available Folders

The plugin supports organizing notes into folders. Default examples:
- **Dailies** - Daily notes and meeting notes
- **1v1s** - One-on-one meeting notes
- **Planning** - Planning sessions
- **Tasks** - Task-focused notes

You can add custom folders by editing the skill configuration files to match your workflow.

### Session File
Active note sessions are tracked in:
`~/.claude/active-note-session.txt`

---

## 🐛 Troubleshooting

**Action items not showing up in `/whatamidoing`:**
- Ensure checkbox format is correct: `- [ ]` (space inside brackets)
- Check that file is in the vault directory
- Verify file has `.md` extension

**Filters not working:**
- Check spelling of filter keywords
- Ensure date format is `YYYY-MM-DD`
- Try without filters first to verify items exist

**Meeting notes not parsing correctly:**
- Provide more structured input
- Manually specify attendees and date if not clear from context
- Try breaking very long transcripts into sections

---

## 📝 Changelog

### 2.1.0 (2026-02-04)
- **NEW**: Box vault support for cloud backup and sync
- **ENHANCED**: `/note` now offers optional Box sync on session end
- **ADDED**: Local-first workflow with on-demand cloud backup
- **ADDED**: Dual-vault architecture for reliability + cloud access

### 2.0.0 (2026-02-03)
- **NEW**: `/meeting-notes` skill for meeting transcript parsing
- **NEW**: `/digest` skill for action item summaries and analytics
- **ENHANCED**: `/actionitem` now supports owner, due date, and metadata
- **ENHANCED**: `/whatamidoing` now supports filtering and stale detection
- **ENHANCED**: Smart tagging and auto-categorization
- **ADDED**: Status indicators (🔴 🟡 🟢 ⚠️)
- **ADDED**: Comprehensive analytics and insights

### 1.0.0 (2026-01-28)
- Initial release
- `/note` skill for saving notes
- `/actionitem` skill for quick capture
- `/whatamidoing` skill for scanning action items

---

## 👤 Author

**Matthew Beltran**
matt.beltran@ticketmaster.com

---

## 📄 License

Private - Internal Use Only

---

**Ready to transform your meeting notes into actionable intelligence? Start with `/meeting-notes` today!** 🚀
