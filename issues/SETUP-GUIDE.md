# Issues Management System - Setup Guide

**Complete guide for setting up the issues management system in any project.**

---

## Quick Setup (Any Project)

### Prerequisites
- Git repository
- Claude Code installed

### Setup Steps (5 minutes)

**1. Add workflow submodule:**
```bash
git submodule add https://github.com/rglaubitz/features-implementation-workflow.git workflow
git submodule update --init --recursive
```

**2. Copy slash commands:**
```bash
cp workflow/commands/{new-issue,diagnose,propose-solution,test-ready,archive-issue}.md .claude/commands/
```

**3. Create issues directory structure:**
```bash
mkdir -p issues/{new-issue-context,problem-identified,solution-identified,needs-tested,archived}
```

**4. Test the system:**
```bash
# In Claude Code:
/new-issue "Test issue - verify system works"
```

---

## How It Works

### Architecture

**Templates (Reusable - Lives in Workflow):**
```
workflow/
├── issues/
│   ├── README.md           # System overview
│   ├── COMMAND-REFERENCE.md # Complete command docs
│   └── templates/
│       ├── 1-NEW-ISSUE-TEMPLATE.md      # Issue context capture
│       ├── 2-DIAGNOSIS-TEMPLATE.md      # 5-step diagnosis checklist
│       ├── 3-SOLUTION-TEMPLATE.md       # Solution design + rollback
│       └── 4-TESTING-TEMPLATE.md        # 9-phase implementation
└── commands/
    ├── new-issue.md
    ├── diagnose.md
    ├── propose-solution.md
    ├── test-ready.md
    └── archive-issue.md
```

**Project Data (Your Issues):**
```
issues/
├── new-issue-context/      # New issues awaiting diagnosis
├── problem-identified/     # Diagnosed issues with root cause
├── solution-identified/    # Planned solutions with implementation plan
├── needs-tested/          # Implemented solutions awaiting validation
└── archived/              # Resolved issues organized by YYYY-MM
    └── 2025-10/
        └── ISSUE-001-brief-description/
            ├── SUMMARY.md
            ├── CONTEXT.md
            ├── DIAGNOSIS.md
            ├── SOLUTION.md
            └── TESTING.md
```

**Commands (Copied from Workflow):**
```
.claude/commands/
├── new-issue.md           # References workflow/issues/templates/1-NEW-ISSUE-TEMPLATE.md
├── diagnose.md            # References workflow/issues/templates/2-DIAGNOSIS-TEMPLATE.md
├── propose-solution.md    # References workflow/issues/templates/3-SOLUTION-TEMPLATE.md
├── test-ready.md          # References workflow/issues/templates/4-TESTING-TEMPLATE.md
└── archive-issue.md       # Creates archive with all history
```

---

## Complete Workflow Example

### 1. Create New Issue

```bash
/new-issue "Cache crashes on repeated queries"
```

**What happens:**
- Finds next available ISSUE-NNN (e.g., ISSUE-001)
- Copies `workflow/issues/templates/1-NEW-ISSUE-TEMPLATE.md`
- Creates slug from title: `cache-crashes-on-repeated-queries`
- Saves to: `issues/new-issue-context/ISSUE-001-cache-crashes.md`

**You fill in:**
- Severity (P0-P3)
- Symptoms observed
- Steps to reproduce
- Expected vs actual behavior
- Error messages/stack traces

---

### 2. Diagnose Issue

```bash
/diagnose ISSUE-001
```

**What happens:**
- Reads `issues/new-issue-context/ISSUE-001-cache-crashes.md`
- Loads `workflow/issues/templates/2-DIAGNOSIS-TEMPLATE.md`
- Guides through **5-step mandatory checklist**:

**Step 1: Code Review (REQUIRED)**
- Search codebase for keywords (Grep)
- List ALL affected files
- **READ EVERY FILE** (no assumptions!)
- Map dependencies (upstream + downstream)
- Check for similar patterns elsewhere

