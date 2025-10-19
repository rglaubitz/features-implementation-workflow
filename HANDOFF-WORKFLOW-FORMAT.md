# Handoff Workflow Format for Multi-Day Development

**Created:** October 19, 2025
**Purpose:** Document the preferred format for managing multi-day/multi-week development projects with Claude Code

---

## Pattern Overview

This format enables **seamless context handoffs and continuation across sessions** with zero context loss. It was successfully used for the Graphiti + JSON Integration upgrade (Week 3 Staging Lifecycle).

## Core Components

### 1. Handoff Document Structure

**Location:** `upgrades/active/{project-name}/handoffs/HANDOFF-{PHASE}-{DAYS}.md`

**Example:** `HANDOFF-WEEK3-DAYS1-3.md`

**Template Structure:**

```markdown
# {Phase} Days {X-Y} Complete - Handoff to Days {Z+}

**Date:** {ISO Date}
**Upgrade:** {Project Name}
**Status:** {Phase} {X}% Complete (Days {X-Y} done) | Days {Z+} Ready

---

## 🎯 What Was Accomplished

### {Phase} Days {X-Y}: {Feature Name}

**Goal:** {One-line goal}
**Result:** ✅ **COMPLETE** - All {N} tests passing

**Progress:**
- ✅ **Day {X}:** {Feature} ({N} tests PASSING)
- ✅ **Day {Y}:** {Feature} ({N} tests PASSING)

**Test Count:** {Total} total ({Baseline} baseline + {New} new)

---

## 📂 Files Created/Modified

### Day {X}: {Feature Name}

**Modified:** `{filepath}`
- **Lines:** ~{start}-{end} ({description}, ~{N} lines)
- **Function:** `{function_signature}`
- **Key Features:**
  - Feature 1
  - Feature 2
- **Returns:** {return description}
- **Metrics:** `{metric_name}` ({description})
- **Error Handling:** {error types}

**Created:** `{test_filepath}` ({N} lines)
- **TEST 1:** {Test description} ✅
- **TEST 2:** {Test description} ✅
- **Result:** {N}/{N} passing

**Test Fix Applied:**
- {Description of any test fixes}
- **Reason:** {Why fix was needed}

---

## 🔑 Architectural Decisions

### Decision 1: {Decision Name}
**Context:** {Why this decision was needed}
**Decision:** {What was decided}
**Rationale:**
- Reason 1
- Reason 2
- Can migrate to {alternative} later if needed

---

## 📊 Test Coverage

### Test Suite Breakdown

**Unit Tests ({N} total):**
- `{test_file}.py` - {N} tests ✅
- `{test_file}.py` - {N} tests ✅

**All Tests Passing:**
```bash
{test output showing all passing tests}
```

**Baseline Tests:** ✅ {N} tests still passing (Enhanced Saga preserved)

---

## 🔧 Implementation Patterns Used

### Pattern 1: {Pattern Name}
```python
# Code example showing the pattern
```

---

## 🚧 Known Issues

**None** - All tests passing, no blockers for Days {Z+}

---

## 📋 What's Next: {Phase} Days {Z+}

### Day {Z}: {Feature Name} ({N} tests)
**Goal:** {One-line goal}

**Implementation Plan:**
1. Step 1
2. Step 2
3. Step 3
4. Metrics:
   - `{metric_name}` ({type})

**Tests:** `tests/{test_file}.py`
- **TEST 1:** {Test description}
- **TEST 2:** {Test description}

**Estimated Duration:** {X} hours

---

## 📊 Progress Tracking

**Overall Project:** {X}% complete
- Week 1: {Feature} ✅ 100%
- Week 2: {Feature} ✅ 100%
- **Week {N}: {Feature} 🚀 {X}%** (Days {X-Y} done, Days {Z+} remaining)
- Week {N+1}: {Feature} ⏳ 0%

**Test Count:**
- **Current:** {N} total ({breakdown})
- **After Days {Z+}:** {N} total ({breakdown})

**Files Modified/Created (Days {X-Y}):**
- Modified: {N} files ({list})
- Created: {N} files ({list})
- **Total New Code:** ~{N} lines

---

## 🔗 Key References

**Documentation:**
- [PROGRESS.md](../path/PROGRESS.md) - Overall upgrade progress
- [PLANNING.md](../path/PLANNING.md) - {N}-week implementation plan
- [IMPLEMENTATION.md](../path/IMPLEMENTATION.md) - Step-by-step guide

**Code Locations:**
- {Component}: `{filepath}` ({description})

**Related Handoffs:**
- [HANDOFF-{PREVIOUS}.md](HANDOFF-{PREVIOUS}.md) - Previous work

---

## 💡 Tips for Next Session

**Start Command:**
```
Continue {Phase}. Days {X-Y} complete ({X}%).

