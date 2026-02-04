# Complete Walkthrough - Meeting Intelligence System

A hands-on, step-by-step guide to mastering your new meeting intelligence system. Follow along and build muscle memory!

---

## 🎯 What You'll Learn

By the end of this walkthrough, you'll be able to:
- ✅ Transform messy meeting notes into structured summaries
- ✅ Track action items with rich metadata
- ✅ Filter and find exactly what you need
- ✅ Generate insightful weekly digests
- ✅ Build an effective productivity workflow

**Time to complete:** 20-30 minutes

---

## 📝 Chapter 1: Your First Meeting Note

### Scenario
You just finished the GCO AU/NZ weekly sync. You took rough notes during the meeting. Let's transform them into something useful.

### Your Raw Notes
```
GCO weekly - feb 3
tiana karin matt

talked about q4 rollout. exchange solution approved.
scaling to 100% now

matt - talk to quin about timeline, by feb 10
karin - update confluence this week
tiana - market signoff by feb 15

still figuring out booking protect timing
```

### Step 1: Invoke the Parser

Type this command:
```
/meeting-notes
```

Then paste your raw notes above when prompted.

### Step 2: Watch the Magic

Claude will:
1. **Extract metadata**: Meeting title, date, attendees
2. **Identify decisions**: "Exchange solution approved"
3. **Parse action items**: Extract owners and due dates
4. **Organize discussions**: Structure the narrative
5. **Auto-tag**: Add meeting type and project tags

### Step 3: Review the Output

You'll see something like this:

```markdown
---
created: 2026-02-03
tags: [meeting, weekly-sync, gco, aunz]
meeting_date: 2026-02-03
attendees: [TianaSmith, KarinSparring, MatthewBeltran]
meeting_type: weekly-sync
---

# GCO AU/NZ Weekly Sync - 2026-02-03

## Context
Weekly sync for AU/NZ GCO rollout team to discuss Q4 scaling progress.

## Decisions
- **Exchange Solution Approved**: Approved Exchange and Upgrade solution for Q4 delivery. This unblocks scaling to 100%.

## Action Items
- [ ] Talk to Quin about timeline @MatthewBeltran #2026-02-10 {{project:gco}}
- [ ] Update Confluence @KarinSparring #2026-02-07 {{project:gco}}
- [ ] Market signoff @TianaSmith #2026-02-15 {{project:gco}}

## Follow-ups / Open Questions
- Still need to finalize Booking Protect timing
```

### Step 4: Confirm and Save

Claude will ask you to confirm:
- Meeting title ✓
- Folder location (Dailies) ✓
- Tags (weekly-sync, gco, aunz) ✓
- Attendees ✓

Just confirm and it's saved!

### 🎓 What You Learned
- Meeting parser handles messy input
- Owners and dates extracted automatically
- Smart tagging by meeting type and project
- Output is searchable and structured

---

## 🎯 Chapter 2: Quick Action Capture

### Scenario
During the day, you think of 3 things you need to do. Let's capture them quickly.

### Step 1: Simple Capture (No Metadata)

Type:
```
/actionitem Review the security audit findings
```

**Output:**
```
✓ Added: Review the security audit findings
```

**Result in Quick Capture.md:**
```markdown
- [ ] Review the security audit findings
```

### Step 2: Add an Owner

Type:
```
/actionitem Schedule team retro @me
```

**Output:**
```
✓ Added: Schedule team retro @me
```

Now you know this is YOUR task.

### Step 3: Add a Due Date

Type:
```
/actionitem Submit expense report @me #2026-02-05
```

**Output:**
```
✓ Added: Submit expense report @me (due 2026-02-05)
```

### Step 4: Full Metadata

Type:
```
/actionitem Review PR #247 @me #2026-02-04 {{project:gco, priority:high}}
```

**Output:**
```
✓ Added: Review PR #247 @me (due 2026-02-04, project:gco)
```

### Step 5: For Someone Else

Type:
```
/actionitem Deploy staging environment @DevOpsTeam #2026-02-06 {{project:gco}}
```

**Output:**
```
✓ Added: Deploy staging environment @DevOpsTeam (due 2026-02-06, project:gco)
```

### 🎓 What You Learned
- Simple format: just the task
- Add components incrementally
- `@owner` for who's responsible
- `#YYYY-MM-DD` for due dates
- `{{key:value}}` for metadata
- All components are optional

---

## 🔍 Chapter 3: Finding Your Action Items

### Scenario
It's Monday morning. You want to see what you need to do today, what's overdue, and what's coming up.

### Step 1: See Everything

Type:
```
/whatamidoing
```

