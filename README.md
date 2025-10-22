# Workflow Documentation

This directory contains all workflow documentation for the Apex Memory System Development project.

---

## Available Workflows

### 1. Features Implementation Workflow

**📘 [FEATURES-IMPLEMENTATION-WORKFLOW.md](./FEATURES-IMPLEMENTATION-WORKFLOW.md)**

The comprehensive, battle-tested workflow for implementing major features.

**Use for:**
- Major feature implementations (multi-week, multi-phase)
- System upgrades requiring research
- Features touching multiple components
- Anything requiring deployment planning

**Don't use for:**
- Bug fixes (too heavyweight)
- Simple code changes
- Quick patches

**Quick start:** [FEATURES-QUICK-START.md](./FEATURES-QUICK-START.md)
**Checklist:** [PHASE-IMPLEMENTATION-CHECKLIST.md](./PHASE-IMPLEMENTATION-CHECKLIST.md)

**Success story:** Query Router Upgrade (October 2025)
- 8 research documents
- 20+ implementation files
- 30+ tests
- 8 deployment examples
- Zero rework required

---

## 📖 Session Continuity & Handoffs

### Handoff Workflow Format

**📘 [HANDOFF-WORKFLOW-FORMAT.md](./HANDOFF-WORKFLOW-FORMAT.md)**

The proven format for managing multi-day/multi-week development with Claude Code, enabling zero context loss across sessions.

**Use for:**
- Multi-day implementations (2+ days)
- Multi-week projects (phased development)
- Complex features requiring architectural decisions
- Projects needing session-to-session continuity

**Key Features:**
- ✅ Zero context loss across sessions
- ✅ Copy-paste "Start Command" for instant continuation
- ✅ Complete traceability (decisions, fixes, patterns)
- ✅ Baseline test preservation tracking
- ✅ Architecture decision documentation

**Success Story:** Graphiti + JSON Integration (Week 3)
- 3-day handoff created (HANDOFF-WEEK3-DAYS1-3.md)
- Next session: Instant continuation using "Start Command"
- 11 tests created, 100% pass rate
- All architectural decisions preserved
- Zero time re-discovering context

**Components:**
1. **Handoff Documents** - Complete session-to-session continuity
2. **Quick Reference** - Fast pattern/command lookup
3. **Progress Tracking** - Updated after each day
4. **Handoff Index** - Chronological progression

---

## 📚 Research Documentation Management

### Documentation Chunking Workflow

**📘 [base-structure/research/DOCUMENTATION-CHUNKING-WORKFLOW.md](./base-structure/research/DOCUMENTATION-CHUNKING-WORKFLOW.md)**

Transform large research documents (500+ lines) into usable, workflow-integrated documentation systems.

**The Problem:**
- Large research files (3,000+ lines) → context loss, hallucinations, low utilization (~20%)
- Developers overwhelmed by massive files → research gets created but never used
- Claude reads partial content → incomplete patterns, incorrect implementations

**The Solution:**
- Chunk documentation into focused files (~150 lines each)
- Create INDEX.md with decision tree navigation
- Create WORKFLOW-GUIDE.md for structured usage during development
- Archive originals, maintain cross-references

**Success Metrics:**
- ✅ 80% research utilization (vs 20% without chunking)
- ✅ Focused context → No hallucinations
- ✅ 10-15 min read time (vs 60+ min for full file)
- ✅ Research actually gets used during implementation

**When to Apply:**
- ✅ Research document exceeds 500 lines
- ✅ Document covers multiple distinct topics
- ✅ Research completed and ready for implementation
- ✅ Team needs to reference research during development

**Real-World Example:** Apex UI/UX Enhancements
- **Before:** 4 files, 3,276 lines total (avg 819 lines/file)
- **After:** 16 focused chunks (~150 lines each) + navigation system
- **Result:** Phase 2.5 implementation directly references 7 specific chunks
- **Impact:** Research-backed implementation with explicit file citations

**8-Step Workflow:**
1. Analyze structure → Identify topic boundaries
2. Plan chunks → 4-6 chunks per original file
3. Create chunks → Extract content, add headers
4. Add cross-references → Link related chunks
5. Create INDEX.md → Decision tree navigation
6. Create WORKFLOW-GUIDE.md → Usage during development
7. Archive originals → Preserve history
8. Validate & test → Ensure no information lost

---

## Workflow Components

### Documentation

