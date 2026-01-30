---
name: actionitem
description: Quickly add an action item that will appear in /whatamidoing
---

# Quick Action Item Capture

Add a new action item to your Quick Capture list. These items will automatically appear when you run `/whatamidoing`.

## Vault Location
`/Users/matthew.beltran/Documents/Obsidian Vault`

## Capture File
`/Users/matthew.beltran/Documents/Obsidian Vault/Quick Capture.md`

## Instructions

1. **Get the action item text from the user's command**:
   - The user will provide the action item text as an argument
   - Example: `/actionitem Review the new API documentation`

2. **Check if the capture file exists**:
   - Use Read tool to check if `Quick Capture.md` exists
   - If it doesn't exist, create it with proper YAML frontmatter

3. **Append the action item**:
   - Read the current contents of the file
   - Append a new uncompleted checkbox item: `- [ ] <action item text>`
   - Use Edit tool to add the new item to the file
   - Add items under an "## Action Items" section

4. **File format** (if creating new):
   ```markdown
   ---
   created: YYYY-MM-DD
   tags: [quick-capture, action-items]
   ---

   # Quick Capture

   ## Action Items
   - [ ] <action item text>
   ```

5. **Response to user**:
   - Confirm the action item was added
   - Keep the response brief (e.g., "✓ Added: Review the new API documentation")

## Important Notes
- **BE FRICTIONLESS**: This skill should be as quick as possible
- **DO NOT ask about committing changes** - just add the item and confirm
- **DO NOT ask follow-up questions** unless the action item text is completely missing
- Always append to the "## Action Items" section
- Maintain the checkbox format: `- [ ] ` followed by the text
- Keep the response minimal - just confirm it was added
- If no action item text is provided, ask the user what they want to add