**Output:**
```markdown
# Action Items (8 total)

## 🔴 Overdue (1 item)

### 2026-01-29 - Quick Capture
- [ ] Submit expense report @me #2026-02-01

## 🟡 Due This Week (3 items)

### 2026-02-03 - GCO Weekly Sync
- [ ] Review PR #247 @me #2026-02-04 {{project:gco, priority:high}}
- [ ] Submit expense report @me #2026-02-05

### 2026-02-03 - Quick Capture
- [ ] Talk to Quin @MatthewBeltran #2026-02-10 {{project:gco}}

## 🟢 Future / No Due Date (4 items)

### 2026-02-03 - Quick Capture
- [ ] Review security audit findings
- [ ] Schedule team retro @me
- [ ] Deploy staging environment @DevOpsTeam #2026-02-06 {{project:gco}}
- [ ] Update Confluence @KarinSparring #2026-02-07 {{project:gco}}

---
Summary: 8 total items | 1 overdue | 3 due this week | 4 future/no date
```

### Step 2: Filter by Owner (Just YOUR Items)

Type:
```
/whatamidoing @me
```

**Output:**
```markdown
# Action Items (4 total)

## 🔴 Overdue (1 item)
- [ ] Submit expense report @me #2026-02-01

## 🟡 Due This Week (2 items)
- [ ] Review PR #247 @me #2026-02-04 {{project:gco, priority:high}}
- [ ] Submit expense report @me #2026-02-05

## 🟢 Future / No Due Date (1 item)
- [ ] Schedule team retro @me

---
Summary: 4 items | 1 overdue | 2 due this week | 1 no date
Filters: @me
```

### Step 3: Filter by Project

Type:
```
/whatamidoing project:gco
```

**Output:**
All GCO-related action items from across your notes.

### Step 4: Show Only Overdue

Type:
```
/whatamidoing overdue
```

**Output:**
Just the red items that need attention NOW.

### Step 5: Combine Filters

Type:
```
/whatamidoing @me overdue
```

**Output:**
Only YOUR overdue items.

### 🎓 What You Learned
- Status indicators: 🔴 🟡 🟢
- Filter by `@owner`
- Filter by `project:name`
- Filter by status: `overdue`, `this-week`, `today`
- Combine multiple filters
- Get context (which note each item came from)

---

## 📊 Chapter 4: Your First Digest

### Scenario
It's Friday afternoon. You want to review the week, see what you accomplished, and plan for next week.

### Step 1: Weekly Personal Digest

Type:
```
/digest @me
```

**Output:**
```markdown
# Action Item Digest - Week of 2026-02-03

**Summary:** 4 total items | 1 overdue | 2 due this week | 1 no date

---

## 🔴 Overdue (1 item)

### @me
- [ ] Submit expense report #2026-02-01
  📍 From: 2026-01-29 - Quick Capture
  ⏰ 2 days overdue

---

## 🟡 Due This Week (2 items)

### @me
- [ ] Review PR #247 #2026-02-04 {{project:gco, priority:high}}
  📍 From: 2026-02-03 - GCO Weekly Sync
  ⏰ Due in 1 day

- [ ] Submit expense report #2026-02-05
  📍 From: 2026-02-03 - Quick Capture
  ⏰ Due in 2 days

---

## 📊 Analytics

### By Project
- {{project:gco}}: 1 item
- No project: 3 items

### By Priority
- High: 1 item
- No priority: 3 items

---

## 💡 Insights

- **Most urgent:** Review PR #247 (due tomorrow, high priority)
- **Overdue attention:** 1 item needs immediate action

---

## 🎯 Suggested Actions

1. Submit expense report ASAP (2 days overdue)
2. Review PR #247 tomorrow (high priority)

---

_Generated: 2026-02-03 4:30 PM_
_Filters: @me_
_Sources: 3 notes scanned, 4 action items found_
```

### Step 2: Team-Wide Weekly Digest

Type:
```
/digest weekly
```

**Output:**
Same format but includes EVERYONE'S items, grouped by owner.

### Step 3: Project Status Digest

Type:
```
/digest project:gco
```

**Output:**
All GCO project items with:
- Status breakdown
- Owner distribution
- Timeline analysis
- Blockers identified

### Step 4: Daily Standup Prep

Type:
```
/digest @me today
```

**Output:**
Just YOUR items due TODAY.

### 🎓 What You Learned
- Personal digest: `@me`
- Team digest: `weekly`
- Project digest: `project:name`
- Daily prep: `today`
- Get analytics and insights
- Identify patterns and blockers

---

## 🔄 Chapter 5: Building Your Workflow

