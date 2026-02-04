---
name: tutorial
description: Interactive hands-on tutorial for learning the Meeting Intelligence System
---

# Interactive Meeting Intelligence Tutorial

Guide users through hands-on exercises to learn the meeting intelligence system. This is a step-by-step, interactive tutorial that provides real-time feedback and guidance.

## Vault Locations

**Local Vault (Primary):** `/Users/matthew.beltran/Documents/Obsidian Vault`
**Box Vault (Optional):** `~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault`

All notes save locally first. Box sync is optional when ending sessions.

## Tutorial Structure

The tutorial has 6 levels:
1. **Level 1: First Meeting Note** - Parse a sample meeting
2. **Level 2: Action Item Mastery** - Learn rich metadata
3. **Level 3: Filtering Power** - Master /whatamidoing
4. **Level 4: Weekly Digest** - Generate insights
5. **Level 5: Note Sessions & Box Sync** - Learn note workflow and cloud backup
6. **Level 6: Workflow Integration** - Put it all together

## Instructions

### Tutorial State Management

**Create a tutorial tracking file:**
- Path: `~/.claude/meeting-intelligence-tutorial-state.json`
- Track: current level, completed exercises, user progress

**State format:**
```json
{
  "current_level": 1,
  "completed_exercises": [],
  "started_at": "2026-02-03T10:00:00Z",
  "last_session": "2026-02-03T10:30:00Z",
  "user_name": "matthew.beltran"
}
```

### Step 1: Check for Existing Tutorial State

1. **Use Bash to check if tutorial state exists**:
   ```bash
   cat ~/.claude/meeting-intelligence-tutorial-state.json 2>/dev/null || echo "NEW_USER"
   ```

2. **If NEW_USER**:
   - Welcome the user
   - Explain what they'll learn
   - Ask if they want to start Level 1
   - Create initial state file

3. **If RETURNING**:
   - Read their progress
   - Show completion status
   - Ask if they want to continue or restart

### Step 2: Level-Specific Content

## Level 1: Your First Meeting Note

**Learning objective:** Transform messy notes into structured summaries

**Exercise:**
```
I'm going to give you some messy meeting notes. Your job is to use /meeting-notes to structure them.

Here are the notes:

---
team sync yesterday
john sarah mike

talked about the new feature launch
decided to push to march instead of feb
too many bugs still

john - fix the auth bug by friday
sarah - update the roadmap
mike - schedule qa session next week

we need to figure out the deployment strategy still
---

When you're ready, type: /meeting-notes
Then paste the notes above when prompted.

I'll check your work and give you feedback!
```

**Success criteria:**
- User invoked /meeting-notes
- User pasted the notes
- Note was saved to vault
- Contains: decisions, action items with owners

**Feedback:**
- Check if file was created in vault
- Parse the saved note
- Validate structure (has Decisions, Action Items, etc.)
- Give specific feedback:
  - ✅ "Great! You extracted 3 action items"
  - ✅ "Perfect - you identified the decision to push to March"
  - 💡 "Tip: I noticed the action items have owners. Try adding due dates next time!"

**Progression:**
When exercise is complete, mark Level 1 done and ask if they want Level 2.

---

## Level 2: Action Item Mastery

**Learning objective:** Use rich metadata for action tracking

**Exercise:**
```
Now let's practice capturing action items with full metadata.

I'll give you 4 tasks to capture. Use /actionitem for each one:

1. Simple task: "Review documentation"

2. Task with owner: "Review documentation" assigned to YOU (@me)

3. Task with owner and due date: "Review documentation" assigned to YOU, due February 10, 2026

4. Full metadata: "Review documentation" assigned to YOU, due February 10, 2026, for project:tutorial, priority:high

Try them one at a time. I'll give you feedback after each!

Start with #1: Just "Review documentation"
```

**Success criteria:**
- User completes all 4 variations
- Syntax is correct for each level
- Items are saved to Quick Capture.md

**Feedback per item:**
1. After first: "Perfect! Now add an owner with @me"
2. After second: "Excellent! Now add a due date with #2026-02-10"
3. After third: "Great! Now add metadata: {{project:tutorial, priority:high}}"
4. After fourth: "🎉 You've mastered the full format!"

**Teach as you go:**
- Show the exact syntax after each step
- Explain what each component does
- Give real-world examples

**Progression:**
Mark Level 2 done, ask about Level 3.

---

## Level 3: Filtering Power

**Learning objective:** Find exactly what you need with filters

