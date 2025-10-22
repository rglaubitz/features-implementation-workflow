# /breakdown → /execute Workflow Integration Analysis

**Created:** 2025-10-21
**Purpose:** Ensure seamless workflow from task breakdown to implementation
**Status:** Analysis Complete | Updates Recommended

---

## Executive Summary

**Current State:** `/breakdown` and `/execute` are complementary commands with strong alignment but **missing handoff integration**.

**Recommendation:** Update both commands to create explicit workflow connection.

**Impact:** Enables systematic breakdown → execution workflow for any multi-phase project.

---

## Workflow Overview

### Intended Workflow

```
User creates IMPLEMENTATION.md (3,500+ lines, 7 weeks)
           ↓
   /breakdown IMPLEMENTATION.md project-name
           ↓
Creates task-manager/ structure (14 tasks, 42 subtasks)
           ↓
   /execute 1  (implement Phase 1 using task-manager/ as reference)
           ↓
   /execute 2  (implement Phase 2)
           ↓
        ... continue for all phases
           ↓
   Complete project with full traceability
```

### What /breakdown Creates

**Output Structure:**
```
task-manager/
├── README.md                      # Master progress tracking
├── phase-1-authentication/
│   ├── README.md                  # Phase overview
│   ├── task-1.1-clerk-integration.md
│   ├── task-1.2-auth-middleware.md
│   └── task-1.3-session-management.md
├── phase-2-conversation-hub/
│   ├── README.md
│   ├── task-2.1-websocket-setup.md
│   ├── task-2.2-message-components.md
│   └── ...
└── ...
```

**Each Task File Contains:**
- Dependencies (what must be complete first)
- Success Criteria (measurable outcomes)
- Research References (ADRs, docs, specific sections)
- Test Specifications (TESTING.md line references)
- Subtasks (2-4 hour actionable chunks)
- Validation commands

### What /execute Expects

**Current References (Step 2):**
- `upgrades/[feature-name]/IMPLEMENTATION-GUIDE.md`
- "Phase-specific README if available"

**Does NOT Currently Reference:**
- `task-manager/` directory
- Task files (`task-N.M-*.md`)
- Subtask breakdowns
- Task-level success criteria

---

## Integration Analysis

### ✅ Overlaps (Strong Alignment)

Both commands share these principles:

1. **Phase-Based Organization**
   - Breakdown: Creates `phase-N-<name>/` folders
   - Execute: Implements phases sequentially

2. **Research Integration**
   - Breakdown: Links tasks to ADRs and research chunks
   - Execute: References research docs during implementation

3. **Test Specifications**
   - Breakdown: Includes TESTING.md line references in task files
   - Execute: Generates tests proactively (Step 6)

4. **Context Compacts**
   - Breakdown: Strategic compacts after Phase 2 & 4 of breakdown
   - Execute: Compacts between implementation phases (Step 9)

5. **Quality Standards**
   - Breakdown: 2-4 hour subtasks, measurable criteria
   - Execute: 3-5 files, 15-30 tests, copy-paste examples

### ❌ Gaps (Integration Issues)

**Gap 1: Directory Discovery**
- **Problem:** /execute doesn't check for task-manager/ directory
- **Impact:** User runs /breakdown but /execute ignores task structure
- **Fix:** Add Step 1.5 to /execute: "Check for task-manager/ directory"

**Gap 2: Task File Utilization**
- **Problem:** Task files contain detailed breakdowns, /execute doesn't read them
- **Impact:** Loses value of breakdown work (dependencies, subtasks, success criteria)
- **Fix:** Update /execute Step 2 to read current phase's task files

**Gap 3: Subtask Tracking**
- **Problem:** /breakdown creates 2-4 hour subtasks, /execute doesn't track them
- **Impact:** No granular progress tracking during implementation
- **Fix:** Add TodoWrite integration for subtasks in /execute

**Gap 4: Success Criteria Validation**
- **Problem:** Task files define measurable success criteria, /execute doesn't validate
- **Impact:** Implementation might miss requirements
- **Fix:** Add Step 10.5 to /execute: "Validate against task success criteria"