**Step 2: Error Analysis (REQUIRED)**
- Analyze full error message
- Identify error type
- Trace stack trace to origin
- Review error handling

**Step 3: Reproduction (REQUIRED)**
- Follow exact steps from context
- Reproduce the issue
- Isolate minimal case
- Test edge cases

**Step 4: Impact Analysis (REQUIRED)**
- Direct impact (what breaks)
- Cascading effects (secondary breakage)
- User impact
- Database/API changes

**Step 5: Root Cause Analysis (REQUIRED)**
- Identify THE ACTUAL BUG
- Contributing factors
- Why not caught earlier
- Check for similar past issues

**Output:**
- Creates: `issues/problem-identified/ISSUE-001-DIAGNOSIS.md`
- Moves: `ISSUE-001-CONTEXT.md` to `problem-identified/`

---

### 3. Propose Solution

```bash
/propose-solution ISSUE-001
```

**What happens:**
- Reads diagnosis + context
- Loads `workflow/issues/templates/3-SOLUTION-TEMPLATE.md`
- Guides through **5-step mandatory checklist**:

**Step 1: Solution Design**
- Evaluate 2-3 different approaches
- Pros/cons for each
- Select best option with justification

**Step 2: Implementation Plan**
- List ALL files to modify (with line numbers)
- Exact code changes (BEFORE/AFTER)
- Execution order
- Risk assessment

**Step 3: Testing Strategy**
- Unit tests (what to test)
- Integration tests (end-to-end workflows)
- Regression tests (full suite)
- Performance tests (if applicable)

**Step 4: Rollback Plan**
- Can we rollback? (Yes/No and why)
- Rollback steps (exact commands)
- Data migration needs
- Rollback risks

**Step 5: Documentation**
- Code comments needed
- API docs to update
- Architecture docs to update

**Output:**
- Creates: `issues/solution-identified/ISSUE-001-SOLUTION.md`
- Moves: CONTEXT + DIAGNOSIS to `solution-identified/`

---

### 4. Implement and Test

```bash
/test-ready ISSUE-001
```

**What happens:**
- Reads all 3 files (context, diagnosis, solution)
- Loads `workflow/issues/templates/4-TESTING-TEMPLATE.md`
- Guides through **9-phase mandatory checklist**:

**Phase 1: Pre-Implementation Review**
**Phase 2: Implementation** (follow plan)
**Phase 3: Unit Testing** (create + run tests)
**Phase 4: Integration Testing** (verify fix works)
**Phase 5: Regression Testing** (no breakage)
**Phase 6: Performance Testing** (if applicable)
**Phase 7: Code Quality** (black, isort, flake8, mypy)
**Phase 8: Documentation** (comments, API docs, CHANGELOG)
**Phase 9: Commit** (with detailed message)

**Validation Gates:**
- ✅ Original issue fixed
- ✅ All tests pass
- ✅ Code quality checks pass
- ✅ Documentation updated
- ✅ Commit created

**Output:**
- Creates: `issues/needs-tested/ISSUE-001-TESTING.md`
- Moves: All 3 files to `needs-tested/`
- Creates git commit

---

### 5. Archive Resolved Issue

```bash
/archive-issue ISSUE-001
```

**What happens:**
- Reads all 4 files
- Verifies resolution complete
- Creates: `issues/archived/2025-10/ISSUE-001-cache-crashes/`
- Creates: `SUMMARY.md` (quick reference)
- Moves all files to archive

**Archive structure:**
```
archived/2025-10/ISSUE-001-cache-crashes/
├── SUMMARY.md      # Quick reference
├── CONTEXT.md      # Original issue
├── DIAGNOSIS.md    # Root cause analysis
├── SOLUTION.md     # Fix proposal
└── TESTING.md      # Validation results
```

---

## Using in Multiple Projects

### Wrapper + Main Codebase Pattern

**If you have a wrapper repo (research, planning) and main codebase:**

