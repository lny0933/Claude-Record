---
name: feedback_list_memories_after_save
description: "After saving any memory, always list all current memories for the user to review"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 7feafe17-ea35-4b6b-9210-2885b5ceb648
---

After saving any memory entry, always enumerate all current memories in full for the user to review.

**Why:** User wants visibility into the full memory state after every write.

**How to apply:** Immediately after every memory write (new or update), read MEMORY.md and list all entries with their file content summary.