**Just Completed:**
- Day {X}: {feature} ✅
- Day {Y}: {feature} ✅

**Next: Day {Z} - {feature}**
- Implement {component}
- {Key task}
- Tests: {N} unit tests

**Context:**
- {Current}/{Expected} tests passing
- {X}% overall project complete
- All previous tests green
- Read HANDOFF-{PHASE}-DAYS{X-Y}.md for full context
```

**Key Files to Reference:**
- `{file}.py` - {Why to reference}

**Testing Strategy:**
- Run individual test file first: `pytest {path} -v`
- Verify baseline tests still pass: `pytest {paths} -v`
- Update PROGRESS.md after each day completion

---

**Total Duration (Days {X-Y}):** ~{X} hours
**Lines of Code:** ~{N} lines
**Test Pass Rate:** {N}/{N} (100%)
**Status:** ✅ Ready for Days {Z+}
```

---

### 2. Quick Reference Document

**Location:** `upgrades/active/{project-name}/CLAUDE-QUICK-REFERENCE.md`

**Purpose:** Fast lookup for common patterns, file locations, test commands

**Key Sections:**
- 🚀 **Starting a New Session** (files to read in order)
- 📂 **Key Directory Locations** (organized file tree)
- 🎯 **Common Patterns** (code templates with examples)
- 📊 **Test Execution Commands** (copy-paste ready)
- 📝 **Progress Tracking Workflow** (when to update what)
- 🔑 **Key Metrics to Track** (current status at a glance)
- 🚨 **Important Reminders** (always do / never do)
- 🔗 **Quick Links** (essential reading)
- 🎯 **Current Session Template** (copy-paste starter for next session)

**Example Quick Reference Pattern:**
```markdown
## 🎯 Common Patterns

### Pattern 1: Adding a New Temporal Activity

**File:** `apex-memory-system/src/apex_memory/temporal/activities/ingestion.py`

```python
@activity.defn
async def activity_name(...) -> ReturnType:
    """Brief description."""
    import required_modules  # Import inside function

    record_temporal_activity_started('activity_name')

    try:
        # Activity logic
        record_temporal_data_quality(metric_type='...', value=...)
        record_temporal_activity_completed('activity_name', success=True)
        return result

    except ApplicationError:
        record_temporal_activity_completed('activity_name', success=False)
        raise
```

**Corresponding Test Pattern:**
```python
@pytest.mark.asyncio
async def test_activity_success():
    with patch('apex_memory.temporal.activities.ingestion.record_temporal_activity_started'), \
         patch('...') as mock_...:
        result = await activity_name(...)
        assert result == expected
```
```

---

### 3. Progress Tracking Document

**Location:** `upgrades/active/{project-name}/PROGRESS.md`

**Updated After Each Day:**
- Change status from "pending" to "completed" ✅
- Add implementation details under completed section
- Update test count (Current vs. Expected Final)
- Add test results (X/X passing)
- Move day from "Remaining Deliverables" to "Completed Deliverables"

