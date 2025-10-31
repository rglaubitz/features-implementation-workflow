# Issues Management System

**Purpose:** Meticulous, structured approach to debugging and fixing issues in the Apex Memory System.

**Philosophy:** Every issue follows a **mandatory checklist** approach to ensure:
- Complete diagnosis (no assumptions)
- Proper root cause analysis
- Comprehensive solution design
- Thorough testing
- Full documentation

---

## 🎯 Quick Start

### 1. Report New Issue
```bash
/new-issue "Cache system crashes on repeated queries"
```
**Result:** Creates `issues/new-issue-context/ISSUE-001-cache-crashes.md`

### 2. Diagnose Problem
```bash
/diagnose ISSUE-001
```
**Result:** Creates structured diagnosis in `issues/problem-identified/`

### 3. Propose Solution
```bash
/propose-solution ISSUE-001
```
**Result:** Creates solution proposal in `issues/solution-identified/`

### 4. Test & Validate
```bash
/test-ready ISSUE-001
```
**Result:** Moves to `issues/needs-tested/` with testing checklist

### 5. Archive Resolved Issue
```bash
/archive-issue ISSUE-001
```
**Result:** Moves to `issues/archived/YYYY-MM/ISSUE-001/`

---

## 📁 Directory Structure

```
issues/
├── README.md                      # This file
├── templates/
│   ├── 1-NEW-ISSUE-TEMPLATE.md   # Initial issue capture
│   ├── 2-DIAGNOSIS-TEMPLATE.md   # Problem analysis checklist
│   ├── 3-SOLUTION-TEMPLATE.md    # Solution design checklist
│   ├── 4-TESTING-TEMPLATE.md     # Validation checklist
│   └── COMMAND-REFERENCE.md      # All slash commands
├── new-issue-context/
│   └── ISSUE-NNN-*.md            # New issues start here
├── problem-identified/
│   ├── ISSUE-NNN-CONTEXT.md      # Original issue
│   └── ISSUE-NNN-DIAGNOSIS.md    # Diagnosis results
├── solution-identified/
│   ├── ISSUE-NNN-DIAGNOSIS.md    # Problem analysis
│   └── ISSUE-NNN-SOLUTION.md     # Solution proposal
├── needs-tested/
│   ├── ISSUE-NNN-CONTEXT.md      # Original issue
│   ├── ISSUE-NNN-DIAGNOSIS.md    # Problem analysis
│   ├── ISSUE-NNN-SOLUTION.md     # Solution proposal
│   └── ISSUE-NNN-TESTING.md      # Testing results
└── archived/
    └── YYYY-MM/
        └── ISSUE-NNN-*/
            ├── SUMMARY.md          # Quick reference
            ├── CONTEXT.md          # Original issue
            ├── DIAGNOSIS.md        # Problem analysis
            ├── SOLUTION.md         # Fix proposal
            └── TESTING.md          # Validation results
```

---

## 🔄 Workflow States

### 1. New Issue Context
**Purpose:** Capture raw issue information

**Entry:** `/new-issue <title>`

**Content:**
- Symptoms observed
- Steps to reproduce
- Expected vs actual behavior
- Error messages
- Affected components

**Exit:** `/diagnose ISSUE-NNN` → moves to Problem Identified

---

### 2. Problem Identified
**Purpose:** Structured diagnosis following mandatory checklist

**Entry:** `/diagnose ISSUE-NNN`

**Mandatory Checklist:**
- ✅ Code review (identify affected files)
- ✅ Error analysis (root cause)
- ✅ Reproduction (verify issue)
- ✅ Impact analysis (cascading effects)
- ✅ Root cause analysis (primary + contributing factors)

**Exit:** `/propose-solution ISSUE-NNN` → moves to Solution Identified

---

### 3. Solution Identified
**Purpose:** Design solution with implementation plan

**Entry:** `/propose-solution ISSUE-NNN`

**Mandatory Checklist:**
- ✅ Solution design (evaluate options)
- ✅ Implementation plan (exact changes)
- ✅ Testing strategy (unit + integration + regression)
- ✅ Rollback plan (safety net)
- ✅ Documentation (code comments + docs)

**Exit:** `/test-ready ISSUE-NNN` → moves to Needs Tested

---

### 4. Needs Tested
**Purpose:** Implement, test, and validate fix

**Entry:** `/test-ready ISSUE-NNN`

**Mandatory Checklist:**
- ✅ Pre-implementation review
- ✅ Implementation (follow plan)
- ✅ Validation (original issue fixed)
- ✅ Regression testing (no breakage)
- ✅ Documentation (update docs)
- ✅ Commit (detailed message)

**Exit:** `/archive-issue ISSUE-NNN` → moves to Archived

---

### 5. Archived
**Purpose:** Store resolved issues for future reference

**Entry:** `/archive-issue ISSUE-NNN`

**Organization:** By month (YYYY-MM)

**Contents:** Complete issue history (context → diagnosis → solution → testing)

---

## 🎯 Mandatory Principles

