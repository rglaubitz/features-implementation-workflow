# Execute Phase Implementation

**Command:** `/execute [phase-number]`
**Purpose:** Systematic implementation using task-manager structure
**Workflow:** Lean 5-step pattern (Load → Execute → Validate → Track → Next)

---

## Prerequisites

Before running `/execute`:

- ✅ `/breakdown` completed (task-manager/ structure exists)
- ✅ All previous phase dependencies met
- ✅ Development environment ready (services running)

**If task-manager/ not found:** Error - Run `/breakdown IMPLEMENTATION.md [project-name]` first

---

## Workflow Overview

The lean 5-step execution pattern:

```
Step 1: Load Task Context (30 sec)
   └─ Auto-read phase tasks, show checklist

Step 2: Execute Subtasks Interactively (varies)
   └─ Work through subtasks with quality standards

Step 3: Validate Implementation (5-10 min)
   └─ Run tests, verify success criteria (BLOCKING quality gate)

Step 4: Track Progress (10 sec)
   └─ Auto-update task-manager/ READMEs

Step 5: Next Action (instant)
   └─ Show next task, recommend compacts
```

**Total overhead per phase:** ~10 minutes (vs 30+ minutes in legacy workflow)

---

## Step 1: Load Task Context 📂

**Auto-detect task-manager/ structure and load phase tasks.**

### Detection

Check for `task-manager/` directory in current project:

```bash
if [ -d "task-manager/" ]; then
    echo "✅ Task Manager structure detected"
    TASK_MANAGER_MODE=true
else
    echo "❌ No task-manager/ found"
    echo "   Run: /breakdown IMPLEMENTATION.md [project-name]"
    exit 1
fi
```

### Load Phase Tasks

**Read these files automatically:**

1. **Master README** - `task-manager/README.md`
   - Overall project progress
   - All phases with completion status

2. **Phase Overview** - `task-manager/phase-{N}-*/README.md`
   - Current phase summary
   - All tasks for this phase
   - Phase dependencies

3. **Task Files** - `task-manager/phase-{N}-*/task-{N}.{M}-*.md`
   - Detailed task breakdown
   - Subtasks (2-4 hour actionable chunks)
   - Dependencies (what must be complete first)
   - Success criteria (measurable outcomes)
   - Research references (ADRs, docs with line numbers)
   - Test specifications (exact tests to create)

### Display Context

**Announce loaded context:**

```
📂 TASK CONTEXT LOADED

Phase {N}: {Phase Name}
Duration: {X} weeks
Status: {Current status}

Tasks for this phase:
├─ Task {N}.1: {Name} ({Duration}, {Y} tests)
│  ├─ Subtask {N}.1.1: {Name} (4 hours)
│  ├─ Subtask {N}.1.2: {Name} (6 hours)
│  ├─ Subtask {N}.1.3: {Name} (6 hours)
│  └─ Subtask {N}.1.4: {Name} (4 hours)
│
├─ Task {N}.2: {Name} ({Duration}, {Z} tests)
│  ├─ Subtask {N}.2.1: {Name} (4 hours)
│  └─ ...
│
└─ ... (all tasks for phase)

Phase Totals:
  - Tasks: {X}
  - Subtasks: {Y}
  - Tests: {Z}
  - Estimated Duration: {N} weeks

Research References:
  - ADR-00{X}: {Title} (referenced in Task {N}.{M})
  - research/documentation/{topic}.md (lines {X}-{Y})

Dependencies Verified:
  ✓ {Dependency 1} (Phase {N-1} complete)
  ✓ {Dependency 2} ({Service} running)

✓ All task files loaded
✓ Research references extracted
✓ Test specifications identified
✓ Ready to implement
```

### Quality Gate

**Verify before proceeding:**

- ✅ task-manager/ structure exists and is valid
- ✅ All phase task files are readable
- ✅ Dependencies from previous phases are met
- ✅ Success criteria are clearly defined
- ✅ Research references are accessible