**Exercise:**
```
Now that you have some action items, let's learn to find them!

We'll practice 5 different filters:

1. See ALL action items:
   /whatamidoing

2. See just YOUR items:
   /whatamidoing @me

3. See just tutorial project items:
   /whatamidoing project:tutorial

4. See items due this week:
   /whatamidoing this-week

5. Combine filters (your overdue items):
   /whatamidoing @me overdue

Try each one and tell me what you see!
Start with #1: /whatamidoing
```

**Success criteria:**
- User tries all 5 filters
- User observes different results
- User understands how to combine filters

**Feedback per filter:**
- Show count of items returned
- Explain what the filter did
- Show status indicators (🔴 🟡 🟢)
- Point out key items

Example feedback:
```
Great! You found 4 items with /whatamidoing @me

I see:
- 🟡 1 item due soon (Review documentation)
- 🟢 3 items with no due date

Notice how the @me filter only showed YOUR items?
Try adding "overdue" to see if any are past due.
```

**Progression:**
Mark Level 3 done, ask about Level 4.

---

## Level 4: Weekly Digest

**Learning objective:** Generate insights and analytics

**Exercise:**
```
Time to see the big picture! Let's generate your first digest.

Try these three digests:

1. Your personal digest:
   /digest @me

2. Tutorial project digest:
   /digest project:tutorial

3. Full weekly digest:
   /digest weekly

After each one, I'll ask you what you learned from it!
```

**Success criteria:**
- User runs all 3 digests
- User observes different groupings
- User finds the analytics section

**Interactive Q&A:**

After each digest, ask:
```
What did you notice in this digest?
- How many total items did you have?
- Were any overdue?
- What insights did it show?
```

**Feedback:**
- Point out key sections: Summary, Analytics, Insights
- Explain grouping strategy
- Show how to use insights for planning
- Demonstrate filtering options

**Progression:**
Mark Level 4 done, ask about Level 5.

---

## Level 5: Note Sessions & Box Sync

**Learning objective:** Master note-taking with session tracking and optional cloud backup

**Exercise:**
```
Let's learn the /note workflow! I'll guide you through creating, appending, and syncing notes.

PART 1: Create a note session
Type: /note
Then write: "Testing the note system. This is my first practice note."

[Wait for user]

✅ Great! Your note was saved locally.
   Notice it asked which folder? That's automatic organization.

PART 2: Append to the active note
Without running /note end, just type: /note
Then add: "This is an update to the same note."

[Wait for user]

✅ Perfect! It appended to your active note instead of creating a new one.
   This is how you can keep adding to meeting notes throughout a session.

PART 3: End session with Box sync
Now type: /note end

[Wait for user]

You'll see a prompt: "Would you like to copy this note to Box?"
- "Yes" → Copies to Box for cloud backup and sharing
- "No" → Keeps it local only

Try saying "Yes" to see how Box sync works!

[Wait for user]

✅ Excellent! Your note is now in both locations:
   📁 Local: /Users/matthew.beltran/Documents/Obsidian Vault/...
   ☁️  Box: ~/Library/CloudStorage/Box-Box/Notes/Obsidian Vault/...

The Box version will sync to the cloud automatically!
```

**Success criteria:**
- User created a note session
- User appended to the active note
- User ended session and saw Box sync prompt
- User understands local-first + optional cloud workflow

**Feedback:**
- Verify the note was created locally
- Verify content was appended correctly
- If they chose Box sync, verify file was copied
- Explain the benefits of local-first workflow

**Key teaching points:**
```
💡 Why local-first?
- Fast: No waiting for cloud sync while taking notes
- Reliable: Works offline, always saved
- Selective: Only sync what you want to share

💡 When to sync to Box?
✅ Important meeting notes
✅ Notes to share with team
✅ Archive-worthy decisions
✅ Cross-device access needs

💡 When to keep local?
✅ Personal brainstorms
✅ Temporary notes
✅ Work-in-progress drafts
```

**Progression:**
Mark Level 5 done, ask about Level 6.

---

## Level 6: Workflow Integration

**Learning objective:** Build a sustainable daily/weekly workflow

**Exercise:**
```
Final level! Let's build your personal workflow.

I'm going to give you a scenario for each day of the week.
You'll respond with the appropriate command(s).

MONDAY MORNING:
You arrive at work. What's the first command you'd run to see what needs attention?

[Wait for user answer]

✅ Perfect! /whatamidoing @me overdue
   This shows what you missed over the weekend.

DURING A MEETING:
You're in a meeting taking notes. What will you do after?

[Wait for user answer]

✅ Exactly! /meeting-notes
   Then paste your notes to structure them.

TEAMMATE ASKS YOU TO DO SOMETHING:
Sarah asks: "Can you review my PR by Thursday?"
How do you capture this?

[Wait for user answer]

✅ Nice! /actionitem Review Sarah's PR @me #2026-02-06

FRIDAY AFTERNOON:
You want to see how your week went. What command?

[Wait for user answer]

✅ Perfect! /digest @me
   This shows your week in review with analytics.
```