### Daily Workflow

**Morning (5 minutes):**
```bash
/whatamidoing @me overdue    # What's overdue?
/whatamidoing @me today      # What's due today?
```

**During the day:**
```bash
/actionitem [task] @me #[date] {{project:name}}
```

**End of day (2 minutes):**
```bash
/whatamidoing @me            # What's still pending?
```

### Weekly Workflow

**Monday morning (10 minutes):**
```bash
/digest @me this-week        # Plan my week
/digest project:gco          # Check project status
```

**After each meeting:**
```bash
/meeting-notes               # Parse meeting notes
```

**Friday afternoon (15 minutes):**
```bash
/digest @me                  # Review my week
/whatamidoing stale          # Clean up old items
```

### Team Lead Workflow

**Before weekly sync:**
```bash
/digest weekly               # Team status overview
```

**During sync:**
Take notes normally

**After sync:**
```bash
/meeting-notes               # Parse and structure
```

**Share digest:**
Copy/paste digest output to Slack or email

---

## 🎯 Chapter 6: Real-World Examples

### Example 1: You're a PM Managing Multiple Projects

**Monday morning:**
```bash
/digest project:gco
/digest project:payments
/digest project:fraud
```

**After stakeholder meeting:**
```bash
/meeting-notes
[paste meeting notes from Confluence or Teams]
```

**Throughout the week:**
```bash
/actionitem Follow up with legal @me #2026-02-08 {{project:gco, priority:high}}
/actionitem Review mockups @Designer #2026-02-10 {{project:payments}}
```

**Friday review:**
```bash
/digest weekly
```

### Example 2: You're an Engineering Lead

**Daily standup prep:**
```bash
/whatamidoing @me today
```

**After code review:**
```bash
/actionitem Refactor auth service @TechLead #2026-02-12 {{project:security}}
```

**Weekly 1v1s:**
```bash
/meeting-notes
[paste 1v1 notes]
```

**End of sprint:**
```bash
/digest this-week
/whatamidoing stale          # Clean up board
```

### Example 3: You're an Individual Contributor

**Morning routine:**
```bash
/whatamidoing @me overdue
/whatamidoing @me today
```

**Quick captures:**
```bash
/actionitem Review Sarah's PR @me {{priority:medium}}
/actionitem Deploy to staging @me #2026-02-06 {{project:feature-x}}
```

**Weekly planning:**
```bash
/digest @me this-week
```

---

## 💡 Chapter 7: Pro Tips & Best Practices

### Tip 1: Consistent Naming

**Use same format for owners:**
- ✅ `@TianaSmith` everywhere
- ❌ Don't mix `@Tiana`, `@TianaS`, `@tsmith`

**Why?** Filtering breaks with inconsistent names.

### Tip 2: Date Format Discipline

**Always use YYYY-MM-DD:**
- ✅ `#2026-02-10`
- ❌ `#2/10/26`, `#Feb 10`, `#02-10-2026`

**Why?** Sorting and filtering require consistent format.

### Tip 3: Minimal Tagging

**Keep metadata simple:**
- ✅ `{{project:gco, priority:high}}`
- ❌ `{{project:gco, priority:high, status:todo, sprint:23, team:payments, type:bug}}`

**Why?** Over-tagging is hard to maintain and filter.

### Tip 4: Due Dates Are Special

**Only use for real deadlines:**
- ✅ External deliverables, hard commitments
- ❌ Everything (creates noise)

**Why?** Overdue list loses meaning if everything has dates.

### Tip 5: Regular Cleanup

**Weekly stale item review:**
```bash
/whatamidoing stale
```

**Actions:**
- Complete it
- Assign an owner
- Set a due date
- Delete if no longer relevant

**Why?** Prevents list bloat and decision fatigue.

### Tip 6: Meeting Type Consistency

**Use standard meeting types:**
- `weekly-sync` - Regular team syncs
- `1v1` - One-on-ones
- `planning` - Planning sessions
- `retro` - Retrospectives

**Why?** Makes searching and filtering easier.

### Tip 7: Project Tag Strategy

**Align with your org structure:**
- If your team uses "GCO", use `project:gco`
- If you work on "Payments Platform", use `project:payments`

**Why?** Natural mental model = easier adoption.

---

## 🚀 Chapter 8: Advanced Techniques

### Technique 1: Meeting Templates

**For recurring meetings:**

Save this as a snippet:
```markdown
GCO Weekly Sync - [DATE]

Attendees: Tiana, Karin, Matt

Progress:
-

Blockers:
-

Decisions:
-

Action items:
-
```

Use with `/meeting-notes` each week.