**NO REDUNDANT PLANNING** - Just load and display what `/breakdown` already documented.

**Time:** ~30 seconds (automated file reading)

---

## Step 2: Execute Subtasks Interactively 💻

**Work through subtasks systematically with quality standards.**

### Task Execution Loop

**For each task in the phase:**

#### Display Current Task

```
═══════════════════════════════════════════════════════════
Task {N}.{M}: {Task Name}
═══════════════════════════════════════════════════════════

Duration: {X} hours
Tests: {Y} specifications
Status: ⬜ Not Started

Dependencies:
  {List dependencies or "None - ready to start"}

Success Criteria:
  1. {Criterion 1} (measurable outcome)
  2. {Criterion 2} (measurable outcome)
  3. {Criterion 3} (measurable outcome)
  ...

Research References:
  - {ADR or doc} (lines {X}-{Y}) - {Why relevant}
  - {ADR or doc} (lines {A}-{B}) - {Why relevant}

Subtasks:
  ⬜ {N}.{M}.1: {Name} (4 hours)
  ⬜ {N}.{M}.2: {Name} (6 hours)
  ⬜ {N}.{M}.3: {Name} (6 hours)
  ⬜ {N}.{M}.4: {Name} (4 hours)
```

### Subtask Execution

**For each subtask in the task:**

#### 1. Display Subtask Details

```
─────────────────────────────────────────────────────────
Subtask {N}.{M}.{S}: {Name}
─────────────────────────────────────────────────────────

Duration: {X} hours
Status: ⬜ Not Started

Implementation Steps:
  {Copy steps directly from task file}

Files to Create/Modify:
  {List from task file}

Code Examples:
  {Reference to IMPLEMENTATION.md sections via task file}

Validation Commands:
  {Commands from task file to verify this subtask}
```

#### 2. Implement the Code

**Quality Standards (Applied Automatically):**

**Code Quality:**
- ✅ Type hints everywhere (`def func(x: int) -> str:`)
- ✅ Google-style docstrings for all classes/functions
- ✅ Async/await where appropriate
- ✅ Structured logging (`logger.info()`, not `print()`)
- ✅ Proper error handling (specific exceptions, try/except)
- ✅ No TODO/FIXME in production code

**Code Pattern:**
```python
"""Module-level docstring explaining purpose.

Author: Apex Infrastructure Team
Created: {YYYY-MM-DD}
"""

import logging
from typing import List, Dict, Any, Optional

logger = logging.getLogger(__name__)


class ComponentName:
    """Component description.

    This component handles {what it does}.

    Args:
        param1: Description.
        param2: Description.

    Examples:
        >>> component = ComponentName()
        >>> result = await component.method()
    """

    def __init__(self, param1: str, param2: Optional[int] = None):
        """Initialize component."""
        self.param1 = param1
        self.param2 = param2
        logger.info(f"Initialized {self.__class__.__name__}")

    async def method(self) -> Dict[str, Any]:
        """Method description.

        Returns:
            Dictionary with results.

        Raises:
            ValueError: If validation fails.
        """
        try:
            # Implementation
            result = await self._internal_method()
            logger.info(f"Method completed successfully")
            return result
        except Exception as e:
            logger.error(f"Method failed: {e}")
            raise
```

**File Organization:**
- ✅ Modular design (200-500 lines per file)
- ✅ Clear imports and dependencies
- ✅ Logical file structure (group related functionality)

#### 3. Announce Progress

```
📝 Implementing Subtask {N}.{M}.{S}...

Creating/Modifying:
  - {File 1} ({NEW/MODIFY}) - {Purpose}
  - {File 2} ({NEW/MODIFY}) - {Purpose}

Lines: ~{Estimated lines}
```

#### 4. Validate Subtask

**Run validation commands from task file:**