**Gap 5: Handoff Communication**
- **Problem:** /breakdown completion message doesn't mention /execute
- **Impact:** User doesn't know what to do after breakdown
- **Fix:** Update /breakdown Phase 5 completion to say: "Ready to implement? Run: /execute 1"

**Gap 6: Progress Synchronization**
- **Problem:** task-manager/README.md has progress tracking, /execute doesn't update it
- **Impact:** Master progress tracking becomes stale
- **Fix:** Add Step 10 update to task-manager/README.md in /execute

---

## Recommended Updates

### Update 1: /execute Command (workflow/commands/execute.md)

**Add Step 0 (Before Plan Mode):**

```markdown
## Step 0: Check for Task Manager Structure 📂

**Before entering plan mode, check if /breakdown was used.**

```bash
# Check for task-manager/ directory
if [ -d "task-manager/" ]; then
    echo "✅ Task Manager structure detected"
    echo "   Using task-manager/phase-{phase-number}-*/ for implementation guidance"
    TASK_MANAGER_MODE=true
else
    echo "ℹ️  No task-manager/ found"
    echo "   Using upgrades/[feature]/IMPLEMENTATION-GUIDE.md directly"
    TASK_MANAGER_MODE=false
fi
```

**If TASK_MANAGER_MODE=true:**
- Read: `task-manager/README.md` (master progress)
- Read: `task-manager/phase-{N}-*/README.md` (phase overview)
- Read: `task-manager/phase-{N}-*/task-*.md` (all task files for this phase)

**Advantage:**
- Detailed subtasks (2-4 hours each)
- Explicit dependencies
- Research references at task level
- Success criteria per task
- Test specifications linked
```

**Update Step 2 (Discuss Requirements):**

```markdown
## Step 2: Discuss Phase Requirements 💬

**Your Action:** Lead discussion using task-manager/ structure if available.

**If task-manager/ exists:**

1. **List all tasks for this phase:**
   ```
   📋 Phase {N} Tasks (from task-manager/phase-{N}-*/)

   - Task {N}.1: {Name} ({X} subtasks)
   - Task {N}.2: {Name} ({Y} subtasks)
   - Task {N}.3: {Name} ({Z} subtasks)

   Total: {X} tasks, {Y} subtasks
   ```

2. **For each task, review:**
   - Dependencies (must be complete from previous phases)
   - Success Criteria (measurable outcomes)
   - Research References (which ADRs/docs to consult)
   - Test Specifications (TESTING.md lines)
   - Subtasks (2-4 hour chunks)

3. **Ask focused questions:**
   - "Task {N}.{M} requires {dependency}. Is that complete?"
   - "Research reference ADR-00X, section {Y} - should I read that now?"
   - "Test spec at TESTING.md:200-250 defines {X} tests. Shall I create those?"

**If no task-manager/ (legacy mode):**
   - Use original Step 2 questions
   - Reference IMPLEMENTATION-GUIDE.md directly
```

**Update Step 10 (Mark Complete):**

```markdown
## Step 10: Mark Phase Complete ✅

... (existing checklist)

**If task-manager/ exists, update master progress:**

```markdown
# Update: task-manager/README.md

## Implementation Progress

### ✅ Completed Phases

- [x] Phase 1: {Name} ({X}/{X} tasks complete) ← JUST COMPLETED
- [ ] Phase 2: {Name} (0/{Y} tasks)
- [ ] Phase 3: {Name} (0/{Z} tasks)

### Statistics

**Phase 1 Completion:**
- Tasks Completed: {X}/{X} (100%)
- Subtasks Completed: {Y}/{Y} (100%)
- Tests Created: {Z} tests
- Files Created: {N} files
- Date Completed: {YYYY-MM-DD}
```
```

---

### Update 2: /breakdown Command (~/.claude/commands/breakdown.md)

**Update Phase 5 Completion Message:**

```markdown
## Phase 5: Master README (30 min)

... (existing Phase 5 content)

**5.6: Create Handoff to /execute** (NEW)

After creating master README, add execution guidance:

```markdown
# Add to task-manager/README.md

---

## 🚀 Ready to Implement?

