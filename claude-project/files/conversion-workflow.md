# Conversion Workflow

This file contains the detailed methodology for converting monolithic prompts to JIT architecture.

## Phase 1: Structural Analysis

### 1.1 Initial Assessment

Examine the original prompt to identify:

**Content Categories**:
- Core identity and role definition
- Primary workflows and procedures
- Examples and demonstrations
- Edge cases and exceptions
- Constraints and guardrails
- Output formatting requirements

**Structural Patterns**:
- Section delimiters (XML tags, markdown headers, etc.)
- Conditional logic (if-then statements)
- Reference relationships between sections
- Repetition and redundancy

### 1.2 Dependency Mapping

Create a dependency graph:

```
[Section A] ──requires──▶ [Section B]
[Section C] ──optional──▶ [Section D]
[Section E] ──standalone──
```

**Questions to answer**:
- Which sections are always needed?
- Which sections are mutually exclusive?
- Which sections have prerequisites?
- Which sections are truly standalone?

### 1.3 Usage Pattern Analysis

Estimate usage frequency for each section:

| Frequency | Description | JIT Strategy |
|-----------|-------------|--------------|
| Always | Every interaction | Keep in core |
| Often | Most interactions | Consider core or eager load |
| Sometimes | Specific task types | JIT with clear trigger |
| Rarely | Edge cases only | JIT with specific trigger |

## Phase 2: Architecture Design

### 2.1 Core Prompt Design

The core prompt should contain:

✅ **Include**:
- Essential identity/role
- High-level capability overview
- Routing logic with triggers
- Universal constraints
- Output format skeleton

❌ **Exclude**:
- Detailed procedures (move to JIT)
- Extensive examples (move to JIT)
- Edge case handling (move to JIT)
- Domain-specific knowledge (move to JIT)

### 2.2 JIT File Organization

Recommended file structure:

```
files/
├── workflows/
│   ├── primary-workflow.md
│   ├── secondary-workflow.md
│   └── edge-case-handling.md
├── examples/
│   ├── standard-examples.md
│   └── complex-examples.md
├── domain/
│   ├── domain-knowledge.md
│   └── terminology.md
└── constraints/
    └── detailed-constraints.md
```

### 2.3 Trigger Design

Effective triggers should be:

**Specific**: Clearly identify when to load
**Observable**: Based on explicit user signals
**Non-overlapping**: Each trigger maps to one file
**Complete**: Cover all usage scenarios

**Trigger patterns**:
```
When user mentions [keyword/phrase] → Load [file]
When task type is [category] → Load [file]
When output requires [format] → Load [file]
When edge case [condition] → Load [file]
```

## Phase 3: Content Extraction

### 3.1 Extraction Protocol

For each section being extracted:

1. **Identify boundaries**: Clear start and end points
2. **Check dependencies**: Note any required context
3. **Preserve formatting**: Maintain original structure
4. **Add context header**: Document when/why to use
5. **Define trigger**: Specify loading conditions

### 3.2 JIT File Template

```markdown
# [File Name]

## Trigger Conditions
- Load when: [specific conditions]
- Related files: [if applicable]

## Content

[Extracted content here]

## Usage Notes
[Any context needed for proper application]
```

### 3.3 Content Transformation

Sometimes extraction requires transformation:

| Original Pattern | Transformation |
|------------------|----------------|
| Inline examples | Consolidate into examples file |
| Scattered edge cases | Group by category |
| Redundant instructions | Deduplicate, reference once |
| Implicit logic | Make explicit in routing |

## Phase 4: Integration

### 4.1 Core Prompt Assembly

Structure the core prompt:

```markdown
# [Role/Identity]

[1-2 sentence role definition]

## Capabilities
[Brief capability list]

## Context Loading
[Trigger table or logic]

## Universal Guidelines
[Always-applicable constraints]

## Output Format
[Basic format template]
```

### 4.2 Cross-Reference Validation

Verify:
- [ ] All original content is represented
- [ ] No circular dependencies between JIT files
- [ ] Triggers cover all scenarios
- [ ] No orphaned content

### 4.3 Documentation

Create supporting documentation:
- Architecture overview diagram
- Trigger quick-reference
- Maintenance notes
- Version history

## Phase 5: Validation

### 5.1 Functionality Testing

Test scenarios:
1. Common use cases → Should work with minimal JIT loading
2. Complex use cases → Appropriate files should load
3. Edge cases → Correct edge case file should load
4. Invalid inputs → Graceful handling

### 5.2 Token Efficiency Verification

Measure:
- Baseline: Original prompt token count
- Core: New core prompt token count
- Average JIT: Mean tokens loaded per task type
- Reduction: Calculate percentage savings

### 5.3 Iteration

Based on testing results:
- Adjust trigger specificity
- Rebalance core vs. JIT content
- Consolidate or split files as needed
- Refine routing logic

---

*Refer to `extraction-patterns.md` for common patterns and `examples.md` for demonstrations.*
