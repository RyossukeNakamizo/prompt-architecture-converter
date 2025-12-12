# Scoring Rubric

This rubric provides consistent criteria for evaluating JIT architecture conversions.

## Overview

| Dimension | Max Points | Weight |
|-----------|------------|--------|
| Token Efficiency | 20 | 20% |
| Functionality Preservation | 40 | 40% |
| Retrieval Accuracy | 25 | 25% |
| Maintainability | 15 | 15% |
| **Total** | **100** | **100%** |

---

## Token Efficiency (20 points)

Measures the token savings achieved by the conversion.

| Score | Criteria |
|-------|----------|
| 20 | >80% reduction with full functionality |
| 18 | 70-80% reduction with full functionality |
| 15 | 60-70% reduction with full functionality |
| 12 | 50-60% reduction with full functionality |
| 10 | 40-50% reduction with full functionality |
| 5 | 20-40% reduction |
| 0 | <20% reduction or functionality loss |

### Calculation

```
Reduction % = (Original - Average_Session) / Original × 100

Where:
- Original = Total tokens in monolithic prompt
- Average_Session = Core + weighted average of JIT files loaded
```

### Notes
- Measure across representative task distribution
- Weight by actual usage frequency if known
- Account for multi-file loading scenarios

---

## Functionality Preservation (40 points)

Measures whether the converted architecture maintains all original capabilities.

| Score | Criteria |
|-------|----------|
| 40 | 100% test cases pass, output quality maintained or improved |
| 35 | 98%+ test cases pass, negligible quality variations |
| 30 | 95%+ test cases pass, minor quality variations |
| 25 | 90%+ test cases pass, acceptable quality |
| 20 | 85%+ test cases pass, noticeable but acceptable degradation |
| 10 | 80%+ test cases pass, significant degradation |
| 0 | <80% test cases pass or critical failures |

### Testing Protocol

1. Identify all capabilities in original prompt
2. Create test cases for each capability
3. Execute tests with converted architecture
4. Compare outputs for semantic equivalence

### Quality Assessment

- **Output completeness**: All required elements present
- **Accuracy**: Information is correct
- **Consistency**: Similar inputs yield similar quality
- **Edge case handling**: Unusual scenarios handled appropriately

---

## Retrieval Accuracy (25 points)

Measures how accurately the system loads appropriate JIT files.

| Score | Criteria |
|-------|----------|
| 25 | >95% precision AND >95% recall |
| 22 | >95% precision OR >95% recall, other >90% |
| 20 | >90% precision AND >90% recall |
| 15 | >85% precision AND >85% recall |
| 10 | >80% precision AND >80% recall |
| 5 | >75% precision OR >75% recall |
| 0 | <75% precision AND <75% recall |

### Definitions

**Precision**: Of files loaded, what percentage were actually needed?
```
Precision = Correctly_Loaded / Total_Loaded
```

**Recall**: Of files needed, what percentage were loaded?
```
Recall = Correctly_Loaded / Total_Needed
```

### Measurement Protocol

1. Define ground truth: Which files should load for each test case
2. Execute test cases
3. Record actual files loaded
4. Calculate precision and recall

---

## Maintainability (15 points)

Measures the long-term viability of the architecture.

| Score | Criteria |
|-------|----------|
| 15 | Excellent: Clear separation, self-documenting, trivial updates |
| 12 | Good: Clean separation, good documentation, easy updates |
| 10 | Acceptable: Adequate separation, reasonable documentation |
| 7 | Fair: Some coupling, documentation gaps |
| 5 | Poor: Significant coupling, unclear organization |
| 0 | Unacceptable: High coupling, no documentation, brittle |

### Assessment Criteria

**Separation of Concerns**
- [ ] Each file has single, clear purpose
- [ ] Minimal dependencies between files
- [ ] Changes isolated to relevant files

**Documentation Quality**
- [ ] Clear trigger conditions documented
- [ ] File purposes explained
- [ ] Dependencies noted

**Update Ease**
- [ ] Adding new functionality is straightforward
- [ ] Modifying existing content doesn't break others
- [ ] Routing logic is comprehensible

---

## Total Score Interpretation

| Score Range | Rating | Interpretation |
|-------------|--------|----------------|
| 90-100 | Excellent | Production-ready, exemplary conversion |
| 80-89 | Good | Production-ready with minor improvements possible |
| 70-79 | Acceptable | Usable, but improvements recommended |
| 60-69 | Needs Work | Significant improvements required |
| 50-59 | Poor | Major revision needed |
| <50 | Inadequate | Consider alternative approach |

---

## Scoring Worksheet

```markdown
## Conversion Scoring

### Basic Information
- Project: [Name]
- Date: [Date]
- Evaluator: [Name]

### Token Efficiency [__/20]
- Original tokens: ____
- Core prompt tokens: ____
- Avg session tokens: ____
- Reduction: ____%
- Score justification: 

### Functionality Preservation [__/40]
- Test cases total: ____
- Test cases passed: ____
- Pass rate: ____%
- Quality notes:
- Score justification:

### Retrieval Accuracy [__/25]
- Precision: ____%
- Recall: ____%
- Score justification:

### Maintainability [__/15]
- Separation: [Poor/Fair/Good/Excellent]
- Documentation: [Poor/Fair/Good/Excellent]
- Update ease: [Poor/Fair/Good/Excellent]
- Score justification:

### Total Score: [__/100]

### Summary
[Overall assessment and recommendations]
```

---

*Use this rubric consistently across all evaluations for comparable results.*