| Document | Purpose | When to Use |
|----------|---------|-------------|
| [FEATURES-IMPLEMENTATION-WORKFLOW.md](./FEATURES-IMPLEMENTATION-WORKFLOW.md) | Complete workflow guide | Read once, reference during implementation |
| [FEATURES-QUICK-START.md](./FEATURES-QUICK-START.md) | One-page cheat sheet | Quick reference during active work |
| [PHASE-IMPLEMENTATION-CHECKLIST.md](./PHASE-IMPLEMENTATION-CHECKLIST.md) | Detailed phase checklist | Use for each implementation phase |
| [HANDOFF-WORKFLOW-FORMAT.md](./HANDOFF-WORKFLOW-FORMAT.md) | Session continuity format | Multi-day/multi-week projects |
| [base-structure/research/DOCUMENTATION-CHUNKING-WORKFLOW.md](./base-structure/research/DOCUMENTATION-CHUNKING-WORKFLOW.md) | Research documentation management | Large research files (500+ lines) |

### Templates

All templates are in [`templates/features/`](./templates/features/):

| Template | Purpose |
|----------|---------|
| [IMPROVEMENT-PLAN-TEMPLATE.md](./templates/features/IMPROVEMENT-PLAN-TEMPLATE.md) | Comprehensive feature specification |
| [IMPLEMENTATION-GUIDE-TEMPLATE.md](./templates/features/IMPLEMENTATION-GUIDE-TEMPLATE.md) | Step-by-step implementation guide |
| [DEPLOYMENT-GUIDE-TEMPLATE.md](./templates/features/DEPLOYMENT-GUIDE-TEMPLATE.md) | Deployment procedures |
| [README-TEMPLATE.md](./templates/features/README-TEMPLATE.md) | Feature overview and progress tracking |
| [PHASE-README-TEMPLATE.md](./templates/features/PHASE-README-TEMPLATE.md) | Per-phase documentation |

---

## The Features Implementation Workflow

### Overview

A **7-phase, research-first workflow** that ensures production-ready features with zero rework.

```
Phase 0: Identify → Phase 1: RDF → Phases 2-5: Implement → Phase 6: Deploy Docs → Phase 7: Ship
   (1 day)          (1 week)         (4-6 weeks)            (1 week)            (ongoing)
```

### Key Success Factors

✅ **Research-first** → Better decisions
✅ **Plan mode first** → Aligned approach
✅ **Proactive tests** → Quality without asking
✅ **Context compact** → Prevents overflow
✅ **Examples alongside** → Usable immediately
✅ **Docs as you go** → Never falls behind
✅ **Deployment manual last** → Complete operational guide

### The Phase Implementation Pattern

For each implementation phase (Phases 2-5):

1. 🛑 **Enter Plan Mode** - Pause before coding
2. 💬 **Discuss Requirements** - What do we need?
3. 📚 **Fill Research Gaps** - Get missing info
4. ▶️ **Exit Plan Mode** - Ready to execute
5. 💻 **Write Code** - Real working code (3-5 files)
6. ✨ **Generate Tests** - Proactively! (15-30 tests)
7. 📝 **Create Examples** - Copy-paste ready
8. 📄 **Update Docs** - Phase README, CHANGELOG
9. 🗜️ **Context Compact** - Before next phase (critical!)
10. ✅ **Mark Complete** - Phase done, ready for next

### Timeline (Major Feature)

```
Week 1:   Phase 1 (RDF)                    → 8 research docs
Week 2-3: Phase 2 (Foundation)             → Code + 15 tests → COMPACT
Week 3-4: Phase 3 (Intelligent Features)   → Code + 15 tests → COMPACT
Week 5-6: Phase 4 (Advanced Features)      → Code + 15 tests → COMPACT
Week 7:   Phase 5 (Polish)                 → Code + 15 tests → COMPACT
Week 8:   Phase 6 (Deployment Manual)      → 4 guides + 8 examples
Week 8+:  Phase 7 (Ship)                   → Deploy + monitor

Total: 8 weeks for major feature
Context compacts: 4 (critical!)
```

---

## Quick Decision Tree

```
Starting work?
├─ Major feature (multi-week)?
│  └─ Use Features Implementation Workflow
│
├─ Bug fix?
│  └─ Use regular development flow (not this workflow)
│
├─ Simple change?
│  └─ Use regular development flow (not this workflow)
│
└─ Research needed?
   └─ Start with Phase 1 (RDF)

During implementation?
├─ Starting new phase?
│  └─ Enter plan mode first!
│
├─ Just finished coding?
│  └─ Generate tests proactively
│
├─ Phase complete?
│  └─ Context compact!
│
└─ All phases done?
   └─ Create deployment manual

Ready to ship?
├─ All tests passing?
│  └─ Create deployment guides
│
├─ Guides complete?
│  └─ Final commit
│
├─ Deployed?
│  └─ Move to completed/
│
└─ Done! 🎉
```

---

## Getting Started

### For a New Feature

