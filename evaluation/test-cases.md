# Test Case Templates

This document provides templates for systematically testing JIT architecture conversions.

## Test Case Template

```markdown
## Test Case: [Unique ID]

### Metadata
- **Date**: YYYY-MM-DD
- **Tester**: [Name/Handle]
- **Original System**: [Brief description]
- **Prompt Domain**: [Category]

### Original System
- **Total tokens**: [Count]
- **Structure**: [Monolithic/Partially modular]
- **Primary functions**: [List]

### JIT Architecture
- **Core prompt tokens**: [Count]
- **JIT files**: [Count]
- **File breakdown**:
  | File | Tokens | Purpose |
  |------|--------|---------|
  | [name] | [count] | [purpose] |

### Test Scenarios

#### Scenario 1: [Name]
- **Input**: [Description of test input]
- **Expected files loaded**: [List]
- **Actual files loaded**: [List]
- **Expected behavior**: [Description]
- **Actual behavior**: [Description]
- **Pass/Fail**: [Result]

### Measurements

| Metric | Value |
|--------|-------|
| Token reduction (core vs original) | X% |
| Avg tokens per session | [Count] |
| Trigger accuracy | X% |
| Functionality preservation | X% |

### Evaluation Scores
- Token Efficiency: [0-20]
- Functionality: [0-40]
- Retrieval Accuracy: [0-25]
- Maintainability: [0-15]
- **Total**: [0-100]

### Observations
[What worked well, what didn't, unexpected findings]

### Recommendations
[Suggested improvements]
```

---

## Test Scenario Categories

### Category 1: Single-Topic Queries
Test that single-topic queries load only relevant files.

### Category 2: Multi-Topic Queries
Test that complex queries correctly identify multiple relevant files.

### Category 3: Edge Cases
Test unusual or boundary scenarios.

### Category 4: Negative Cases
Test that irrelevant files are not loaded.

---

## Metrics Collection Guide

### Token Counting
- Specify tokenizer used
- Count system prompt separately
- Include file content in loaded token count

### Accuracy Measurement
```
Precision = True Positives / (True Positives + False Positives)
Recall = True Positives / (True Positives + False Negatives)
```

### Functionality Testing
- Create comprehensive test suite from original capabilities
- Verify each capability is preserved
- Document any changes

---

*Use this template to contribute validated test results.*
