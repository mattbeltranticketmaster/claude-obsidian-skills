# Claude Obsidian Skills - Meeting Intelligence System

Transform your Obsidian vault into a powerful meeting intelligence system with structured notes, smart action tracking, automated digests, and optional cloud sync.

**Version 2.1.0** - Latest update: Box vault support for cloud backup and cross-device access!

---

## 🎯 Features

### Meeting Intelligence
- **🎤 Parse meeting transcripts** - Convert messy notes into structured summaries
- **📊 Smart action tracking** - Extract action items with owners, due dates, and metadata
- **🏷️ Auto-tagging** - Automatic meeting type and project tagging
- **🔍 Advanced filtering** - Find exactly what you need with powerful filters
- **📈 Weekly digests** - Automated summaries with analytics and insights

### Note Management
- **✍️ Session-based notes** - Notes append to active sessions automatically
- **☁️ Box vault sync** - Optional cloud backup when ending sessions
- **⚡ Local-first workflow** - Fast, reliable note-taking
- **📂 Smart organization** - YAML frontmatter with metadata and tags

### Action Item Tracking
- **⚡ Quick capture** - Zero-friction action item creation
- **🎯 Rich metadata** - Owners, due dates, projects, priorities
- **🔴🟡🟢 Status indicators** - Overdue, due soon, stale detection
- **🔍 Comprehensive scanning** - Find all action items across your vault

---

## 📚 Available Skills

### `/meeting-notes` - Meeting Intelligence Parser
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

---

### `/note` - Save Structured Notes
Save notes to your Obsidian vault with session tracking and optional Box sync.

**Features:**
- Session-based note tracking - append to active notes
- Local-first workflow for speed and reliability
- Optional Box sync when ending sessions
- Smart folder organization

**Example:**
```
/note
[your notes]

/note
[additional updates]

/note end
# Prompts: "Would you like to copy this note to Box?"
```

---

### `/actionitem` - Quick Action Capture
Instantly add action items with rich metadata.

**Simple format:**
```
/actionitem Review the API documentation
```

**Enhanced format:**
```
/actionitem Review API docs @TianaSmith #2026-02-10 {{project:gco, priority:high}}
```

**Components:**
- `@owner` - Person responsible
- `#YYYY-MM-DD` - Due date
- `{{key:value}}` - Metadata tags

---

### `/whatamidoing` - Smart Action Scanner
Scan your vault for action items with powerful filtering.

**Examples:**
```
/whatamidoing                      # All items
/whatamidoing @me                  # Your items
/whatamidoing @me overdue          # Your overdue items
/whatamidoing project:gco          # Project-specific items
/whatamidoing this-week            # Due this week
```

**Features:**
- 🔴 Overdue items
- 🟡 Due within 3 days
- 🟢 Due later / no due date
- ⚠️ Stale items (>14 days old)

---

### `/digest` - Weekly Action Digest
Generate comprehensive action item summaries with analytics.

**Examples:**
```
/digest                   # Weekly digest
/digest @me              # Your personal digest
/digest project:gco      # Project status
/digest overdue          # Overdue items only
```

**What you get:**
- 📊 Summary statistics
- 🎯 Items grouped by status and owner
- 💡 Actionable insights
- 📈 Analytics by project and priority

---

### `/tutorial` - Interactive Tutorial
Learn the system with hands-on exercises.

```
/tutorial
```

Guides you through 6 levels:
1. First meeting note
2. Action item mastery
3. Filtering power
4. Weekly digests
5. Note sessions & Box sync
6. Workflow integration

---

## 🚀 Installation

### Prerequisites