```bash
# Example validation commands
alembic upgrade head                    # Database migration
python -c "from module import Class"    # Import verification
curl http://localhost:8000/endpoint     # API endpoint check
```

**Show results:**

```
Validation Results:
  ✓ {Validation 1} passed
  ✓ {Validation 2} passed
  ✓ {Validation 3} passed
```

#### 5. Mark Subtask Complete

```
✅ Subtask {N}.{M}.{S} Complete

Delivered:
  ✓ {File 1} created ({X} lines)
  ✓ {File 2} updated (+{Y} lines)
  ✓ All validations passed

Time: {Actual time spent}
```

### Task Progress Tracking

**Show continuous progress:**

```
Task {N}.{M} Progress:
  ├─ Subtasks: {S}/{TOTAL} complete ({XX}%)
  ├─ Estimated remaining: {X} hours
  └─ Status: {On Track / Ahead / Behind}
```

**When all subtasks complete, proceed to Step 3 (Validate Implementation).**

**NO REDUNDANT DISCUSSION** - Just execute what's documented in subtask steps.

**Time:** Varies by subtask complexity (actual implementation work)

---

## Step 3: Validate Implementation ✅

**Run tests and verify success criteria - THIS IS A BLOCKING QUALITY GATE.**

### Automatic Test Generation

**Generate tests proactively (WITHOUT being asked):**

After implementing each task, IMMEDIATELY create comprehensive tests.

#### Test Structure

```python
# File: tests/unit/test_{component}.py (NEW)

"""Unit tests for {component}.

Tests verify:
- Core functionality
- Edge cases
- Error handling
- Integration points

Test Specifications: TESTING.md lines {X}-{Y}

Author: Apex Infrastructure Team
Created: {YYYY-MM-DD}
"""

import pytest
from unittest.mock import Mock, AsyncMock, patch

from apex_memory.{module} import ComponentName


@pytest.fixture
def component():
    """Fixture providing test component instance."""
    return ComponentName(param1="test-value")


@pytest.mark.asyncio
async def test_core_functionality(component):
    """Test primary use case.

    Validates: {Success criterion from task file}
    """
    result = await component.method()

    assert result is not None
    assert result["status"] == "success"


@pytest.mark.asyncio
async def test_edge_case_empty_input(component):
    """Test handling of empty input.

    Validates: Edge case from TESTING.md line {X}
    """
    result = await component.method_with_input("")

    assert result["status"] == "skipped"


@pytest.mark.asyncio
async def test_error_handling(component):
    """Test error handling for invalid input.

    Validates: Error handling requirement
    """
    with pytest.raises(ValueError):
        await component.method_with_validation("invalid")


@pytest.mark.asyncio
async def test_integration_with_external_service(component):
    """Test integration with external service.

    Validates: Integration point from task dependencies
    """
    with patch("apex_memory.external.service_call") as mock_service:
        mock_service.return_value = {"data": "test"}

        result = await component.call_external_service()

        assert result["data"] == "test"
        mock_service.assert_called_once()
```

**Announce test creation:**

```
✨ Generating tests for Task {N}.{M}...

Test File: tests/unit/test_{component}.py (NEW)
Test Count: {Y} tests
Scenarios:
  - Core functionality ({X} tests)
  - Edge cases ({Y} tests)
  - Error handling ({Z} tests)
  - Integration points ({A} tests)

Coverage Target: 80%+
```

### Run Test Suite

**Execute tests for this task:**

```bash
# Run tests
pytest tests/unit/test_{component}.py -v

# Check coverage
pytest tests/unit/test_{component}.py \
  --cov=apex_memory.{module} \
  --cov-report=term \
  --cov-report=html
```

**Display results:**

```
Running tests for Task {N}.{M}...

Test Results:
  ✓ test_core_functionality PASSED
  ✓ test_edge_case_empty_input PASSED
  ✓ test_error_handling PASSED
  ✓ test_integration_with_external_service PASSED
  ... (all tests)

Summary:
  ✓ {Y}/{Y} tests passing (100%)
  ✓ Coverage: {X}% (target: 80%+)
  ✓ No failures or errors
```

