# Documentation Chunking Workflow

**Purpose:** Transform large research documents into usable, workflow-integrated documentation systems

**Problem Solved:** Large research files (500-900+ lines) cause context loss, hallucinations, and low utilization during development

**Success Metric:** Increase research utilization from ~20% to ~80% during implementation

---

## The Problem

**Without chunking:**
- Claude reads 3,700-line file → uses ~15,000 tokens
- Loses context of earlier sections
- Hallucinates patterns from incomplete recall
- Developers read 900-line file → overwhelming, skipped

**With chunking:**
- Claude reads 150-line file → uses ~600 tokens
- Focused context, accurate recall
- No hallucination (complete section in memory)
- Developers read 150 lines → manageable, actually used

---

## When to Apply This Workflow

**Apply chunking when:**
- ✅ Research document exceeds 500 lines
- ✅ Document covers multiple distinct topics
- ✅ Research completed and ready for implementation
- ✅ Team needs to reference research during development

**Don't apply chunking when:**
- ❌ Document is <300 lines (manageable as-is)
- ❌ Document covers single, cohesive topic
- ❌ Research is still in progress (frequent changes)

---

## Workflow Overview

```
Step 1: Analyze Structure
    ↓
Step 2: Plan Chunks (4-6 per original file)
    ↓
Step 3: Create Chunks (~150 lines each)
    ↓
Step 4: Add Cross-References
    ↓
Step 5: Create Navigation System (INDEX.md)
    ↓
Step 6: Create Workflow Guide
    ↓
Step 7: Archive Originals
    ↓
Step 8: Validate & Test
```

---

## Step 1: Analyze Structure

**Goal:** Understand the research document's organization

**Actions:**

1. **Read the entire document**
   - Identify major sections (headings)
   - Note distinct topics
   - Count lines per section

2. **Identify natural boundaries**
   - Topic shifts
   - Technology changes
   - Pattern categories

3. **Document findings**
   ```markdown
   Original File: claude-tool-use-and-streaming.md (642 lines)

   Major Sections:
   - Tool Use API (150 lines)
   - Streaming API (120 lines)
   - Apex Tool Definitions (230 lines)
   - Tool Orchestration (200 lines)

   Total: 4 natural chunks
   ```

**Deliverable:** Analysis notes showing chunk boundaries

---

## Step 2: Plan Chunks

**Goal:** Design optimal chunk structure

**Guidelines:**

- **Chunk Size:** 80-250 lines (target 150 lines)
- **Count:** 4-6 chunks per original file
- **Focus:** Each chunk = 1 cohesive topic
- **Independence:** Each chunk standalone (can be read alone)

**Planning Template:**

```markdown
# Chunk Plan: [Original File Name]

**Original:** [filename] ([line count] lines)
**Target Chunks:** [count]

## Chunk Breakdown

### Chunk 1: [topic-name.md]
- **Lines:** ~150
- **Content:** [description]
- **Standalone:** Yes/No

### Chunk 2: [topic-name.md]
- **Lines:** ~120
- **Content:** [description]
- **Standalone:** Yes/No

[... continue for all chunks ...]

## Cross-References Needed
- Chunk 1 → Chunks 2, 3
- Chunk 2 → Chunks 1, 4
[... etc ...]
```

**Deliverable:** Complete chunk plan with boundaries

---

## Step 3: Create Chunks

**Goal:** Extract content into focused files

**Process:**

1. **Create chunk files**
   ```bash
   # In research/documentation/ folder
   touch tool-use-api.md
   touch streaming-api.md
   touch apex-tool-definitions.md
   touch tool-orchestration.md
   ```

2. **Add standard header**
   ```markdown
   # [Topic Name] - [Context]

   **Source:** [Original file or URL]
   **Date Created:** [Date]
   **Documentation Tier:** Tier 1/2/3

   **Related Documentation:**
   - For [topic] → see `[filename.md]`
   - For [topic] → see `[filename.md]`

   ---
   ```

3. **Extract content**
   - Copy relevant section from original
   - Ensure complete context (include prerequisites)
   - Add code examples inline
   - Preserve formatting

