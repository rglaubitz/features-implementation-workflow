# Issues Management - Command Reference

**Purpose:** Complete reference for all issues management slash commands.

---

## Command Overview

| Command | Purpose | Input | Output |
|---------|---------|-------|--------|
| `/new-issue` | Create new issue | Title | ISSUE-NNN.md in new-issue-context/ |
| `/diagnose` | Diagnose problem | ISSUE-NNN | DIAGNOSIS.md in problem-identified/ |
| `/propose-solution` | Design solution | ISSUE-NNN | SOLUTION.md in solution-identified/ |
| `/test-ready` | Begin testing | ISSUE-NNN | TESTING.md in needs-tested/ |
| `/archive-issue` | Archive resolved | ISSUE-NNN | Moved to archived/YYYY-MM/ |

---

## `/new-issue <title>`

### Purpose
Create a new issue from template with auto-incrementing issue ID.

### Usage
```
/new-issue "Cache system crashes on repeated queries"
```

### What It Does
1. Find next available ISSUE-NNN number
2. Create slug from title: "cache-system-crashes"
3. Copy `1-NEW-ISSUE-TEMPLATE.md` → `ISSUE-NNN-slug.md`
4. Fill in metadata (ID, date, etc.)
5. Save to `issues/new-issue-context/`
6. Open file for editing

### Output
```
✅ Created: issues/new-issue-context/ISSUE-009-cache-crashes.md
📝 Please fill in:
   - Severity (P0-P3)
   - Symptoms
   - Steps to reproduce
   - Expected vs actual behavior

Next step: /diagnose ISSUE-009
```

### Parameters
- **title** (required): Short description of issue
  - Format: Plain text, 3-100 characters
  - Example: "Cache crashes on repeated queries"

---

## `/diagnose ISSUE-NNN`

### Purpose
Guide through systematic diagnosis using mandatory checklist.

### Usage
```
/diagnose ISSUE-009
```

### What It Does
1. Read `new-issue-context/ISSUE-NNN-*.md`
2. Create `2-DIAGNOSIS-TEMPLATE.md` copy
3. Guide through **5-step mandatory checklist**:
   - ✅ Step 1: Code review (grep, read files, map dependencies)
   - ✅ Step 2: Error analysis (stack trace, error handling)
   - ✅ Step 3: Reproduction (verify issue, isolate minimal case)
   - ✅ Step 4: Impact analysis (direct + cascading effects)
   - ✅ Step 5: Root cause (primary + contributing factors)
4. Fill in diagnosis results
5. Move files to `problem-identified/`

### Output
```
✅ Diagnosis complete!
📊 Results:
   - Root cause: No error handling in cache operations
   - Files affected: router.py:563, cache.py:105
   - Impact: All queries crash if cache fails
   - Severity: P0 (confirmed)

Created:
   - issues/problem-identified/ISSUE-009-CONTEXT.md
   - issues/problem-identified/ISSUE-009-DIAGNOSIS.md

Next step: /propose-solution ISSUE-009
```

### Parameters
- **ISSUE-NNN** (required): Issue ID
  - Format: ISSUE-001, ISSUE-009, etc.
  - Must exist in `new-issue-context/`

### Checklist Enforcement
❌ **Will not proceed without:**
- Reading all affected files
- Mapping dependencies
- Reproducing issue
- Identifying root cause

---

## `/propose-solution ISSUE-NNN`

### Purpose
Design solution with implementation plan and rollback strategy.

### Usage
```
/propose-solution ISSUE-009
```

### What It Does
1. Read `problem-identified/ISSUE-NNN-DIAGNOSIS.md`
2. Create `3-SOLUTION-TEMPLATE.md` copy
3. Guide through **5-step mandatory checklist**:
   - ✅ Step 1: Solution design (evaluate 2-3 options)
   - ✅ Step 2: Implementation plan (exact file changes)
   - ✅ Step 3: Testing strategy (unit + integration + regression)
   - ✅ Step 4: Rollback plan (safety net)
   - ✅ Step 5: Documentation (code comments + docs)
4. Fill in solution proposal
5. Move files to `solution-identified/`

### Output
```
✅ Solution proposal complete!
💡 Recommended approach: Add try-catch to cache operations

📋 Implementation plan:
   - Modify router.py:563-605 (cache read)
   - Modify router.py:735-786 (cache write)
   - Add 2 unit tests
   - No breaking changes

🔄 Rollback: git revert (backwards compatible)

Created:
   - issues/solution-identified/ISSUE-009-DIAGNOSIS.md
   - issues/solution-identified/ISSUE-009-SOLUTION.md

Next step: /test-ready ISSUE-009
```

### Parameters
- **ISSUE-NNN** (required): Issue ID
  - Must exist in `problem-identified/`

### Options Evaluation
**Requires evaluating multiple approaches:**
- Option 1: {recommended}
- Option 2: {alternative}
- Option 3: {fallback}

---

## `/test-ready ISSUE-NNN`

### Purpose
Implement solution and validate through comprehensive testing.

### Usage
```
/test-ready ISSUE-009
```