### Verify Success Criteria

**Check each criterion from task file:**

```
Verifying Task {N}.{M} success criteria:

From task file:
  1. {Criterion 1}
     ✓ Verified: {How verified}

  2. {Criterion 2}
     ✓ Verified: {How verified}

  3. {Criterion 3}
     ✓ Verified: {How verified}

  ... (all criteria)

All success criteria met: ✅
```

### Quality Gate (BLOCKING)

**This gate BLOCKS progression if not met.**

#### If Tests Fail or Criteria Not Met:

```
⚠️  QUALITY GATE FAILED

Cannot proceed to next task until issues resolved.

Issues Found:
  ❌ test_{name} FAILED
     Error: {Error message}
     Fix required: {Suggested fix}

  ❌ Success criterion "{Criterion}" NOT MET
     Expected: {Expected state}
     Actual: {Actual state}
     Fix required: {Suggested fix}

Actions Required:
  1. Fix failing tests
  2. Verify all success criteria
  3. Re-run validation (Step 3)

Do NOT proceed until quality gate passes.
```

**User must fix issues and validation must pass before continuing.**

#### If All Pass:

```
✅ QUALITY GATE PASSED

Task {N}.{M}: {Task Name}

Validation Results:
  ✓ All success criteria met ({X}/{X})
  ✓ All tests passing ({Y}/{Y})
  ✓ Code coverage: {Z}% (≥80% target)
  ✓ No errors or warnings

Implementation Quality:
  ✓ Type hints complete
  ✓ Docstrings complete
  ✓ Error handling implemented
  ✓ Logging structured
  ✓ No TODO/FIXME in production code

Ready to mark Task {N}.{M} complete and update progress.

Proceeding to Step 4...
```

**ENFORCES QUALITY** - Cannot skip failing tests or incomplete success criteria.

**Time:** 5-10 minutes per task (automated testing + verification)

---

## Step 4: Track Progress 📊

**Automatically update task-manager/ structure with completion status.**

### Update Task File

**File:** `task-manager/phase-{N}-*/task-{N}.{M}-*.md`

**Update header:**
```markdown
**Status:** ✅ Complete
**Completed:** {YYYY-MM-DD}
**Actual Duration:** {X} hours (estimated: {Y} hours)
```

**Update progress tracking section:**
```markdown
## Progress Tracking

**Subtasks:** 4/4 complete (100%)

- [x] Subtask {N}.{M}.1: {Name} ✅ ({Completion date})
- [x] Subtask {N}.{M}.2: {Name} ✅ ({Completion date})
- [x] Subtask {N}.{M}.3: {Name} ✅ ({Completion date})
- [x] Subtask {N}.{M}.4: {Name} ✅ ({Completion date})

**Tests:** {Y}/{Y} passing (100%)
**Success Criteria:** {X}/{X} met (100%)
```

### Update Phase README

**File:** `task-manager/phase-{N}-*/README.md`

**Update task table:**
```markdown
| Task | Name | Status | Duration | Tests | Subtasks |
|------|------|--------|----------|-------|----------|
| {N}.1 | {Name} | ✅ | 2 days | 10/10 | 4/4 |
| {N}.2 | {Name} | ⬜ | 1 day | 0/6 | 0/4 |
| {N}.3 | {Name} | ⬜ | 1 day | 0/4 | 0/4 |
```

**Update totals:**
```markdown
**Totals:**
- Tasks: 1/4 complete (25%)
- Subtasks: 4/16 complete (25%)
- Tests: 10/42 passing (24%)
```

### Update Master README

**File:** `task-manager/README.md`

**Update progress table:**
```markdown
| Phase | Name | Tasks | Subtasks | Tests | Status | Progress |
|-------|------|-------|----------|-------|--------|----------|
| {N} | {Phase Name} | 1/4 | 4/16 | 10/42 | 🔄 | 25% |
```