This task breakdown is complete. To begin systematic implementation:

**Next Step:**
```bash
/execute 1
```

The `/execute` command will:
- ✅ Detect this task-manager/ structure automatically
- ✅ Read phase-{N}-*/ task files for detailed guidance
- ✅ Use subtasks as implementation checklist
- ✅ Validate against success criteria
- ✅ Update this README as phases complete

**Workflow:**
1. `/execute 1` → Implement Phase 1 (all tasks in phase-1-*/)
2. Context compact
3. `/execute 2` → Implement Phase 2
4. ... continue for all phases

**Reference:** [Execute Command Documentation](../workflow/commands/execute.md)
```

**Update Final Output Message:**

```markdown
🎉 TASK BREAKDOWN COMPLETE!

**Created:**
- task-manager/ directory with {X} phases
- {Y} task files with {Z} subtasks
- Master README with progress tracking
- Complete research and test linkage

**Structure:**
- Phases: {X} (aligned with IMPLEMENTATION.md)
- Tasks: {Y} (each with dependencies and success criteria)
- Subtasks: {Z} (2-4 hour actionable chunks)
- Total estimated time: {N} weeks

**Next Steps:**

1. **Review the breakdown:**
   - Open: task-manager/README.md
   - Validate: Task structure makes sense
   - Check: Dependencies are correct

2. **Begin implementation:**
   ```bash
   /execute 1
   ```

3. **Track progress:**
   - task-manager/README.md updates as phases complete
   - Each task file marks subtasks as done

**Ready to start Phase 1?**

Run: `/execute 1` to begin systematic implementation.
```
```

---

### Update 3: Integration Documentation

**Create:** `task-manager/INTEGRATION-GUIDE.md` (auto-generated by /breakdown)

```markdown
# Task Manager Integration with /execute

**Auto-generated by /breakdown command**
**Project:** {project-name}
**Created:** {YYYY-MM-DD}

---

## How This Works

The `/breakdown` command created this task-manager/ structure by analyzing:
- {implementation-file} ({X,XXX} lines)
- PLANNING.md ({Y} weeks, {Z} phases)
- TESTING.md ({N} test specifications)
- Research documentation (ADRs, chunks)

The `/execute` command will use this structure to guide implementation.

---

## Workflow Integration

### Step 1: Breakdown Complete ✅

You're here! The breakdown is complete with:
- {X} phases
- {Y} tasks
- {Z} subtasks (2-4 hours each)

### Step 2: Begin Implementation

```bash
/execute 1
```

**What happens:**
1. /execute detects task-manager/ structure
2. Reads phase-1-*/ task files
3. Uses subtasks as implementation checklist
4. Validates against success criteria
5. Updates this README as tasks complete

### Step 3: Continue Through Phases

After each phase:
- Context compact
- `/execute {N+1}` for next phase
- Repeat until all phases complete

---

## Task File Structure

Each `task-{N}.{M}-{name}.md` file contains:

```markdown
# Task {N}.{M}: {Name}

**Dependencies:** What must be complete first
**Success Criteria:** Measurable outcomes
**Research References:** ADRs and docs to consult
**Test Specifications:** Which tests to create
**Subtasks:** 2-4 hour actionable chunks
```

**The /execute command reads all of this to guide implementation.**

---

## Progress Tracking

**Master Progress:** `task-manager/README.md`
- Updated by /execute after each phase
- Shows completion percentages
- Tracks timeline vs. planned

**Phase Progress:** `task-manager/phase-{N}-*/README.md`
- Shows task completion within phase
- Lists all subtasks

**Task Progress:** Individual task files
- Checkbox subtasks (can manually track)

---

## Benefits of This Integration

**Without task-manager/:**
- Read large IMPLEMENTATION.md (3,500+ lines)
- Manually track what's done
- No granular progress visibility

**With task-manager/:**
- ✅ Focused task files (150-300 lines each)
- ✅ Automated progress tracking
- ✅ Subtask-level visibility
- ✅ Explicit dependencies
- ✅ Research references at task level
- ✅ Success criteria validation

---

## Next Steps

**Ready to begin?**

```bash
/execute 1
```

**Questions?**
- See: workflow/commands/execute.md (command documentation)
- See: task-manager/README.md (master progress)
- See: phase-1-*/README.md (phase overview)
```