### Technique 2: Batch Processing

**Process multiple meetings at once:**

After a long day of meetings:
```bash
/meeting-notes
Meeting 1: [notes]

---

Meeting 2: [notes]

---

Meeting 3: [notes]
```

Claude will ask if you want separate notes or combined.

### Technique 3: Digest Comparison

**Track progress over time:**

Week 1:
```bash
/digest @me
```
(Copy output somewhere)

Week 2:
```bash
/digest @me
```
(Compare with Week 1 manually)

**Look for:**
- Item count trend (up/down?)
- Completion velocity
- Overdue pattern

### Technique 4: Context Linking

**In meeting notes, link to Jira/Confluence:**

```markdown
## Discussion
We reviewed [TMG-1393](https://jira.livenation.com/browse/TMG-1393)

See also: [Confluence Design Doc](https://confluence.company.com/page/123)
```

**Why?** One-click navigation to related resources.

### Technique 5: Priority Filtering

**See only high-priority items:**
```bash
/whatamidoing {{priority:high}}
```

**Combine with other filters:**
```bash
/whatamidoing @me {{priority:high}} overdue
```

### Technique 6: Cloud Backup with Box

**Local-first workflow with optional cloud sync:**

All notes are saved locally first for speed and reliability. When you're done with a note, you can optionally copy it to Box for cloud backup and sharing.

**Workflow:**
```bash
/note
[your meeting notes]
```
→ Saves locally to: `/Users/matthew.beltran/Documents/Obsidian Vault`

Add more content:
```bash
/note
[additional updates]
```
→ Appends to the same local note

End session:
```bash
/note end
```
→ Prompts: "Would you like to copy this note to Box?"
→ If yes, copies to: `~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

**When to use Box sync:**
- ✅ Important meeting notes for team sharing
- ✅ Notes you need to access from multiple devices
- ✅ Archive-worthy decisions and outcomes
- ✅ Compliance or record-keeping requirements

**When to keep local only:**
- ✅ Personal brainstorming or drafts
- ✅ Temporary notes or quick captures
- ✅ Work-in-progress notes not ready to share

**Benefits:**
- **Fast note-taking** - No waiting for cloud sync while working
- **Reliable** - Always saved locally even if Box is offline
- **Selective sync** - Only back up what matters
- **Identical structure** - Same folders in both locations

---

## 🎓 Graduation: You're Ready!

### What You've Mastered

✅ **Meeting Intelligence**
- Parse messy notes into structure
- Auto-extract actions with metadata
- Smart tagging

✅ **Action Tracking**
- Rich metadata (owner, date, project)
- Status awareness (overdue, due soon, stale)
- Advanced filtering

✅ **Digests & Analytics**
- Personal and team digests
- Project health monitoring
- Actionable insights

✅ **Workflow Integration**
- Daily routines
- Weekly reviews
- Team collaboration

### Your Workflows

- 📅 **Daily:** Check overdue, plan today
- 📊 **Weekly:** Review digest, clean up stale items
- 🎤 **After meetings:** Parse and structure
- ⚡ **Throughout day:** Quick capture actions

### Next Steps

1. **Practice:** Use it daily for a week
2. **Refine:** Adjust tags/filters to your workflow
3. **Share:** Introduce to your team
4. **Evolve:** Build new workflows as needs emerge

---

## 📚 Reference

### Quick Command Reference

```bash
# Action capture
/actionitem [task] @owner #YYYY-MM-DD {{key:value}}

# Meeting parsing
/meeting-notes

# Action scanning
/whatamidoing                    # All items
/whatamidoing @me                # Your items
/whatamidoing project:name       # Project items
/whatamidoing overdue            # Overdue only
/whatamidoing @me overdue        # Your overdue items

# Digests
/digest                          # Weekly digest
/digest @me                      # Your digest
/digest project:name             # Project digest
/digest today                    # Daily digest

# Notes
/note                            # Start new note or append to active
/note new                        # Force new note (ignore active session)
/note end                        # End session (offers Box sync)
```

### Metadata Format Reference

```markdown
- [ ] Task @Owner #YYYY-MM-DD {{key:value, key:value}}

Owner: @Username
Date: #2026-02-10
Metadata: {{project:name, priority:level}}
```

### Status Indicators

- 🔴 Overdue
- 🟡 Due within 3 days
- 🟢 Due later / no date
- ⚠️ Stale (>14 days old)

---

## 🎉 Congratulations!

You've completed the walkthrough and are now a Meeting Intelligence System power user!

**Keep this document** as a reference guide. Come back whenever you need a refresher.

**Now go build some incredible workflows!** 🚀