4. **Add references section**
   ```markdown
   ---

   ## References

   **Official Documentation:**
   - [Doc Name]: [URL]

   **Related Apex Documentation:**
   - [Topic] → `filename.md`

   ---

   **Last Updated:** [Date]
   **Documentation Version:** 1.0.0
   **Tier:** Tier 1 (Official Documentation)
   ```

**Deliverable:** All chunk files created with content

---

## Step 4: Add Cross-References

**Goal:** Enable navigation between related chunks

**Pattern:**

```markdown
**Related Documentation:**
- For streaming responses → see `streaming-api.md`
- For Apex-specific tools → see `apex-tool-definitions.md`
- For multi-step workflows → see `tool-orchestration.md`
```

**Guidelines:**

- Add 2-4 cross-references per chunk
- Link to directly related topics only
- Use relative paths (`filename.md`)
- Keep descriptions concise (1-5 words)

**Validation:**

```bash
# Check all chunks have cross-references
for file in *.md; do
  if grep -q "Related Documentation" "$file"; then
    echo "✓ $file"
  else
    echo "✗ $file - MISSING CROSS-REFS"
  fi
done
```

**Deliverable:** All chunks cross-referenced

---

## Step 5: Create Navigation System (INDEX.md)

**Goal:** Provide decision tree navigation

**Structure:**

```markdown
# Documentation Index - Chunked Research Navigation

**Purpose:** Master navigation for all chunked research documentation
**Created:** [Date]
**Total Chunks:** [count] focused files (from [original count] files)

---

## How to Use This Index

**When implementing features**, use this index to find the specific
documentation chunk you need instead of reading large files.

**Decision tree format:**
```
Need to [do something]?
  → Read [specific-file.md]
```

---

## Quick Navigation by Task

### Implementing [Feature Category]

**Need to understand [subtopic]?**
→ Read `[filename.md]`

**Need to [specific action]?**
→ Read `[filename.md]`
→ Read `[filename.md]`

[... continue for all major tasks ...]

---

## Documentation Chunks by Topic

### [Topic Category] ([count] files)

1. **[filename.md]** (~[lines] lines)
   - [One-line description]
   - [Key content highlights]

2. **[filename.md]** (~[lines] lines)
   - [One-line description]
   - [Key content highlights]

[... continue for all chunks ...]

---

## File Size Comparison

**Before Chunking:**
- [file1.md]: [lines] lines
- [file2.md]: [lines] lines
- **Total:** [total] lines in [count] files

**After Chunking:**
- [count] focused files
- **Average:** ~[avg] lines per file (vs [old_avg] average before)
- **Range:** [min]-[max] lines (manageable reads)
- **Benefit:** Read only what you need ([example] lines vs [old_example])

---

## Cross-References

**All chunks include cross-references** pointing to related documentation.

**This ensures you can navigate between related topics easily.**
```

**Deliverable:** Complete INDEX.md with decision trees

---

## Step 6: Create Workflow Guide

**Goal:** Document how to use chunks during development

**Structure:**

```markdown
# Workflow Guide - Using Chunked Documentation During Development

**Purpose:** Structured workflow for using chunked research docs throughout
the project

**Goal:** Ensure research gets used, not forgotten

---

## Workflow Overview

```
Planning → Research → Implementation → Review
   ↓          ↓            ↓             ↓
  ADR     Read chunks   Apply patterns  Validate
