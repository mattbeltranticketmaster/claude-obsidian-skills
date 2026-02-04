# Quick Start Guide - Meeting Intelligence System

Get productive with your new meeting intelligence system in 5 minutes!

## ⚡ Immediate Use Cases

### 1. Just Had a Meeting? Parse It!

```
/meeting-notes
```

Then paste your meeting notes (messy is fine):

```
GCO weekly sync, Feb 3, 2026

Tiana, Karin, Matt

Talked about the Exchange solution. We're going to move forward with it for Q4.
This will let us scale to 100%.

Matt needs to talk to Quin about timeline - aim for Feb 10.
Karin will update the Confluence docs this week.

Still figuring out Booking Protect timing.
```

Claude will transform this into a structured note with:
- ✅ Clear decisions section
- ✅ Auto-extracted action items with owners and due dates
- ✅ Smart tags (meeting-type, project, etc.)
- ✅ Proper formatting and organization

---

### 2. Quick Action Item?

```
/actionitem Review PR #247 @me #2026-02-05 {{project:gco}}
```

Done! It's captured and will show up in your action lists.

---

### 3. What Do I Need to Do Today?

```
/whatamidoing @me overdue
```

Shows all YOUR overdue items with clear status indicators:
- 🔴 Overdue
- 🟡 Due soon
- 🟢 Future

---

### 4. Weekly Team Review?

```
/digest project:gco
```

Get a complete digest with:
- All GCO project action items
- Grouped by status and owner
- Analytics and insights
- Suggested actions

---

## 🎯 Your First Week

### Day 1: Monday

**Morning standup:**
```
/whatamidoing @me today
```

**After team meeting:**
```
/meeting-notes
[paste meeting notes]
```

---

### Day 2-4: Tuesday - Thursday

**Daily check:**
```
/whatamidoing @me
```

**Quick captures throughout the day:**
```
/actionitem Follow up with design @me #2026-02-07 {{project:gco}}
/actionitem Review security docs @me {{priority:high}}
```

---

### Day 5: Friday

**Weekly review:**
```
/digest @me this-week
```

**Team status:**
```
/digest project:gco
```

**Clean up stale items:**
```
/whatamidoing stale
```

---

## 💪 Level Up: Advanced Usage

### Power User Filters

**My overdue items for GCO:**
```
/whatamidoing @me overdue project:gco
```

**Everything due this week:**
```
/whatamidoing this-week
```

**All high-priority items:**
```
/whatamidoing {{priority:high}}
```

---

### Meeting Intelligence Pro Tips

**1. Confluence Integration**

Have meeting notes in Confluence? Just provide the URL:
```
/meeting-notes https://confluence.livenation.com/display/ECOM/Meeting+Notes
```

Claude will fetch and parse it automatically!

**2. Teams Transcript**

After a Teams meeting, copy the transcript and:
```
/meeting-notes
[paste Teams transcript]
```

Works perfectly with Teams auto-transcription.

**3. Multiple Sources**

Had a meeting with notes from multiple people?
```
/meeting-notes
My notes: [your notes]

Also from Confluence: [Confluence URL]

Additional context: [more notes]
```

Claude will merge everything intelligently.

---

### Digest Intelligence

**Compare weeks:**
```
/digest weekly
```
Then next week, run it again. Claude remembers and can show trends!

**Project health check:**
```
/digest project:gco
```
See all GCO work, who's blocked, what's overdue.

**Personal productivity:**
```
/digest @me last-30-days
```
See your completion patterns over the past month.

---

## 📊 Real-World Examples

### Example 1: Product Manager

**Monday morning:**
```
/digest project:gco
```
*Output:*
- 3 overdue items (need follow-up)
- 8 due this week
- 2 stale items (>14 days)
- Insight: "@TianaSmith has 5 overdue items - schedule 1v1?"

**After 1v1 with Tiana:**
```
/meeting-notes
1v1 with Tiana - Feb 3

Discussed her workload. She's blocked on legal review for 2 items.
I'll follow up with legal team by Thursday.

She'll have the market sign-off done by next Monday instead of this week.

Action: Update roadmap to reflect new timeline.
```
*Output:* Structured 1v1 note with action items automatically assigned