**Update overall progress:**
```markdown
**Overall Progress:** {X}/23 tasks ({Y}%) | {A}/89 subtasks ({B}%)
```

### Display Update Summary

```
📊 PROGRESS UPDATED

Task {N}.{M} Complete:
  ✓ 4/4 subtasks done
  ✓ {Y}/{Y} tests passing (100%)
  ✓ All success criteria met
  ✓ Completed: {YYYY-MM-DD}
  ✓ Duration: {X} hours (estimated: {Y} hours)

Files Updated:
  ✓ task-manager/phase-{N}-*/task-{N}.{M}-*.md
  ✓ task-manager/phase-{N}-*/README.md
  ✓ task-manager/README.md

Phase {N} Progress:
  ├─ Tasks: {X}/{TOTAL} complete ({Y}%)
  ├─ Subtasks: {A}/{TOTAL} complete ({B}%)
  └─ Tests: {C}/{TOTAL} passing ({D}%)

Overall Project Progress:
  ├─ Tasks: {E}/23 complete ({F}%)
  ├─ Subtasks: {G}/89 complete ({H}%)
  └─ Tests: {I}/107 passing ({J}%)

Estimated Remaining: {X} hours this phase, {Y} hours total
```

**FULLY AUTOMATED** - No manual README editing required.

**Time:** ~10 seconds (automated file updates)

---

## Step 5: Next Action 🎯

**Provide clear guidance on what to do next.**

### Determine Next Action

**Three possible states:**

1. **More tasks in current phase** → Continue to next task
2. **Phase complete** → Recommend context compact
3. **Project complete** → Celebrate and prepare deployment

### State 1: More Tasks in Phase

**If tasks remaining in current phase:**

```
═══════════════════════════════════════════════════════════
NEXT TASK
═══════════════════════════════════════════════════════════

Task {N}.{M+1}: {Task Name}

Duration: {X} hours
Tests: {Y} tests to create
Dependencies:
  ✓ Task {N}.{M} (Complete)
  {Other dependencies if any}

Subtasks:
  ⬜ {N}.{M+1}.1: {Name} (4 hours)
  ⬜ {N}.{M+1}.2: {Name} (6 hours)
  ⬜ {N}.{M+1}.3: {Name} (3 hours)
  ⬜ {N}.{M+1}.4: {Name} (2 hours)

Phase {N} Progress: {X}/{TOTAL} tasks ({Y}%)
Estimated Remaining: {Z} hours

Ready to continue? Proceeding to Step 2 for next task...
```

**Auto-proceed to Step 2 (Execute Subtasks) for next task.**

### State 2: Phase Complete

**If all tasks in phase are done:**

```
🎉 PHASE {N} COMPLETE!

══════════════════════════════════════════════════════════
PHASE COMPLETION SUMMARY
══════════════════════════════════════════════════════════

Phase {N}: {Phase Name}
Duration: {X} weeks (estimated: {Y} weeks)
Status: ✅ COMPLETE

Tasks Completed:
  ✅ Task {N}.1: {Name} ({Duration}, {Tests} tests)
  ✅ Task {N}.2: {Name} ({Duration}, {Tests} tests)
  ✅ Task {N}.3: {Name} ({Duration}, {Tests} tests)
  ✅ Task {N}.4: {Name} ({Duration}, {Tests} tests)

Deliverables:
  ✓ {X} implementation files created/modified
  ✓ {Y} lines of code written
  ✓ {Z} tests created (100% passing)
  ✓ {A} research references used
  ✓ All success criteria met

Quality Metrics:
  ✓ Test coverage: {X}% (≥80% target)
  ✓ Code quality: All standards met
  ✓ Documentation: 100% complete
  ✓ No TODO/FIXME in production code

══════════════════════════════════════════════════════════

⚠️  RECOMMENDED: Context Compact

Why compact now:
  - Phase {N} complete ({X} tasks, {Y} subtasks)
  - ~{Z} hours of implementation discussion
  - Next phase: {A} tasks, ~{B} hours of new work
  - Estimated conversation size: {C}k tokens

What gets preserved:
  ✓ All code files created
  ✓ All tests and validation results
  ✓ Progress in task-manager/ (all READMEs updated)
  ✓ Phase completion status
  ✓ Critical architectural decisions

What gets summarized:
  - Step-by-step implementation details
  - Code generation discussions
  - Test creation iterations
  - Debugging sessions

Resume Command After Compact:
  /execute {N+1}

Options:
  1. /compact (RECOMMENDED - cleaner context for next phase)
  2. /execute {N+1} (continue without compact)
  3. Take a break (checkpoint saved, can resume anytime)

Current state saved in task-manager/ - safe to compact or pause.
```