```

---

## Phase 1: Planning (Before Writing Code)

### Step 1: Identify Feature Requirements
[User/Claude determines what needs to be built]

### Step 2: Find Relevant Documentation
**Use INDEX.md decision trees**

### Step 3: Read Identified Chunks
**DO:** Read all 3-4 relevant chunks (450-600 lines total)
**DON'T:** Try to read all 16 chunks

### Step 4: Document Architectural Decisions
**Create ADR before implementing**

---

## Phase 2: Implementation (While Writing Code)

### Step 1: Keep Chunks Open
[Open relevant chunks in editor/browser]

### Step 2: Reference Chunks During Development
**Pattern: Look → Implement → Verify**

### Step 3: Use QUICK-REFERENCE for Speed
[Link to quick reference file]

### Step 4: Ask Claude to Reference Chunks
**Good prompt:** "Implement [feature]. First, read [chunk.md],
then apply those patterns to [project]."

---

## Phase 3: Review (After Writing Code)

### Step 1: Self-Review Against Chunks
[Checklist approach]

### Step 2: Validate Implementation
[Ask Claude to review against chunks]

### Step 3: Document Deviations
[Record any deviations from research]

---

## Common Workflows

### Workflow A: New Component from Scratch
[Step-by-step with chunk references]

### Workflow B: Debugging Existing Code
[Step-by-step with chunk references]

### Workflow C: Adding New Feature
[Step-by-step with chunk references]

---

## Anti-Patterns (What NOT to Do)

### ❌ Anti-Pattern 1: Skipping Research
[Problem and solution]

### ❌ Anti-Pattern 2: Reading Everything
[Problem and solution]

### ❌ Anti-Pattern 3: Not Referencing Chunks
[Problem and solution]

---

## Measuring Success

**Good signs you're using chunks effectively:**
✅ Code comments reference specific chunks
✅ PRs mention which chunks were followed
✅ ADRs cite chunk files

**Bad signs you're not using chunks:**
❌ No chunk references in code/PRs
❌ Reimplementing patterns from scratch
❌ Claude hallucinating instead of reading chunks
```

**Deliverable:** Complete WORKFLOW-GUIDE.md

---

## Step 7: Archive Originals

**Goal:** Preserve original files while using chunks

**Process:**

```bash
# Create originals folder
mkdir -p research/documentation/originals

# Move original large files
mv ai-native-ui-patterns.md originals/
mv claude-artifacts-ui-pattern.md originals/
mv claude-tool-use-and-streaming.md originals/
mv shadcn-ui-integration.md originals/

# Verify
ls -la originals/
```

**Rationale:**
- Preserve history
- Allow comparison if needed
- Clean up working directory

**Deliverable:** Original files archived

---

## Step 8: Validate & Test

**Goal:** Ensure no information lost and system works

**Validation Checklist:**

