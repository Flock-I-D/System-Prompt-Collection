---
description: Analyze coding problems and provide focused implementation plans with complexity assessment
---

# Problem Analysis Workflow

When the user says "I want to implement/refactor/fix X", follow this workflow:

## Steps

### 1. Search & Understand
- Use `code_search` to locate relevant code
- **Check implementation status:**
  - **Already implemented** - Inform user, avoid duplicate work
  - **Partially implemented** - Identify what's missing/incomplete
  - **Needs refactor** - Assess if refactor better than new implementation
  - **Not implemented** - Proceed with new implementation
- Read existing implementations and related patterns
- Identify affected files, modules, and dependencies

### 2. Analyze
**Current State:** Implementation status, how it currently works, what's missing/broken
**Required Changes:** What to add/modify/remove/refactor, which files affected

### 3. Assess Complexity
- **LOW** (1-2h): Single file, no deps, straightforward
- **MEDIUM** (3-8h): Multiple files, may need deps, some architecture
- **HIGH** (1+ days): System-wide, new infrastructure, extensive testing

### 4. Pre-Implementation Alignment
- **Goal & scope**: Define what success is and what is explicitly out of scope
- **Assumptions**: List technical assumptions, mark fragile ones, and how to validate them
- **Approach decision**:
  - Propose at least 2 approaches
  - Compare trade-offs
  - Choose one and justify
- **Contracts & boundaries**: Define inputs/outputs, expected types, and possible errors
- **Acceptance criteria (DoD)**: State what must be true to consider it done
- **Testing & observability**: What to test and how you’d debug/observe failures (logs/metrics)
- **Risks & intentional debt**: Risks to watch and debt you’re choosing to accept

### 5. Create Implementation Plan
- Break down into ordered phases and steps
- Specify files to create/modify
- Highlight risks and testing strategy
- **Stay focused** - only address what was asked

### 6. Save to task.md
After user confirms, save the plan to `task.md` with:
```markdown
# Task: [Problem Statement]

**Complexity:** 🟢/🟡/🔴 [LEVEL] - [Time]
**Status:** In Progress
**Started:** [Date]

## Assumptions
- [Assumption 1]

## Approach
- **Chosen approach:** [Name]
- **Alternatives considered:**
  - [Alt 1] - [Trade-off]

## Implementation Checklist

### Phase 1: [Name]
- [ ] Step 1
- [ ] Step 2

### Phase 2: [Name]
- [ ] Step 3

## Acceptance Criteria
- [Criterion 1]

## Notes
- Key decisions and approaches

## Testing & Observability
- **Tests:** [What to test]
- **Debug/observability:** [Logs/metrics]

## Risks
- Important considerations
```

## Response Template

```markdown
# Problem Analysis: [Statement]

## Current State
[Brief description]

## Required Changes
[What needs to happen]

## Pre-Implementation Alignment
**Goal & scope:** [What is in/out]

**Assumptions:**
- [Assumption 1] - [How to validate]

**Approach decision:**
- **Option A:** [Pros/cons]
- **Option B:** [Pros/cons]
- **Chosen:** [A/B] - [Why]

**Contracts & boundaries:**
- Inputs:
- Outputs:
- Errors:

**Acceptance criteria (DoD):**
- [Criterion 1]

**Testing & observability:**
- Tests:
- Debug/observability:

## Complexity Assessment
🟢/🟡/🔴 [LEVEL] - [Time]
- [Why this level]

## Implementation Plan

### Phase 1: [Name]
- [ ] Task 1
- [ ] Task 2

## Files to Modify/Create
- `path/file.py` - [Changes]

## Risks
- [Key considerations]

---
**Ready to proceed?**