**Option A: Issues in wrapper only (recommended)**
```
Wrapper-Repo/
├── workflow/ (submodule)
├── issues/ (all issues tracked here)
└── main-codebase/ (symlink to actual repo)

Main-Repo/
├── workflow/ (submodule - optional for flexibility)
└── NO issues/ directory
```

**Benefits:**
- ✅ Clean separation (issues with research, code stays focused)
- ✅ Issues track research, upgrades, and code problems
- ✅ Single location for all project issues

**Workflow:**
```bash
cd Wrapper-Repo
/new-issue "Problem in main codebase"
# → Creates in Wrapper-Repo/issues/

/diagnose ISSUE-001
# → Uses Wrapper-Repo/workflow/issues/templates/

# Fix implementation may edit main-codebase/ files
/test-ready ISSUE-001
# → Issue artifacts stay in Wrapper-Repo/issues/
# → Code changes go to main codebase
```

---

**Option B: Issues in both repos**
```
Wrapper-Repo/
├── workflow/ (submodule)
└── issues/ (high-level issues, research, upgrades)

Main-Repo/
├── workflow/ (submodule)
└── issues/ (code-specific issues)
```

**Benefits:**
- ✅ Flexibility to create issues where relevant
- ✅ Code issues stay with code
- ✅ Research issues stay with research

**Setup:**
```bash
# In each repo:
git submodule add https://github.com/rglaubitz/features-implementation-workflow.git workflow
cp workflow/commands/*.md .claude/commands/
mkdir -p issues/{new-issue-context,problem-identified,solution-identified,needs-tested,archived}
```

---

## Updating the System

### Update Workflow Templates

**When workflow repository is updated:**
```bash
cd workflow
git pull origin main
cd ..
git add workflow
git commit -m "chore: Update workflow submodule"
```

Slash commands automatically reference latest templates from workflow.

### Update Slash Commands

**If command definitions change:**
```bash
# Remove old commands
rm .claude/commands/{new-issue,diagnose,propose-solution,test-ready,archive-issue}.md

# Copy new versions
cp workflow/commands/{new-issue,diagnose,propose-solution,test-ready,archive-issue}.md .claude/commands/
```

---

## Troubleshooting

### Issue: Slash commands can't find templates

**Error:** `workflow/issues/templates/1-NEW-ISSUE-TEMPLATE.md not found`

**Solution:**
```bash
# Verify workflow submodule exists
ls workflow/

# If missing, add it
git submodule add https://github.com/rglaubitz/features-implementation-workflow.git workflow
git submodule update --init --recursive

# Verify templates exist
ls workflow/issues/templates/
```

---

### Issue: /new-issue creates wrong ISSUE number

**Problem:** Next issue number detection incorrect

**Solution:**
- Check `issues/new-issue-context/` for highest ISSUE-NNN
- Issue numbers increment forever (never reset)
- If gap needed, manually create placeholder

---

### Issue: Git won't commit empty issues/ directories

**Problem:** Empty folders not tracked by git

**Solution:** This is normal! Only commit when issues exist.

Or create `.gitkeep`:
```bash
touch issues/new-issue-context/.gitkeep
touch issues/problem-identified/.gitkeep
# etc.
git add issues/**/.gitkeep
```

---

## Best Practices

### ✅ Do's

- **Always complete full checklist** (no skipping steps)
- **Read all affected files** (no assumptions)
- **Test thoroughly** (unit + integration + regression)
- **Document decisions** (why, not just what)
- **Create detailed commit messages**

### ❌ Don'ts

- **Don't skip diagnosis phase**
- **Don't assume root cause without evidence**
- **Don't modify code without impact analysis**
- **Don't commit without tests**
- **Don't archive without validation**

---

## Support

**Documentation:**
- System overview: `workflow/issues/README.md`
- Command reference: `workflow/issues/COMMAND-REFERENCE.md`
- Quick start: `workflow/issues/QUICK-START.md`

**Source:**
- GitHub: https://github.com/rglaubitz/features-implementation-workflow

---

**Setup Guide Version:** 1.0
**Last Updated:** 2025-10-31