- [Claude Code CLI](https://code.claude.com/) installed
- An Obsidian vault
- (Optional) Box account for cloud sync

### Quick Setup

1. **Add to Claude Code marketplace**:
   ```bash
   claude plugin marketplace add https://github.com/mattbeltranticketmaster/claude-obsidian-skills.git
   claude plugin install obsidian-notes
   ```

2. **Update vault paths** in skill files to match your setup:
   - Local vault: `/Users/your-username/Documents/Obsidian Vault`
   - Box vault (optional): `~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

3. **Try it out**:
   ```bash
   claude
   # Type: /meeting-notes or /note or /actionitem
   ```

---

## 📖 Usage

### Quick Start Workflow

**After a meeting:**
```
/meeting-notes
[paste your meeting notes or transcript]
```

**Quick action capture:**
```
/actionitem Follow up with John @me #2026-02-10 {{project:gco}}
```

**Check what you need to do:**
```
/whatamidoing @me
```

**Weekly review:**
```
/digest weekly
```

---

## ☁️ Box Vault Setup (Optional)

### Why Box Sync?

- **Cloud backup** - Protection against local drive issues
- **Cross-device access** - Work from anywhere
- **Team sharing** - Share meeting notes via Box
- **Selective sync** - Choose what to back up

### Setup Steps

1. **Ensure Box is installed and syncing**:
   ```bash
   ls ~/Library/CloudStorage/Box-Box
   ```

2. **Create Box vault structure**:
   ```bash
   mkdir -p ~/Library/CloudStorage/Box-Box/Notes/"Obsidian Vault"/{Dailies,Tasks,1v1s,Planning}
   ```

3. **Use the workflow**:
   - All notes save locally first (fast)
   - When you run `/note end`, choose to copy to Box
   - Box automatically syncs to cloud

---

## 🔧 Configuration

### Vault Locations

**Local Vault (Primary):**
`/Users/matthew.beltran/Documents/Obsidian Vault`

**Box Vault (Optional):**
`~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

### Available Folders
- **Dailies** - Daily notes and meeting notes
- **1v1s** - One-on-one meeting notes
- **Planning** - Planning sessions
- **Tasks** - Task-focused notes
- **Org Planning** - Organizational planning
- **AIMS** - AIMS-related work
- **Installment** - Installment/payment work
- **Interviews** - Interview notes

---

## 📚 Documentation

- **[README.md](plugins/obsidian-notes/README.md)** - Full documentation
- **[QUICK_START.md](plugins/obsidian-notes/QUICK_START.md)** - 5-minute quickstart
- **[WALKTHROUGH.md](plugins/obsidian-notes/WALKTHROUGH.md)** - Comprehensive guide
- **[Tutorial](/tutorial)** - Interactive hands-on tutorial

---

## 💡 Pro Tips

### 1. Use Consistent Naming
- ✅ `@TianaSmith` everywhere
- ❌ Don't mix `@Tiana`, `@TianaS`, `@tsmith`

### 2. Set Realistic Due Dates
Use due dates sparingly for truly time-sensitive items.

### 3. Review Regularly
- **Daily**: Check `@me overdue`
- **Weekly**: Run `/digest weekly`
- **Monthly**: Clean up stale items

### 4. Sync Important Notes to Box
Use `/note end` to copy important meeting notes to Box for:
- Cloud backup
- Cross-device access
- Team sharing

---

## 📈 What's Next

### Roadmap for 2.2
- [ ] Integration with calendar for automatic meeting detection
- [ ] Slack digest notifications
- [ ] Completion velocity tracking
- [ ] Team dashboards

### Roadmap for 3.0
- [ ] Natural language date parsing ("next Friday" → `#2026-02-07`)
- [ ] Recurring task templates
- [ ] Meeting agenda generation
- [ ] Integration with Jira/Linear

---

## 🐛 Troubleshooting

**Action items not showing up:**
- Ensure checkbox format is `- [ ]` (space inside brackets)
- Check file is in vault directory
- Verify `.md` extension

**Filters not working:**
- Check spelling of filter keywords
- Ensure date format is `YYYY-MM-DD`

**Box sync not working:**
- Verify Box is installed and syncing
- Check Box folder exists
- Ensure sufficient disk space

---

## 📝 Changelog

### v2.1.0 (February 2026)
- **NEW**: Box vault support for cloud backup and sync
- **ENHANCED**: `/note` now offers optional Box sync on session end
- **ADDED**: Local-first workflow with on-demand cloud backup
- **ADDED**: Dual-vault architecture

### v2.0.0 (February 2026)
- **NEW**: `/meeting-notes` skill for meeting transcript parsing
- **NEW**: `/digest` skill for action item summaries and analytics
- **ENHANCED**: `/actionitem` with owner, due date, and metadata
- **ENHANCED**: `/whatamidoing` with filtering and stale detection
- **ADDED**: Status indicators (🔴 🟡 🟢 ⚠️)

### v1.0.0 (January 2026)
- Initial release
- Note capture with session tracking
- Action item scanner
- Quick capture skill

---

## 👤 Author

**Matthew Beltran**
matt.beltran@ticketmaster.com

---

## 📄 License

Private - Internal Use Only

---

**Ready to transform your meeting notes into actionable intelligence? Start with `/meeting-notes` or `/tutorial` today!** 🚀
