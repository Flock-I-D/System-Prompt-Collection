---
description: Execute tasks from task.md in order with progress tracking
---

# Task Implementation Workflow

Execute implementation tasks from `task.md` systematically.

## Steps

### 1. Read Current Task
- Read `task.md` to identify next pending task: `- [ ]`
- Understand the task context and requirements
- Check dependencies - ensure previous tasks are completed

### 2. Implement Task
- Follow repository guidelines (see `AGENTS.md`)
- Make focused, minimal changes
- Use existing patterns and conventions
- Add necessary imports, error handling, and validation
- **Test as you go** - don't wait until the end

### 3. Verify Implementation
- Run the code to verify it works
- Check for errors or warnings
- Test edge cases if applicable
- Verify integration with existing code

### 4. Update task.md
- Mark task as completed: `- [x]`
- Add implementation notes if needed
- Update status and progress
- Commit changes with descriptive message

### 5. Move to Next Task
- Identify next pending task `- [ ]`
- If all tasks complete, update overall status to "Completed"
- Summarize what was accomplished

## Implementation Rules

- **One task at a time** - Complete before moving to next
- **Sequential order** - Follow phase order unless dependencies allow parallel work
- **Validate continuously** - Test after each task, not at the end
- **Update immediately** - Mark tasks done as you complete them
- **Stay focused** - Don't add features not in the task list
- **Ask for help** - If blocked, explain the issue clearly

## Progress Tracking

After each task completion, update `task.md`:

```markdown
### Phase 1: [Name]
- [x] Step 1 ✅ Completed
- [x] Step 2 ✅ Completed
- [ ] Step 3 ⏳ In progress
```

Add notes section for important decisions:
```markdown
## Implementation Notes
- **[Date]**: Completed Phase 1 - Used X approach for Y
- **[Date]**: Modified Step 3 - Changed from A to B because...
```

## When Stuck

If you encounter issues:
1. **Document the blocker** in task.md
2. **Explain what you tried** and what didn't work
3. **Ask specific questions** about the problem
4. **Suggest alternatives** if you see other approaches

## Task Completion

When all tasks are done:
1. Mark overall status as "Completed"
2. Add completion date
3. Run full test suite if available
4. Update documentation if needed
5. Summarize implementation and key decisions