### 1. Always Review Codebase
**Never make assumptions.** Always:
- ✅ `grep` for keywords
- ✅ `Read` all affected files
- ✅ Map dependencies (upstream + downstream)
- ✅ Check for similar patterns elsewhere

### 2. Always Verify Impact
**Never change code without impact analysis.** Always:
- ✅ Direct impact (immediate breakage)
- ✅ Cascading effects (secondary breakage)
- ✅ Database schema changes
- ✅ API breaking changes
- ✅ User-facing impact

### 3. Always Test Thoroughly
**Never commit without comprehensive testing.** Always:
- ✅ Unit tests (specific functions)
- ✅ Integration tests (end-to-end)
- ✅ Regression tests (existing functionality)
- ✅ Performance tests (if performance-related)

### 4. Always Document
**Never leave future developers guessing.** Always:
- ✅ Code comments (why, not what)
- ✅ API docs (if API changed)
- ✅ Architecture docs (if design changed)
- ✅ Commit message (detailed)

### 5. Always Have Rollback Plan
**Never deploy without escape hatch.** Always:
- ✅ Can rollback? (yes/no)
- ✅ Rollback steps (exact commands)
- ✅ Data migration needed? (yes/no)
- ✅ Rollback risks (what breaks)

---

## 📝 Severity Levels

### P0 - Critical (Production Blocker)
- System crashes
- Data loss
- Security vulnerabilities
- **SLA:** Fix within 24 hours

### P1 - High (Major Functionality Broken)
- Core features broken
- Performance degradation >50%
- **SLA:** Fix within 1 week

### P2 - Medium (Minor Functionality Broken)
- Non-core features broken
- Workarounds available
- **SLA:** Fix within 2 weeks

### P3 - Low (Enhancement/Nice-to-Have)
- Cosmetic issues
- Minor improvements
- **SLA:** Fix when capacity available

---

## 🔍 Example: Full Workflow

### Step 1: New Issue
```bash
/new-issue "Cache system crashes on repeated queries"
```

**Creates:** `issues/new-issue-context/ISSUE-009-cache-crashes.md`

**Content:**
```markdown
# ISSUE-009: Cache System Crashes on Repeated Queries

**Severity:** P0
**Symptoms:** 500 errors on 2nd-3rd query
**Steps to Reproduce:** Query "ACME Corporation" with use_cache=true, repeat
```

---

### Step 2: Diagnose
```bash
/diagnose ISSUE-009
```

**Claude is guided through checklist:**
1. ✅ Code review → identifies cache.py, router.py
2. ✅ Error analysis → no try-catch around cache operations
3. ✅ Reproduction → confirmed crash
4. ✅ Impact → all queries crash if cache enabled
5. ✅ Root cause → cache failures propagate as 500 errors

**Creates:** `issues/problem-identified/ISSUE-009-DIAGNOSIS.md`

---

### Step 3: Propose Solution
```bash
/propose-solution ISSUE-009
```

**Claude is guided through checklist:**
1. ✅ Solution design → Add try-catch to cache operations
2. ✅ Implementation plan → Modify router.py lines 563-605, 735-786
3. ✅ Testing strategy → Test cache errors don't crash
4. ✅ Rollback plan → `git revert` (backwards compatible)
5. ✅ Documentation → Add code comments

**Creates:** `issues/solution-identified/ISSUE-009-SOLUTION.md`

---

### Step 4: Test
```bash
/test-ready ISSUE-009
```

**Claude implements fix and validates:**
1. ✅ Reproduce original issue (crashes without fix)
2. ✅ Apply fix (add try-catch)
3. ✅ Verify fixed (no more crashes)
4. ✅ Regression test (existing tests pass)
5. ✅ Commit with detailed message

**Creates:** `issues/needs-tested/ISSUE-009-TESTING.md`

---

### Step 5: Archive
```bash
/archive-issue ISSUE-009
```

**Moves to:** `issues/archived/2025-10/ISSUE-009-cache-crashes/`

**Contains:**
- SUMMARY.md (quick reference)
- CONTEXT.md (original issue)
- DIAGNOSIS.md (problem analysis)
- SOLUTION.md (fix proposal)
- TESTING.md (validation results)

---

## 📚 Additional Resources

- **Templates:** See `issues/templates/` for all templates
- **Commands:** See `issues/templates/COMMAND-REFERENCE.md` for detailed command docs
- **Examples:** See `issues/archived/` for real-world examples

---

## 🎯 Success Metrics

### Quality Gates
- ✅ Every issue has complete diagnosis (all checklist items)
- ✅ Every solution has rollback plan
- ✅ Every fix has comprehensive tests
- ✅ Every commit has detailed message
- ✅ Every issue is archived with full history

### Metrics to Track
- Average time to resolution (by severity)
- Test coverage increase per issue
- Regression rate (bugs introduced by fixes)
- Documentation completeness

---

**Last Updated:** 2025-10-26
**System Version:** 1.0
**Maintainer:** Richard Glaubitz
