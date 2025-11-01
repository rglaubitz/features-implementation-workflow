# Issues System - Quick Start

**Get started with issues management in 5 minutes.**

---

## 🚀 First Time Setup

### Prerequisites
- Git repository
- Claude Code installed

### Setup Commands (Copy & Paste)

```bash
# 1. Add workflow submodule
git submodule add https://github.com/rglaubitz/features-implementation-workflow.git workflow
git submodule update --init --recursive

# 2. Copy slash commands
cp workflow/commands/{new-issue,diagnose,propose-solution,test-ready,archive-issue}.md .claude/commands/

# 3. Create issues directory structure
mkdir -p issues/{new-issue-context,problem-identified,solution-identified,needs-tested,archived}

# 4. Test it (in Claude Code)
# /new-issue "Test - verify system works"
```

**Done!** ✅ System ready to use.

---

## 📋 Daily Usage

### Create New Issue

```
/new-issue "Brief description of problem"
```

**Example:**
```
/new-issue "Cache system crashes on repeated queries"
```

**Output:** Creates `issues/new-issue-context/ISSUE-001-cache-system-crashes.md`

---

### Diagnose Issue

```
/diagnose ISSUE-001
```

**What it does:**
- Guides through 5-step mandatory checklist
- Searches codebase for related code
- Analyzes errors and stack traces
- Reproduces issue
- Identifies root cause

**Output:**
- Creates `ISSUE-001-DIAGNOSIS.md`
- Moves files to `problem-identified/`

---

### Propose Solution

```
/propose-solution ISSUE-001
```

**What it does:**
- Evaluates 2-3 different approaches
- Creates implementation plan
- Designs testing strategy
- Documents rollback plan

**Output:**
- Creates `ISSUE-001-SOLUTION.md`
- Moves files to `solution-identified/`

---

### Implement and Test

```
/test-ready ISSUE-001
```

**What it does:**
- Implements the solution
- Runs unit + integration + regression tests
- Validates code quality (black, isort, flake8, mypy)
- Creates git commit

**Output:**
- Creates `ISSUE-001-TESTING.md`
- Moves files to `needs-tested/`
- Creates commit

---

### Archive Resolved Issue

```
/archive-issue ISSUE-001
```

**What it does:**
- Verifies resolution complete
- Creates archive folder with full history
- Generates summary

**Output:** `issues/archived/2025-10/ISSUE-001-description/`

---

## 📂 Where Things Live

### Templates (Don't Edit - They're Reusable)

```
workflow/issues/templates/
├── 1-NEW-ISSUE-TEMPLATE.md      # Issue context capture
├── 2-DIAGNOSIS-TEMPLATE.md      # 5-step diagnosis checklist
├── 3-SOLUTION-TEMPLATE.md       # Solution design + rollback
└── 4-TESTING-TEMPLATE.md        # 9-phase implementation
```

### Your Issues (Project-Specific)

```
issues/
├── new-issue-context/      # New issues awaiting diagnosis
├── problem-identified/     # Diagnosed issues with root cause
├── solution-identified/    # Planned solutions
├── needs-tested/          # Implemented solutions
└── archived/YYYY-MM/      # Resolved issues
```

### Commands (Reference Templates)

```
.claude/commands/
├── new-issue.md
├── diagnose.md
├── propose-solution.md
├── test-ready.md
└── archive-issue.md
```

---

## 🎯 Complete Example

**Scenario:** Cache crashes on repeated queries

```bash
# 1. Create issue
/new-issue "Cache crashes on repeated queries"
# → ISSUE-001 created in new-issue-context/

# 2. Fill in symptoms, steps to reproduce, error messages
# (Edit ISSUE-001 file)

# 3. Diagnose
/diagnose ISSUE-001
# → Searches codebase: cache.py, router.py
# → Reads affected files
# → Reproduces crash
# → Root cause: No error handling in cache operations
# → Moves to problem-identified/

# 4. Propose solution
/propose-solution ISSUE-001
# → Option 1: Add try-catch (recommended)
# → Option 2: Redesign cache system
# → Creates implementation plan
# → Defines tests
# → Documents rollback: git revert
# → Moves to solution-identified/

# 5. Implement and test
/test-ready ISSUE-001
# → Adds try-catch to cache.py
# → Creates 2 unit tests
# → Runs regression tests (all pass)
# → Code quality: black, isort, flake8, mypy (all pass)
# → Creates commit: "fix: Add error handling to cache operations"
# → Moves to needs-tested/

# 6. Archive
/archive-issue ISSUE-001
# → Verifies resolution complete
# → Archives to: archived/2025-10/ISSUE-001-cache-crashes/
#    ├── SUMMARY.md
#    ├── CONTEXT.md
#    ├── DIAGNOSIS.md
#    ├── SOLUTION.md
#    └── TESTING.md
```

**Total time:** 1-3 hours (depending on complexity)

---

## ⚡ Quick Tips

### Mandatory Checklists

**Each phase has a checklist - you MUST complete all items:**

- **Diagnosis:** 5 steps (code review, error analysis, reproduction, impact, root cause)
- **Solution:** 5 steps (design, plan, testing, rollback, documentation)
- **Testing:** 9 phases (review, implement, unit, integration, regression, performance, quality, docs, commit)

**Cannot proceed to next phase until current checklist is complete.**

### Always Read Files

- **Don't assume** - read every affected file
- **Use Grep** to search codebase
- **Use Read** to examine files
- **Check dependencies** - what calls this? what does this call?

### Test Thoroughly

- **Unit tests** - specific functions
- **Integration tests** - end-to-end workflows
- **Regression tests** - run full suite
- **Original issue test** - verify fix works

### Document Decisions

- **Why**, not just what
- **Evidence** - test results, code snippets
- **Tradeoffs** - what we gave up
- **Alternatives** - what we didn't choose and why

---

## 🔄 Updating Templates

**When workflow repository is updated:**

```bash
cd workflow
git pull origin main
cd ..
git add workflow
git commit -m "chore: Update workflow submodule"
```

Slash commands automatically use latest templates.

---

## 📚 Full Documentation

- **Complete setup guide:** `workflow/issues/SETUP-GUIDE.md`
- **System overview:** `workflow/issues/README.md`
- **Command reference:** `workflow/issues/COMMAND-REFERENCE.md`

---

**Quick Start Version:** 1.0
**Last Updated:** 2025-10-31