### State 3: Project Complete

**If all phases are done:**

```
🏆 PROJECT COMPLETE! 🏆

══════════════════════════════════════════════════════════
{PROJECT NAME} - IMPLEMENTATION COMPLETE
══════════════════════════════════════════════════════════

All {TOTAL} phases completed successfully!

Phase Summary:
  ✅ Phase 1: {Name} ({X} tasks, {Y} tests)
  ✅ Phase 2: {Name} ({A} tasks, {B} tests)
  ✅ Phase 3: {Name} ({C} tasks, {D} tests)
  ... (all phases)

Final Statistics:
  ✓ Tasks: {X}/{X} complete (100%)
  ✓ Subtasks: {Y}/{Y} complete (100%)
  ✓ Tests: {Z}/{Z} passing (100%)
  ✓ Files: {A} implementation files
  ✓ Lines: ~{B} lines of code
  ✓ Duration: {C} weeks (estimated: {D} weeks)

Quality Achievements:
  ✓ 100% test pass rate
  ✓ {X}% code coverage (≥80% target)
  ✓ Zero TODO/FIXME in production code
  ✓ Complete documentation
  ✓ All examples working

Next Steps:
  1. Review TESTING.md - Run full test suite
  2. Review DEPLOYMENT-GUIDE.md - Prepare deployment
  3. Run production readiness checklist
  4. Deploy to staging environment
  5. User acceptance testing
  6. Production deployment

Congratulations! Ready for deployment. 🚀
```

### Smart Compact Recommendations

**Automatically suggest context compact based on:**

**Triggers:**
- ✅ Each phase complete (natural break point)
- ✅ Before starting tasks >16 hours (multi-day work)
- ✅ When conversation >150k tokens (approaching limit)

**Compact Timing Example:**
```
💡 Smart Compact Recommendation

Compact suggested because:
  - Phase {N} complete (natural checkpoint)
  - {X} hours of detailed implementation work
  - Conversation size: ~{Y}k tokens
  - Next phase: New features, different focus area

Benefits of compacting now:
  ✓ Cleaner context for Phase {N+1}
  ✓ Faster Claude responses
  ✓ Better focus on new work
  ✓ All progress preserved in task-manager/

Checkpoint saved: phase-{N}-complete
Resume command: /execute {N+1}

Safe to compact - all state preserved in files.
```

### Create Checkpoint

**Before any potential compact or break:**

```
Checkpoint Saved: phase-{N}-complete

Current State:
  - Phase {N}: ✅ Complete ({X}/{X} tasks)
  - Overall: {Y}/23 tasks ({Z}%)
  - Next: Phase {N+1} ({A} tasks, ~{B} hours)

Resume Command:
  /execute {N+1}

All progress saved in:
  ✓ task-manager/README.md (master progress)
  ✓ task-manager/phase-{N}-*/README.md (phase complete)
  ✓ task-manager/phase-{N}-*/task-*.md (all tasks)

Safe to:
  - Take a break
  - Compact context
  - Switch projects

Can resume anytime with /execute {N+1}
```