```markdown
### Content Validation
- [ ] All original content present in chunks
- [ ] No duplicate content across chunks
- [ ] All code examples preserved
- [ ] All source citations preserved

### Cross-Reference Validation
- [ ] All chunks have cross-references
- [ ] All cross-references point to existing files
- [ ] No broken links

### Navigation Validation
- [ ] INDEX.md covers all chunks
- [ ] Decision trees complete
- [ ] File size comparison accurate

### Workflow Validation
- [ ] WORKFLOW-GUIDE.md complete
- [ ] All three phases documented
- [ ] Anti-patterns identified
- [ ] Success metrics defined

### Line Count Validation
```bash
# Compare line counts
echo "Original files:"
wc -l originals/*.md

echo "Chunked files:"
wc -l *.md | grep -v originals

# Should be roughly 2x (due to headers, cross-refs, navigation)
```
```

**Testing:**

1. **Read test:** Pick random chunk, read completely
   - Should be understandable standalone
   - Should have clear context
   - Should link to related topics

2. **Navigation test:** Start with INDEX.md
   - Follow decision tree
   - Find relevant chunk
   - Verify chunk addresses topic

3. **Claude test:** Ask Claude to implement feature
   - Prompt: "Read [chunk.md] and implement [feature]"
   - Verify Claude reads correct chunk
   - Verify Claude applies patterns correctly

**Deliverable:** Validated chunking system

---

## Success Metrics

**Quantitative:**
- **Read time:** 10-15 min (2-3 chunks) vs 60+ min (full file)
- **Context quality:** Complete section in memory vs partial recall
- **Usage rate:** 80% target vs 20% baseline
- **Hallucination:** Reduced (focused context vs overwhelmed)

**Qualitative:**
- Code comments reference specific chunks
- PRs cite chunk files
- ADRs link to chunks
- Implementation matches research patterns
- No "I forgot we had research on that" moments

---

## Maintenance

**When to re-chunk:**
- Original file grows 50%+ larger
- New major sections added
- Chunk boundaries no longer make sense

**When to update chunks:**
- Research updated (new versions)
- Breaking changes documented
- New patterns discovered

**Process:**
1. Update specific chunk (not original file)
2. Update cross-references if needed
3. Update INDEX.md decision trees if new patterns
4. Notify team in PR

---

## Example: Real-World Application

**Project:** Apex UI/UX Enhancements

**Original Research:**
- 4 files, 3,276 lines total
- Average 819 lines per file
- Too large to use effectively

**Chunking Applied:**
- 16 focused chunks created
- Average 150 lines per chunk
- INDEX.md with decision trees (334 lines)
- WORKFLOW-GUIDE.md (564 lines)
- Total system: 7,250 lines (chunks + navigation)

**Results:**
- Phase 2.5 implementation directly references chunks
- PLANNING.md links to 7 specific chunks
- Implementation guide references chunks throughout
- Estimated 80% research utilization vs 20% before

**Files:**
```
research/documentation/
├── INDEX.md                            # Master navigation
├── WORKFLOW-GUIDE.md                   # Usage workflow
├── tool-use-api.md                     # 190 lines
├── streaming-api.md                    # 266 lines
├── apex-tool-definitions.md            # 504 lines
├── tool-orchestration.md               # 474 lines
├── artifacts-layout.md                 # 437 lines
├── sheet-component.md                  # 476 lines
├── artifact-types.md                   # 570 lines
├── apex-artifacts-integration.md       # 715 lines
├── vercel-ai-sdk-overview.md           # 281 lines
├── usechat-hook.md                     # 453 lines
├── streaming-ui-patterns.md            # 363 lines
├── tool-visualization.md               # 453 lines
├── shadcn-installation.md              # 325 lines
├── component-catalog.md                # 509 lines
├── customization-guide.md              # 182 lines
├── apex-integration-strategy.md        # 154 lines
└── originals/                          # Archived originals
    ├── ai-native-ui-patterns.md        # 911 lines
    ├── claude-artifacts-ui-pattern.md  # 872 lines
    ├── claude-tool-use-and-streaming.md # 641 lines
    └── shadcn-ui-integration.md        # 850 lines
```

---

## Quick Start Template

**Use this template to apply chunking to your project:**

```bash
# 1. Create documentation folder
mkdir -p research/documentation

# 2. Analyze your large research files
# [Document findings in ANALYSIS.md]

# 3. Plan chunks
# [Create CHUNK-PLAN.md]

# 4. Create chunk files
# [Extract content, add headers]

# 5. Add cross-references
# [Link related chunks]

# 6. Create INDEX.md
# [Decision trees for navigation]

# 7. Create WORKFLOW-GUIDE.md
# [3-phase workflow documentation]

# 8. Archive originals
mkdir -p research/documentation/originals
mv [large-files].md originals/

# 9. Validate
# [Run validation checklist]

# 10. Test
# [Verify with Claude and team]
```

---

## Integration with Research-First Workflow

**This chunking workflow integrates with standard research workflow:**

1. **Research Collection** → Create large research files
2. **Documentation** → Organize findings
3. **Chunking** (NEW) → Transform into usable system
4. **Implementation** → Reference chunks during development
5. **Architecture Decisions** → Cite chunks in ADRs

**Key Benefit:** Research now accessible during Phases 3-5 (Execution → Implementation → Testing) instead of being created in Phase 2 (Mission) and forgotten.

---

## Troubleshooting

### Problem: Chunks too small (<50 lines)

**Solution:** Combine related chunks. Each chunk should be self-contained.

### Problem: Chunks too large (>300 lines)

**Solution:** Split into sub-topics. Look for natural sub-boundaries.

### Problem: Chunks not standalone

**Solution:** Add context sections. Include prerequisites and definitions.

### Problem: Cross-references unclear

**Solution:** Use descriptive link text. "For streaming → see streaming-api.md"

### Problem: INDEX.md overwhelming

**Solution:** Use decision trees, not flat lists. Guide user to correct chunk.

### Problem: Low adoption by team

**Solution:** Add to CLAUDE.md project instructions. Require chunk citations in PRs.

---

## References

**This workflow pattern based on:**
- Information architecture principles (chunking theory)
- Cognitive load theory (working memory limits ~7 items)
- User experience research (progressive disclosure)
- Technical writing best practices (DITA, topic-based authoring)

**Success case:**
- Apex UI/UX Enhancements: 80% estimated research utilization vs 20% baseline
- Implementation directly tied to research via explicit file references
- Zero hallucination issues (focused context)

---

**Last Updated:** 2025-10-21
**Version:** 1.0.0
**Status:** Battle-tested (Apex UI/UX Enhancements project)