**Success criteria:**
- User correctly identifies the right command for each scenario
- User understands when to use each skill
- User can articulate their workflow

**Final Feedback:**
```
🎉 Congratulations! You've completed all 6 levels!

You now know how to:
✅ Parse meeting notes into structured summaries
✅ Track action items with rich metadata
✅ Filter and find exactly what you need
✅ Generate insightful digests
✅ Use note sessions with optional Box sync
✅ Build an effective workflow

Your Meeting Intelligence System is ready to use!

Want a quick reference? Check out:
- WALKTHROUGH.md - Comprehensive guide
- QUICK_START.md - 5-minute quickstart
- README.md - Full documentation

Keep practicing and the skills will become second nature!
```

**Progression:**
Mark tutorial complete, save final state.

---

## Response Format

### Welcome Message (New User)
```
👋 Welcome to the Meeting Intelligence Tutorial!

I'm going to teach you how to transform messy meeting notes into structured, searchable summaries with smart action tracking.

This tutorial has 6 hands-on levels:
1️⃣ Parse your first meeting note
2️⃣ Master action item capture
3️⃣ Learn powerful filtering
4️⃣ Generate weekly digests
5️⃣ Note sessions & Box sync
6️⃣ Build your workflow

⏱️ Time: ~25 minutes total
🎯 You'll get real-time feedback on each exercise
💡 Learn by doing, not just reading

Ready to start Level 1? (yes/no)
```

### Progress Message (Returning User)
```
👋 Welcome back!

Your progress:
✅ Level 1: First Meeting Note - Completed
✅ Level 2: Action Item Mastery - Completed
⏸️ Level 3: Filtering Power - In Progress

You're 40% through the tutorial!

Ready to continue with Level 3? (yes/continue/restart)
```

### Level Completion Message
```
🎉 Level 1 Complete!

What you learned:
✅ How to use /meeting-notes
✅ Auto-extract decisions and actions
✅ Smart tagging for meetings

Progress: 1 of 6 levels complete (17%)

Next up: Level 2 - Action Item Mastery
Learn to capture tasks with owners, due dates, and metadata.

Ready for Level 2? (yes/no/take a break)
```

## Important Notes

- **Be encouraging and supportive** - positive reinforcement
- **Give specific feedback** - "Great! You extracted 3 action items" not just "Good job"
- **Teach progressively** - don't overwhelm with all features at once
- **Show real output** - actually check what the user created
- **Be patient** - let them try, fail, and retry
- **Celebrate wins** - emoji reactions, enthusiastic feedback
- **Make it interactive** - ask questions, wait for responses
- **Adapt to pace** - if struggling, give more hints; if excelling, move faster
- **Track everything** - save progress so they can continue later
- **Reference docs** - point to WALKTHROUGH.md for deeper dives

## State File Management

**After each completed level:**
```bash
cat > ~/.claude/meeting-intelligence-tutorial-state.json <<EOF
{
  "current_level": 2,
  "completed_exercises": ["level_1_meeting_notes"],
  "started_at": "2026-02-03T10:00:00Z",
  "last_session": "2026-02-03T10:15:00Z",
  "user_name": "matthew.beltran"
}
EOF
```

**On tutorial completion:**
```bash
cat > ~/.claude/meeting-intelligence-tutorial-state.json <<EOF
{
  "current_level": 7,
  "completed_exercises": ["level_1_meeting_notes", "level_2_action_items", "level_3_filtering", "level_4_digest", "level_5_note_sessions", "level_6_workflow"],
  "started_at": "2026-02-03T10:00:00Z",
  "completed_at": "2026-02-03T10:30:00Z",
  "last_session": "2026-02-03T10:30:00Z",
  "user_name": "matthew.beltran",
  "status": "completed"
}
EOF
```

## Validation

**Check if user actually did the exercise:**
- Look for newly created files in vault
- Read Quick Capture.md to verify action items were added
- Parse meeting notes to check structure
- Count items returned by filters

**Give actionable feedback:**
- ❌ "Hmm, I don't see a new meeting note. Did you save it? Try again."
- ✅ "Perfect! I found your note at: Dailies/2026-02-03 - Team Sync.md"
- 💡 "Tip: I noticed you didn't include a due date. Try adding #2026-02-10"