**ALWAYS ORIENTED** - Developer always knows what's next, when to compact, how to resume.

**Time:** Instant (guidance display only)

---

## Quick Reference

### Command Usage

```bash
# Auto-detect next phase
/execute

# Execute specific phase
/execute 1        # Phase 1
/execute 2        # Phase 2
/execute 3        # Phase 3
```

### Prerequisites Checklist

Before running `/execute [phase]`:

```
☑ /breakdown completed (task-manager/ exists)
☑ Previous phases complete (check dependencies)
☑ Development environment ready
  ☑ Services running (databases, APIs, etc.)
  ☑ Dependencies installed
  ☑ Environment variables configured
☑ Tests from previous phases still passing
```

### The 5-Step Workflow

```
1. LOAD (30 sec)
   └─ Read task files → Show checklist

2. EXECUTE (varies)
   └─ Implement subtasks → Quality code

3. VALIDATE (5-10 min)
   └─ Generate tests → Verify criteria → BLOCKING GATE

4. TRACK (10 sec)
   └─ Update READMEs → Show progress

5. NEXT (instant)
   └─ Show next task → Recommend compact → Save checkpoint
```

### Quality Standards

**Code Quality (Automatically Applied):**
- ✅ Type hints everywhere
- ✅ Google-style docstrings
- ✅ Async/await where appropriate
- ✅ Structured logging (no print statements)
- ✅ Proper error handling (specific exceptions)
- ✅ No TODO/FIXME in production code

**Testing Standards:**
- ✅ Tests generated proactively (without asking)
- ✅ Unit tests (component isolation)
- ✅ Integration tests (component interaction)
- ✅ Edge cases (boundary conditions)
- ✅ Error tests (exception handling)
- ✅ Coverage ≥80% target
- ✅ 100% test pass rate (blocking gate)

**Progress Tracking:**
- ✅ Fully automated README updates
- ✅ Real-time progress metrics
- ✅ Estimated time remaining
- ✅ Checkpoint saves for safe resumption

### Time Estimates

**Per Phase:**
- Setup: ~30 seconds (Step 1)
- Implementation: Varies (Step 2 - actual coding)
- Validation: ~5-10 minutes per task (Step 3)
- Progress tracking: ~10 seconds (Step 4)
- Next action: Instant (Step 5)

**Total Overhead:** ~10 minutes per phase (vs 30+ minutes in legacy workflow)

### Success Metrics

**What This Workflow Delivers:**
- ✅ Zero redundant planning (trusts /breakdown)
- ✅ Quality enforced (cannot skip failing tests)
- ✅ Progress automated (no manual README updates)
- ✅ Always oriented (clear next steps)
- ✅ Context efficient (strategic compact reminders)
- ✅ Fast execution (30 sec setup vs 15-30 min)

---

## Validation Checkpoints

**Step 1 (Load):**
- [ ] task-manager/ structure detected
- [ ] All task files loaded successfully
- [ ] Dependencies verified
- [ ] Context displayed clearly

**Step 2 (Execute):**
- [ ] Subtasks executed in order
- [ ] Quality standards applied
- [ ] Code follows patterns
- [ ] Validation commands pass

**Step 3 (Validate):**
- [ ] Tests generated proactively
- [ ] All tests passing (100%)
- [ ] Success criteria met
- [ ] Quality gate enforced

**Step 4 (Track):**
- [ ] Task file updated (status, completion date)
- [ ] Phase README updated (task table, totals)
- [ ] Master README updated (progress, overall stats)
- [ ] Progress displayed accurately

**Step 5 (Next):**
- [ ] Next action clear
- [ ] Compact recommended at right time
- [ ] Checkpoint saved
- [ ] Resume command provided

---

**This workflow implements the lean execution pattern that complements /breakdown with zero redundancy and maximum efficiency.**