**Example Update:**
```markdown
## 🚀 Week 3: Staging Lifecycle (IN PROGRESS - Day 4 Complete)

**Status:** 🚀 **In Progress** (80% complete - Days 1-4 done, Day 5 remaining)
**Tests Planned:** 15 tests | **Tests Created:** 13 tests (3+3+5+2)

### Completed Deliverables

#### Day 4: cleanup_staging_activity ✅
- [x] Remove staging after success ✅
- [x] Update metadata for failed ingestions ✅
- [x] Tests: 2 tests ✅
  - **Test Results:** 2/2 passing (100%) ✅

**Current Test Count:** 177 total (121 baseline + 11 Graphiti + 32 JSON + 13 staging)
```

---

### 4. Handoff Index

**Location:** `upgrades/active/{project-name}/handoffs/INDEX.md`

**Updated When Creating Handoffs:**
- List all handoffs chronologically
- Link to each handoff document
- Show progression through phases
- Indicate completion status

**Example:**
```markdown
# Handoff Documents Index

## Week 3: Staging Lifecycle

- [HANDOFF-WEEK3-DAYS1-3.md](HANDOFF-WEEK3-DAYS1-3.md) - Days 1-3 complete (60%) ✅
- [HANDOFF-WEEK3-DAYS4-5.md](HANDOFF-WEEK3-DAYS4-5.md) - Days 4-5 complete (100%) ✅

## Section 9: Temporal Integration

- [HANDOFF-SECTION-9.md](HANDOFF-SECTION-9.md) - Section 9 complete (82% overall) ✅
```

---

## Why This Format Works

### Strengths

1. **Zero Context Loss**
   Everything needed to continue is documented: code locations, decisions, patterns, fixes

2. **Copy-Paste Continuation**
   "Start Command" box lets you resume instantly in next session

3. **Complete Traceability**
   Every decision, fix, and pattern is documented with WHY not just WHAT

4. **Baseline Preservation**
   Always track that existing tests still pass (no regressions)

5. **Time Estimates**
   Helps plan sessions and set expectations

6. **Architecture Record**
   Documents WHY decisions were made, not just WHAT was implemented

7. **Fix Documentation**
   Test fixes are documented with reasons (helps avoid repeat issues)

8. **Pattern Library**
   Implementation patterns section becomes reusable template library

---

## Best Practices

### When to Create Handoffs

1. **End of Phase/Week** (natural break point)
2. **Before Major Architectural Shift** (switching components)
3. **After Completing Multiple Days** (2-3 days work)
4. **Before Expected Context Compact** (preserve continuity)

### What to Always Include

1. ✅ **Exact file paths with line numbers** (`file.py:100-200`)
2. ✅ **Function signatures** (helps locate code)
3. ✅ **Test output** (copy actual pytest results)
4. ✅ **Architectural decisions with rationale** (WHY chosen)
5. ✅ **Test fixes with reasons** (avoid repeat issues)
6. ✅ **Baseline test verification** (no regressions)
7. ✅ **Copy-paste "Start Command"** (instant continuation)
8. ✅ **Time estimates for next steps** (planning)

### Update Workflow

**After Each Day:**
```
1. Update PROGRESS.md (move day to completed, update counts)
2. Update test counts (current vs. final expected)
3. Verify baseline tests still pass
```

**After Multiple Days (Handoff Point):**
```
1. Create HANDOFF-{PHASE}-DAYS{X-Y}.md with full template
2. Update handoffs/INDEX.md with new entry
3. Include "Start Command" for next session
4. Document all architectural decisions made
5. Include all test fixes applied
```

---

## Session Continuity Pattern

### End of Session N
```
1. Complete Day X
2. Update PROGRESS.md
3. Create HANDOFF-{PHASE}-DAYSX-Y.md (if at break point)
4. Update handoffs/INDEX.md
5. Provide "Start Command" for next session
```

### Start of Session N+1
```
1. User provides: "Read HANDOFF-{PHASE}-DAYSX-Y.md"
2. Claude reads handoff + CLAUDE-QUICK-REFERENCE.md
3. User provides "Start Command" from handoff
4. Claude continues Day X+1 with full context
5. Zero time spent re-discovering architecture
```