1. **Read the workflow guide:**
   ```bash
   open workflow/FEATURES-IMPLEMENTATION-WORKFLOW.md
   ```

2. **Create feature directory:**
   ```bash
   mkdir -p upgrades/planned/[feature-name]
   ```

3. **Copy templates:**
   ```bash
   cp workflow/templates/features/IMPROVEMENT-PLAN-TEMPLATE.md upgrades/planned/[feature-name]/IMPROVEMENT-PLAN.md
   cp workflow/templates/features/README-TEMPLATE.md upgrades/planned/[feature-name]/README.md
   ```

4. **Start Phase 0 (Identification):**
   - Fill in README.md with problem statement
   - Define high-level scope
   - Get stakeholder buy-in

5. **Execute Phase 1 (RDF):**
   ```bash
   # Option A: Automated
   /rdf [feature-name]

   # Option B: Manual research + documentation
   ```

6. **Follow the 7-phase workflow:**
   - Use [FEATURES-QUICK-START.md](./FEATURES-QUICK-START.md) as guide
   - Use [PHASE-IMPLEMENTATION-CHECKLIST.md](./PHASE-IMPLEMENTATION-CHECKLIST.md) for each phase
   - Create deployment manual in Phase 6
   - Ship in Phase 7

---

## Quality Standards

### Research Phase

- ✅ Minimum 8 research documents
- ✅ All sources Tier 1-2 (official docs, 1.5k+ star repos)
- ✅ Latest versions verified
- ✅ Complete comparison tables

### Implementation Phase

- ✅ 20+ implementation files
- ✅ 30+ tests (generated proactively!)
- ✅ 80%+ code coverage
- ✅ All async where appropriate

### Example Quality

- ✅ 8+ deployment examples
- ✅ Copy-paste ready
- ✅ No placeholders or TODOs

### Documentation Quality

- ✅ 100% coverage
- ✅ Deployment guide complete
- ✅ Testing guide complete
- ✅ Troubleshooting guide complete

---

## Success Stories

### Query Router Upgrade (October 2025)

**The workflow in action:**

- **Research Phase:** 8 comprehensive research documents (40,000+ words)
- **Implementation:** 4 phases, each with plan mode → code → tests → compact
- **Tests:** 30+ tests generated proactively (never asked!)
- **Context Compacts:** 4 successful compacts (prevented overflow)
- **Deployment:** Complete manual with 4 guides + 8 examples
- **Result:** Production-ready with zero rework

**Timeline:**
- Planned: 8 weeks
- Actual: 8 weeks
- Rework: 0 weeks

**Quality:**
- Documentation: 100% complete
- Tests: 100% passing
- Examples: 100% working
- Deployment: Successful

**Lessons learned:**
- ✅ Plan mode discussions prevented rework
- ✅ Proactive test generation caught bugs early
- ✅ Context compacts kept conversation manageable
- ✅ Deployment manual enabled smooth rollout

---

## Contributing

When adding new workflows:

1. Create main workflow document
2. Create quick-start guide
3. Create templates
4. Add to this README
5. Test with real feature implementation
6. Document lessons learned

---

## Related Resources

### Internal
- [RDF Workflow Guide](../.claude/RDF-WORKFLOW-GUIDE.md) - Automated research workflow
- [Upgrades README](../upgrades/README.md) - Upgrade tracking system
- [Research README](../research/README.md) - Research organization

### Templates
- [Feature Templates](./templates/features/) - All feature templates
- [Example Feature](../upgrades/completed/query-router/) - Complete example

---

## FAQ

**Q: When should I use the Features Implementation Workflow?**

A: Use it for major features that:
- Span multiple weeks (4-8 weeks typical)
- Require research phase
- Touch multiple components
- Need deployment planning
- Require comprehensive testing

**Q: Can I use this workflow for bug fixes?**

A: No, it's too heavyweight. Bug fixes should use the regular development flow.

**Q: What if I skip the plan mode discussion?**

A: You'll likely miss requirements and need rework. Plan mode catches issues before coding.

**Q: What if I skip context compaction?**

A: Context will overflow and you'll lose conversation continuity. Compact after EVERY phase.

**Q: What if I don't generate tests proactively?**

A: Quality will suffer and bugs will reach production. Generate 15-30 tests per phase WITHOUT being asked.

**Q: Can I skip the deployment manual?**

A: No. Without it, nobody can safely deploy your feature. Create it in Phase 6.

---

## Maintenance

This workflow documentation should be updated:
- After each successful feature implementation
- When lessons are learned
- When patterns are discovered
- When templates need improvements

**Last Updated:** October 2025
**Version:** 1.0
**Status:** Production-Ready

---

**This workflow has been battle-tested and is ready for use on any major feature implementation.**
