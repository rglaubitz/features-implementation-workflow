# ISSUE-{NNN}: {Title} - TESTING & VALIDATION

**Issue ID:** ISSUE-{NNN}
**Testing Date:** {YYYY-MM-DD}
**Tested By:** Claude Code
**Status:** Needs Tested

---

## ✅ MANDATORY TESTING CHECKLIST

---

### Phase 1: Pre-Implementation Review

- [ ] **Read solution proposal** (`ISSUE-{NNN}-SOLUTION.md`)
- [ ] **Verify all files identified** (no missing dependencies)
- [ ] **Confirm test plan complete** (unit + integration + regression)
- [ ] **Check for breaking changes** (migration needed?)
- [ ] **Review rollback plan** (can safely revert?)

---

### Phase 2: Implementation

- [ ] **Follow execution order** (from solution proposal)
- [ ] **Step 1:** {description}
  - File: `path/to/file.py`
  - Changes: {what changed}
  - Verified: ✅ Syntax correct

- [ ] **Step 2:** {description}
  - File: `path/to/file.py`
  - Changes: {what changed}
  - Verified: ✅ Syntax correct

- [ ] **All changes made:** ✅ Complete

---

### Phase 3: Unit Testing

#### Test 1: {Test Name}
- [ ] **Test file:** `tests/unit/test_file.py`
- [ ] **Test created:** ✅
- [ ] **Test runs:** ✅
- [ ] **Test passes:** {✅ Pass / ❌ Fail}
- [ ] **Evidence:**
  ```
  {test output}
  ```

#### Test 2: {Test Name}
- [ ] **Test file:** `tests/unit/test_file.py`
- [ ] **Test created:** ✅
- [ ] **Test runs:** ✅
- [ ] **Test passes:** {✅ Pass / ❌ Fail}

---

### Phase 4: Integration Testing

#### Original Issue Reproduction
- [ ] **Reproduce ISSUE-{NNN} WITHOUT fix:**
  - Steps: {from ISSUE-{NNN}-CONTEXT.md}
  - Result: {still broken? yes/no}
  - Evidence: {error message/behavior}

- [ ] **Apply fix and test again:**
  - Steps: {same steps}
  - Result: {fixed? yes/no}
  - Evidence: {success message/behavior}

#### End-to-End Test
- [ ] **Full workflow test:**
  - Input: {test data}
  - Process: {steps}
  - Output: {expected result}
  - Result: {✅ Pass / ❌ Fail}

---

### Phase 5: Regression Testing

- [ ] **Run full test suite:**
  ```bash
  pytest tests/ -v
  ```

- [ ] **Results:**
  - Tests run: {count}
  - Passed: {count}
  - Failed: {count}
  - Skipped: {count}

- [ ] **Any failures?** {Yes/No}
  - If yes: List: {which tests}
  - If yes: Related to fix? {yes/no}
  - If yes: Action: {fix/investigate/acceptable}

---

### Phase 6: Performance Testing

- [ ] **Performance affected?** {Yes/No/Not Applicable}

- [ ] **If applicable:**
  - Baseline: {metric}
  - After fix: {metric}
  - Change: {+/-X%}
  - Acceptable: {yes/no}

---

### Phase 7: Code Quality

- [ ] **Format code:**
  ```bash
  black src/ tests/
  isort src/ tests/
  ```

- [ ] **Lint code:**
  ```bash
  flake8 src/ tests/ --max-line-length=100
  ```

- [ ] **Type check:**
  ```bash
  mypy src/
  ```

- [ ] **All checks pass:** {Yes/No}

---

### Phase 8: Documentation

- [ ] **Code comments added:** ✅
  - File: `file.py:line` - {what commented}

- [ ] **API docs updated:** {✅ Yes / N/A}
  - File: {which docs}

- [ ] **Architecture docs updated:** {✅ Yes / N/A}
  - File: {which docs}

- [ ] **CHANGELOG updated:** ✅
  - Entry: `## [Unreleased] - ISSUE-{NNN}: {Title}`

---

### Phase 9: Commit

- [ ] **Stage changes:**
  ```bash
  git add {files}
  ```

- [ ] **Commit with detailed message:**
  ```bash
  git commit -m "fix: ISSUE-{NNN} - {Title}

  PROBLEM: {1-line problem}
  ROOT CAUSE: {1-line cause}
  FIX: {1-line fix}
  IMPACT: {breaking changes/none}

  Files changed: {list}
  Tests added: {count}
  "
  ```

- [ ] **Commit hash:** {hash}

---

## 🧪 TEST RESULTS SUMMARY

### Unit Tests
| Test Name | Status | Notes |
|-----------|--------|-------|
| test_1 | ✅ Pass | {notes} |
| test_2 | ✅ Pass | {notes} |

### Integration Tests
| Test Name | Status | Notes |
|-----------|--------|-------|
| test_original_issue | ✅ Pass | Issue fixed |
| test_end_to_end | ✅ Pass | {notes} |

### Regression Tests
- **Total:** {count}
- **Passed:** {count}
- **Failed:** {count} (acceptable: {reason})

---

## 📸 EVIDENCE

### Before Fix
```
{Error output showing original issue}
```

### After Fix
```
{Success output showing issue resolved}
```

### Test Output
```
pytest tests/unit/test_file.py::test_name -v
=== test session starts ===
collected 1 item

tests/unit/test_file.py::test_name PASSED [100%]

=== 1 passed in 0.5s ===
```

---

## ✅ RESOLUTION STATUS

### Issue Resolution
- [ ] **Original issue fixed:** {✅ Yes / ❌ No / 🔄 Partial}
- [ ] **No regressions introduced:** ✅
- [ ] **Tests comprehensive:** ✅
- [ ] **Documentation complete:** ✅
- [ ] **Code quality:** ✅

### Final Checklist
- [ ] **Commit created:** ✅ {hash}
- [ ] **Ready to push:** {✅ Yes / ❌ No - {why}}
- [ ] **Ready to deploy:** {✅ Yes / ❌ No - {why}}
- [ ] **Ready to archive:** {✅ Yes / ❌ No - {why}}

---

## 📊 METRICS

### Code Changes
- Files modified: {count}
- Lines added: {count}
- Lines removed: {count}
- Net change: {+/- count}

### Test Coverage
- Tests added: {count}
- Coverage before: {percentage}
- Coverage after: {percentage}
- Coverage change: {+/-percentage}

### Time Spent
- Diagnosis: {hours}
- Solution design: {hours}
- Implementation: {hours}
- Testing: {hours}
- Total: {hours}

---

## ✅ Next Steps

- [ ] Push to repository: `git push`
- [ ] Create PR (if applicable)
- [ ] Deploy to staging
- [ ] Deploy to production
- [ ] Archive issue: `/archive-issue ISSUE-{NNN}`

---

**Testing Version:** 1.0
**Last Updated:** 2025-10-26
