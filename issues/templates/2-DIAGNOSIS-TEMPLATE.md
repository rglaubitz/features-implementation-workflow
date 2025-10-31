# ISSUE-{NNN}: {Title} - DIAGNOSIS

**Issue ID:** ISSUE-{NNN}
**Diagnosis Date:** {YYYY-MM-DD}
**Diagnosed By:** Claude Code
**Status:** Problem Identified

---

## 🎯 MANDATORY DIAGNOSTIC CHECKLIST

**CRITICAL:** All checklist items must be completed. No assumptions allowed.

---

### ✅ Step 1: Code Review (REQUIRED)

#### 1.1 Identify Affected Files
- [ ] **Search codebase for keywords** (from error message/symptoms)
  ```bash
  # Commands used:
  grep -r "keyword" src/
  glob "pattern"
  ```

- [ ] **List all affected files:**
  - Primary file: `path/to/file1.py` (main bug location)
  - Related file: `path/to/file2.py` (calls primary)
  - Related file: `path/to/file3.py` (called by primary)

- [ ] **Read ALL affected files** (use Read tool, no assumptions!)
  - `file1.py` - Read lines {start}-{end}
  - `file2.py` - Read lines {start}-{end}
  - `file3.py` - Read lines {start}-{end}

#### 1.2 Map Dependencies
- [ ] **Upstream dependencies** (what calls this code?)
  - Function: `caller1()` in `file.py:123`
  - Function: `caller2()` in `file.py:456`

- [ ] **Downstream dependencies** (what does this code call?)
  - Function: `callee1()` in `file.py:789`
  - Function: `callee2()` in `file.py:012`

- [ ] **Database dependencies** (what tables/collections affected?)
  - Table: `table_name` (read/write operations)
  - Collection: `collection_name` (queries)

- [ ] **External service dependencies** (what APIs called?)
  - Service: {name} (endpoint: {url})
  - Service: {name} (endpoint: {url})

#### 1.3 Check for Similar Patterns
- [ ] **Grep for similar code patterns** (is this bug elsewhere too?)
  ```bash
  # Search for similar patterns:
  grep -r "similar_pattern" src/
  ```

- [ ] **Similar patterns found:**
  - Location: `file.py:line` (same pattern, same risk)
  - Location: `file.py:line` (same pattern, same risk)

---

### ✅ Step 2: Error Analysis (REQUIRED)

#### 2.1 Error Message Analysis
- [ ] **Full error message:**
  ```
  {Paste complete error here}
  ```

- [ ] **Error type:**
  - [ ] Exception (which type: {ValueError/KeyError/etc})
  - [ ] HTTP error (status code: {500/404/etc})
  - [ ] Database error (which database: {Neo4j/PostgreSQL/etc})
  - [ ] Timeout
  - [ ] Resource exhaustion
  - [ ] Other: {specify}

#### 2.2 Stack Trace Analysis
- [ ] **Error originates at:**
  - File: `path/to/file.py`
  - Line: {line number}
  - Function: `function_name()`
  - Code: `{exact line of code}`

- [ ] **Call stack:**
  1. Entry point: `file.py:line` → `function()`
  2. Calls: `file.py:line` → `function()`
  3. Calls: `file.py:line` → `function()`
  4. Error: `file.py:line` → `function()` ← **CRASH HERE**

#### 2.3 Error Handling Review
- [ ] **Is error caught?** {Yes/No}
  - If yes: Where? `file.py:line`
  - If no: Should it be? {Yes/No}

- [ ] **Is there graceful degradation?** {Yes/No}
  - If yes: What happens? {description}
  - If no: Should there be? {Yes/No}

- [ ] **Are errors logged?** {Yes/No}
  - If yes: Where? `logger.error()` at `file.py:line`
  - If no: Should they be? {Yes/No}

---

### ✅ Step 3: Reproduction (REQUIRED)

#### 3.1 Reproduce Original Issue
- [ ] **Follow exact steps from ISSUE-{NNN}-CONTEXT.md**
  - Step 1: {action taken}
  - Step 2: {action taken}
  - Step 3: {action taken}
  - Result: {did it crash? yes/no}

- [ ] **Symptoms match reported issue?** {Yes/No/Partial}
  - Expected symptom: {from context}
  - Actual symptom: {what I saw}
  - Match: {Yes/No}

#### 3.2 Isolate Minimal Case
- [ ] **Simplest way to trigger:**
  ```bash
  # Minimal reproduction:
  {exact command}
  ```

- [ ] **Minimal data required:**
  ```json
  {minimum data set that triggers issue}
  ```

#### 3.3 Test Edge Cases
- [ ] **Edge case 1:** {description}
  - Test: {what I tried}
  - Result: {crashes/works/partially works}

- [ ] **Edge case 2:** {description}
  - Test: {what I tried}
  - Result: {crashes/works/partially works}

- [ ] **What makes it worse:**
  - Factor: {larger data sets? specific inputs?}

- [ ] **What makes it better:**
  - Factor: {smaller data sets? different inputs?}

---

### ✅ Step 4: Impact Analysis (REQUIRED)

#### 4.1 Direct Impact
- [ ] **What breaks immediately?**
  - Feature: {name} - {how broken}
  - Feature: {name} - {how broken}