---

## File Naming Conventions

### Handoffs
- **Format:** `HANDOFF-WEEK{N}-DAYS{X}-{Y}.md` or `HANDOFF-SECTION-{N}.md`
- **Examples:**
  - `HANDOFF-WEEK3-DAYS1-3.md` (Week-based)
  - `HANDOFF-SECTION-9.md` (Section-based)

### Progress & Reference
- **Progress:** `PROGRESS.md` (singular, one per project)
- **Quick Reference:** `CLAUDE-QUICK-REFERENCE.md` (singular)
- **Index:** `handoffs/INDEX.md` (updated with each new handoff)

### Test Files
- **Format:** `test_{feature_name}.py`
- **Examples:**
  - `test_cleanup_staging_activity.py`
  - `test_staging_manager.py`

---

## Metrics to Track

### Overall Project
- **Completion Percentage:** {X}% complete
- **Phase Breakdown:** Week 1: 100%, Week 2: 100%, Week 3: 80%, Week 4: 0%

### Current Phase
- **Phase Completion:** {X}% complete (Days done / Total days)
- **Days Completed:** X/Y days

### Testing
- **Test Count:** Current vs. Expected Final
- **Baseline Preservation:** {N} tests still passing
- **Pass Rate:** {N}/{N} (100%)

### Code Metrics
- **Lines of Code:** New code added per day/phase
- **Files Modified:** Count and list
- **Files Created:** Count and list

### Time Tracking
- **Duration:** Actual time spent vs. estimated
- **Per Day:** Track actual hours for future estimates

---

## Integration with TODO System

### During Active Work
- Use `TodoWrite` to track tasks within a day
- Mark todos complete as you finish each task
- Keep todos granular (1-2 hour chunks)

### In Handoff Documents
- Handoff documents capture completed todos permanently
- "What Was Accomplished" section = completed todos
- "What's Next" section = upcoming todos

### Pattern
```
Active Session:
├── TodoWrite: Track current day tasks
├── Update todos as you complete each
└── Clear todos at end of day

Handoff Document:
├── "What Was Accomplished" = Completed todos
└── "What's Next" = Upcoming todos for next session
```

---

## Example: Successful Application

### Graphiti + JSON Integration (Week 3)

**Project:** 4-week upgrade (Graphiti integration + JSON support + Staging + Two Workflows)

**Handoff Created:** HANDOFF-WEEK3-DAYS1-3.md

**What Worked:**
- ✅ **Zero context loss** across 3-day implementation
- ✅ **Instant continuation** in next session (used "Start Command")
- ✅ **All architectural decisions preserved** (Local staging vs S3)
- ✅ **All test fixes documented** (httpx patching pattern)
- ✅ **Baseline tests verified** (121 Enhanced Saga tests preserved)
- ✅ **Pattern library created** (StagingManager usage patterns)

**Results:**
- 11 tests created (Days 1-3)
- 100% pass rate
- ~1,017 lines of code
- 3 architectural decisions documented
- 2 test fixes documented with reasons
- Next session: Picked up Day 4 instantly with full context

---

## Template Files

### Minimal Handoff Template
Location: `workflow/templates/HANDOFF-TEMPLATE.md`

### Minimal Quick Reference Template
Location: `workflow/templates/QUICK-REFERENCE-TEMPLATE.md`

### Minimal Progress Template
Location: `workflow/templates/PROGRESS-TEMPLATE.md`

---

## Summary

This handoff workflow format enables **seamless multi-session development** with:
- ✅ Zero context loss
- ✅ Instant session continuation
- ✅ Complete traceability
- ✅ Pattern reusability
- ✅ Baseline preservation
- ✅ Architecture documentation

**Use this format for any multi-day/multi-week development project to ensure continuity and quality.**

---

**Created:** October 19, 2025
**Last Updated:** October 19, 2025
**Status:** ✅ Active Pattern
**Success Rate:** 100% (Graphiti + JSON Integration Week 3)