### What It Does
1. Read all previous files (context, diagnosis, solution)
2. Create `4-TESTING-TEMPLATE.md` copy
3. Guide through **9-phase mandatory checklist**:
   - ✅ Phase 1: Pre-implementation review
   - ✅ Phase 2: Implementation (follow plan)
   - ✅ Phase 3: Unit testing
   - ✅ Phase 4: Integration testing
   - ✅ Phase 5: Regression testing
   - ✅ Phase 6: Performance testing
   - ✅ Phase 7: Code quality (format, lint, type check)
   - ✅ Phase 8: Documentation
   - ✅ Phase 9: Commit
4. Execute implementation
5. Run all tests
6. Create commit
7. Move files to `needs-tested/`

### Output
```
✅ Implementation and testing complete!

🧪 Test results:
   - Unit tests: 2/2 passed
   - Integration tests: 1/1 passed
   - Regression tests: 121/121 passed
   - No performance impact

📝 Commit: abc123
   Files changed: 2
   Lines added: 91
   Lines removed: 47

Created:
   - issues/needs-tested/ISSUE-009-CONTEXT.md
   - issues/needs-tested/ISSUE-009-DIAGNOSIS.md
   - issues/needs-tested/ISSUE-009-SOLUTION.md
   - issues/needs-tested/ISSUE-009-TESTING.md

Next step: /archive-issue ISSUE-009
```

### Parameters
- **ISSUE-NNN** (required): Issue ID
  - Must exist in `solution-identified/`

### Validation Gates
**Will not mark complete until:**
- Original issue verified fixed
- All tests pass (unit + integration + regression)
- Code quality checks pass
- Documentation updated
- Commit created

---

## `/archive-issue ISSUE-NNN`

### Purpose
Move resolved issue to archive with complete history.

### Usage
```
/archive-issue ISSUE-009
```

### What It Does
1. Read all files (context, diagnosis, solution, testing)
2. Verify resolution complete
3. Create `YYYY-MM` folder in archived/
4. Create `ISSUE-NNN-{slug}/` folder
5. Move all files to archive
6. Create `SUMMARY.md` with quick reference
7. Clean up previous folders

### Output
```
✅ Issue archived!

📁 Location: issues/archived/2025-10/ISSUE-009-cache-crashes/

📄 Files:
   - SUMMARY.md (quick reference)
   - CONTEXT.md (original issue)
   - DIAGNOSIS.md (root cause analysis)
   - SOLUTION.md (fix proposal)
   - TESTING.md (validation results)

🎯 Resolution:
   - Problem: Cache failures crashed system
   - Root cause: No error handling
   - Fix: Added try-catch blocks
   - Tests: 4 added, all passed
   - Commit: abc123

Issue ISSUE-009 is now complete and archived.
```

### Parameters
- **ISSUE-NNN** (required): Issue ID
  - Must exist in `needs-tested/`
  - Must have testing complete

### Archive Structure
```
archived/
└── 2025-10/
    └── ISSUE-009-cache-crashes/
        ├── SUMMARY.md          # Quick reference
        ├── CONTEXT.md          # Original issue
        ├── DIAGNOSIS.md        # Problem analysis
        ├── SOLUTION.md         # Fix proposal
        └── TESTING.md          # Validation results
```

---

## Workflow Example

### Complete Flow
```bash
# 1. Create new issue
/new-issue "Cache crashes on repeated queries"
# → Creates ISSUE-009 in new-issue-context/

# 2. Diagnose problem
/diagnose ISSUE-009
# → Guides through systematic diagnosis
# → Identifies root cause
# → Moves to problem-identified/

# 3. Propose solution
/propose-solution ISSUE-009
# → Evaluates multiple approaches
# → Creates implementation plan
# → Moves to solution-identified/

# 4. Implement and test
/test-ready ISSUE-009
# → Implements fix
# → Runs comprehensive tests
# → Creates commit
# → Moves to needs-tested/

# 5. Archive resolved issue
/archive-issue ISSUE-009
# → Verifies resolution
# → Archives with full history
# → Moves to archived/2025-10/
```

### Time Estimate
- New issue: 5-10 minutes
- Diagnosis: 30-60 minutes (depends on complexity)
- Solution: 15-30 minutes
- Implementation: 30-90 minutes (depends on complexity)
- Archive: 2-5 minutes

**Total:** 1.5 - 3 hours per issue (average)

---

## Error Handling

### Command Not Found
```
❌ Error: Issue ISSUE-999 not found in new-issue-context/

Did you mean:
- ISSUE-009: Cache crashes
- ISSUE-010: Query router slow

Usage: /diagnose ISSUE-NNN
```

### Invalid State
```
❌ Error: Cannot run /propose-solution on ISSUE-009
Issue is in: new-issue-context/
Required state: problem-identified/

Next step: /diagnose ISSUE-009
```

### Incomplete Checklist
```
❌ Error: Cannot proceed - checklist incomplete

Missing items:
- [ ] Step 1.1: Identify affected files
- [ ] Step 3.1: Reproduce original issue

Please complete all checklist items before proceeding.
```

---

## Best Practices

### Do's ✅
- Always complete full checklist (no skipping steps)
- Read all affected files (no assumptions)
- Test thoroughly (unit + integration + regression)
- Document decisions (why, not just what)
- Create detailed commit messages

### Don'ts ❌
- Don't skip diagnosis phase
- Don't assume root cause without evidence
- Don't modify code without impact analysis
- Don't commit without tests
- Don't archive without validation

---

**Command Reference Version:** 1.0
**Last Updated:** 2025-10-26