- [ ] **Which users affected?**
  - User group: {all/some/few}
  - Percentage: {estimate}

- [ ] **Data at risk?** {Yes/No}
  - If yes: What data? {description}
  - If yes: Can it be recovered? {Yes/No}

#### 4.2 Cascading Effects
- [ ] **Secondary breakage:**
  - Component: {name} - {why broken}
  - Component: {name} - {why broken}

- [ ] **Performance impact:**
  - Before: {baseline metric}
  - After: {degraded metric}
  - Degradation: {percentage}

- [ ] **Resource impact:**
  - Memory: {increased/decreased/same}
  - CPU: {increased/decreased/same}
  - Network: {increased/decreased/same}

#### 4.3 Database Impact
- [ ] **Schema changes needed?** {Yes/No}
  - If yes: Which tables? {list}
  - If yes: Migration required? {Yes/No}

- [ ] **Data migration needed?** {Yes/No}
  - If yes: What data? {description}
  - If yes: Can rollback? {Yes/No}

#### 4.4 API Changes
- [ ] **Breaking changes?** {Yes/No}
  - If yes: Which endpoints? {list}
  - If yes: Deprecation period needed? {Yes/No}

- [ ] **New endpoints needed?** {Yes/No}
  - If yes: Which? {list}

#### 4.5 User-Facing Impact
- [ ] **What do users see?**
  - Error message: {what they see}
  - Broken functionality: {what doesn't work}
  - Workaround available: {Yes/No}

- [ ] **Business impact:**
  - Revenue impact: {Yes/No/Unknown}
  - SLA breach: {Yes/No}
  - Customer complaints: {Yes/No}

---

### ✅ Step 5: Root Cause Analysis (REQUIRED)

#### 5.1 Primary Root Cause
- [ ] **What is the ACTUAL bug?**
  - Location: `file.py:line`
  - Code: `{exact buggy code}`
  - Bug type: {logic error/null pointer/race condition/etc}
  - Why it happens: {detailed explanation}

#### 5.2 Contributing Factors
- [ ] **What made this bug possible?**
  - Factor 1: {missing error handling}
  - Factor 2: {no input validation}
  - Factor 3: {assumption about data}

#### 5.3 Why Not Caught Earlier
- [ ] **Testing gaps:**
  - Missing test: {what test would have caught this}
  - Coverage gap: {which code not tested}

- [ ] **Code review gaps:**
  - Missed in review: {why}
  - No review: {was it reviewed?}

#### 5.4 Similar Issues
- [ ] **Have we seen this pattern before?**
  - Previous issue: ISSUE-{NNN} ({similar how})
  - Previous issue: ISSUE-{NNN} ({similar how})

- [ ] **Is this systematic?**
  - Pattern: {description}
  - Affected locations: {list}

---

## 📊 DIAGNOSIS RESULTS

### Root Cause Summary

**Primary Cause:**
{1-2 sentence summary of the actual bug}

**Location:**
- File: `path/to/file.py`
- Lines: {start}-{end}
- Function: `function_name()`

**Mechanism:**
{Detailed explanation of how the bug manifests}

**Contributing Factors:**
1. {Factor 1}
2. {Factor 2}
3. {Factor 3}

---

### Affected Components

| Component | Impact | Severity |
|-----------|--------|----------|
| {Component 1} | {How affected} | {High/Medium/Low} |
| {Component 2} | {How affected} | {High/Medium/Low} |
| {Component 3} | {How affected} | {High/Medium/Low} |

---

### Impact Scope

**Direct Impact:**
- {Immediate breakage 1}
- {Immediate breakage 2}

**Cascading Impact:**
- {Secondary effect 1}
- {Secondary effect 2}

**User Impact:**
- Users affected: {number/percentage}
- Functionality lost: {description}
- Workaround: {available/not available}

---

### Severity Justification

**Why {P0/P1/P2/P3}:**
{Detailed justification for severity rating}

**Urgency factors:**
- {Factor 1}
- {Factor 2}

**Can wait?** {Yes/No - why/why not}

---

### Code References

**Primary bug location:**
```python
# File: path/to/file.py:123-156

def buggy_function():
    # Line 145: BUG IS HERE
    result = risky_operation()  # ← No error handling!
    return result
```

**Related code:**
- `file.py:789` - Calls buggy function
- `file.py:012` - Similar pattern (also at risk)

---

### Test Gaps Identified

**Missing tests:**
1. **Test name:** `test_cache_error_handling()`
   - **Purpose:** Verify cache errors don't crash system
   - **Why missing:** {reason}

2. **Test name:** `test_edge_case_large_input()`
   - **Purpose:** Verify handles large inputs gracefully
   - **Why missing:** {reason}

**Coverage gaps:**
- File: `file.py` - {percentage}% coverage
- Missing: Error handling paths not tested

---

## ✅ Next Steps

- [ ] Create solution proposal: `/propose-solution ISSUE-{NNN}`
- [ ] Update severity if changed: {new severity}
- [ ] Notify stakeholders: {list}

---

**Diagnosis Version:** 1.0
**Last Updated:** 2025-10-26