---

## Summary: Workflow After Updates

### User Experience (After Updates)

1. **Create large implementation guide:**
   ```bash
   # User has IMPLEMENTATION.md (3,539 lines, 7 weeks)
   ```

2. **Break it down:**
   ```bash
   /breakdown IMPLEMENTATION.md ui-ux-enhancements
   # Creates task-manager/ with 14 tasks, 42 subtasks
   # Outputs: "Ready to start Phase 1? Run: /execute 1"
   ```

3. **Implement Phase 1:**
   ```bash
   /execute 1
   # Detects task-manager/ automatically
   # Reads phase-1-*/ task files
   # Shows: "Phase 1 has 3 tasks with 8 subtasks"
   # Guides through implementation using task structure
   # Updates task-manager/README.md with progress
   ```

4. **Compact and continue:**
   ```bash
   # Context compact
   /execute 2
   # Reads phase-2-*/ task files
   # Continues with Phase 2
   ```

5. **Complete all phases:**
   ```bash
   # After all phases: task-manager/README.md shows 100% complete
   ```

---

## Integration Quality Metrics

**After these updates:**

✅ **Seamless Handoff**
- /breakdown final message says: "Run: /execute 1"
- /execute Step 0 detects task-manager/ automatically
- No manual file discovery needed

✅ **Full Utilization**
- All task file data used (dependencies, success criteria, subtasks)
- Research references consumed during implementation
- Test specifications drive test generation

✅ **Progress Synchronization**
- task-manager/README.md updated by /execute
- Master progress always current
- Phase completion visible in real-time

✅ **Subtask Tracking**
- /execute uses subtasks as implementation checklist
- TodoWrite integration for granular tracking
- 2-4 hour chunks enable handoff-friendly workflow

✅ **Success Validation**
- /execute validates against task success criteria (Step 10)
- Measurable outcomes confirmed before marking complete
- Quality gates enforced

---

## Files to Update

**1. workflow/commands/execute.md**
- Add Step 0 (Check for task-manager/)
- Update Step 2 (Use task files if available)
- Update Step 10 (Update master README progress)

**2. ~/.claude/commands/breakdown.md**
- Update Phase 5 final message (mention /execute)
- Add handoff section to master README
- Create INTEGRATION-GUIDE.md automatically

**3. Documentation**
- Update CLAUDE.md (both global and project)
- Update Claude-Commands README.md
- Create this integration analysis document

---

## Success Criteria for Integration

**The integration is successful when:**

✅ User runs /breakdown → Gets message: "Run: /execute 1"
✅ User runs /execute 1 → Automatically detects and uses task-manager/
✅ /execute shows: "Phase 1 has X tasks with Y subtasks (from task-manager/)"
✅ /execute guides through subtasks as implementation checklist
✅ /execute updates task-manager/README.md after each phase
✅ No manual file discovery or navigation needed
✅ Complete workflow: /breakdown → /execute → completion

---

## Timeline for Updates

**Estimated effort:** 2-3 hours

1. **Update /execute command** (1.5 hours)
   - Add Step 0 detection logic
   - Update Step 2 task file reading
   - Update Step 10 progress tracking

2. **Update /breakdown command** (45 min)
   - Update Phase 5 completion message
   - Add INTEGRATION-GUIDE.md generation

3. **Testing** (30 min)
   - Run /breakdown on ui-ux-enhancements
   - Verify /execute detects structure
   - Confirm progress tracking works

4. **Documentation** (15 min)
   - Update CLAUDE.md files
   - Commit changes

---

## Conclusion

**Current State:** Two powerful commands with strong alignment but no explicit handoff.

**Proposed State:** Seamless workflow where /breakdown → /execute is automatic and integrated.

**Impact:** Enables systematic task breakdown and execution for any multi-phase project.

**Next Action:** Update both command files as specified above.

---

**Created:** 2025-10-21
**Status:** Analysis Complete | Ready for Implementation
**Author:** Claude Code Workflow Integration Analysis