---

### Example 2: Engineering Lead

**Daily standup prep:**
```
/whatamidoing @me today
```
*Output:*
- 🟡 Review PR #247 (due today)
- 🟡 Deploy to staging (due today)

**After standup:**
```
/actionitem Review Sarah's design doc @me #2026-02-04 {{priority:medium}}
/actionitem Set up pairing session with junior dev @me #2026-02-05
```

**End of week:**
```
/digest @me this-week
```
*Output:*
- Completed: 12 items ✅
- Still open: 3 items
- Net change: -9 items (great progress!)

---

### Example 3: Team Lead

**Before weekly team meeting:**
```
/digest weekly
```
*Output:* Full team status:
- 15 total open items
- 4 overdue (need to discuss)
- 6 stale items (need to close or assign)
- Analytics by owner and project

**During meeting:** Take notes normally, then after:
```
/meeting-notes
[paste your rough notes]
```

**Share digest with team:**
The digest output is already formatted - just copy/paste into Slack or email!

---

## 🚨 Common Pitfalls to Avoid

### ❌ DON'T: Over-tag everything
```
/actionitem Review docs {{priority:high, status:todo, type:review, sprint:23, team:gco}}
```
Keep it simple! Just project and priority if needed.

### ✅ DO: Use minimal effective tagging
```
/actionitem Review docs @me #2026-02-05 {{project:gco, priority:high}}
```

---

### ❌ DON'T: Set due dates for everything
Not everything needs a due date. Use them for real deadlines only.

### ✅ DO: Use due dates sparingly
```
/actionitem Research competitor features @TianaSmith {{project:gco}}
/actionitem Complete legal review @me #2026-02-10 {{project:gco, priority:high}}
```
First item: no deadline needed
Second item: hard deadline, needs due date

---

### ❌ DON'T: Use inconsistent owner names
```
@Tiana, @TianaS, @tsmith, @Tiana Smith
```
This breaks filtering!

### ✅ DO: Pick one format and stick to it
```
@TianaSmith (everywhere)
```

---

## 🎓 Pro Workflows

### Workflow 1: "Inbox Zero" for Action Items

**Daily:**
1. `whatamidoing @me overdue` - handle overdue first
2. `/whatamidoing @me today` - tackle today's items
3. `/actionitem` - capture new items as they come up

**Weekly:**
1. `/digest @me this-week` - review the week
2. `/whatamidoing stale` - clean up old items
3. `/whatamidoing @me` - prioritize for next week

---

### Workflow 2: "Team Health Check"

**For team leads running weekly syncs:**

**Before meeting:**
```
/digest project:gco weekly
```
Review team status, identify blockers

**During meeting:**
Take notes, discuss items from digest

**After meeting:**
```
/meeting-notes
[paste meeting notes]
```
Generate structured summary with new actions

**Share with team:**
Copy digest + meeting summary to Slack/email

---

### Workflow 3: "Project Pulse"

**For PMs tracking multiple projects:**

**Monday morning:**
```
/digest project:gco
/digest project:payments
/digest project:fraud
```
Get status of all projects

**Throughout week:**
Use `/actionitem` to capture project-specific tasks with tags

**Friday afternoon:**
```
/digest weekly
```
Full team view for status update email/meeting

---

## 🆘 Need Help?

**Action items not showing up?**
Check: `/whatamidoing` with no filters first

**Meeting parsing not working well?**
Provide more structure: attendees, date, clear sections

**Filters not working?**
Verify spelling and format of tags/dates

**Want to see examples?**
Check the README.md for comprehensive documentation

---

## 🚀 Ready to Master It?

You now have everything you need to:
- ✅ Parse meetings into structured notes
- ✅ Track action items with rich metadata
- ✅ Filter and find exactly what you need
- ✅ Generate insightful weekly digests
- ✅ Stay on top of your work

**Start simple, then level up!**

Begin with just `/meeting-notes` after your next meeting, and take it from there.

The system grows with you. 🎯
