# Model Selection Guidance

This document provides guidance for selecting appropriate models when implementing JIT architecture conversions. Rather than prescriptive recommendations, it offers a framework for task analysis and model matching.

## Task Analysis Framework

### Step 1: Classify Your Conversion Task

| Task Dimension | Low Complexity | High Complexity |
|----------------|----------------|-----------------|
| Original prompt size | <2,000 tokens | >10,000 tokens |
| Number of distinct workflows | 1-3 | 5+ |
| Edge case density | Few, well-defined | Many, nuanced |
| Inter-dependency level | Independent sections | Highly coupled |
| Domain specificity | General | Specialized |

### Step 2: Identify Critical Capabilities

**For JIT architecture conversion, key model capabilities include:**

1. **Structural Analysis**
   - Ability to identify logical boundaries in prompts
   - Recognition of implicit dependencies
   - Understanding of prompt design patterns

2. **Abstraction & Generalization**
   - Extracting principles from specific examples
   - Creating flexible routing logic
   - Balancing specificity with adaptability

3. **Long-Context Reasoning**
   - Maintaining coherence across large inputs
   - Tracking relationships between distant sections
   - Consistent output quality at scale

4. **Instruction Following**
   - Precise adherence to conversion methodology
   - Structured output generation
   - Format consistency

### Step 3: Match Task to Model Tier

| Task Profile | Suggested Model Tier | Rationale |
|--------------|---------------------|-----------|
| Simple, well-structured prompts | Any capable model | Straightforward extraction |
| Complex prompts with nuanced logic | Frontier models (e.g., Opus, Sonnet) | Requires sophisticated reasoning |
| High-volume batch conversions | Cost-optimized models | Efficiency at scale |
| Initial exploration/prototyping | Fast, capable models | Rapid iteration |

## Considerations by Conversion Phase

### Phase 1: Analysis

**Goal**: Understand the original prompt's structure and logic

**Model needs**:
- Strong reading comprehension
- Ability to identify patterns and categories
- Structured output capability

**Guidance**: Use the most capable model available for initial analysis. This phase sets the foundation for the entire conversion.

### Phase 2: Decomposition

**Goal**: Extract components into modular JIT files

**Model needs**:
- Consistent formatting
- Accurate content preservation
- Clear boundary identification

**Guidance**: Capable mid-tier models often suffice. Validate outputs against original for completeness.

### Phase 3: Routing Logic Design

**Goal**: Create core prompt with effective triggers

**Model needs**:
- Abstract reasoning
- Understanding of conditional logic
- Anticipation of edge cases

**Guidance**: This is often the most challenging phase. Consider using frontier models and iterating based on testing.

### Phase 4: Validation

**Goal**: Verify functionality preservation

**Model needs**:
- Consistent execution
- Ability to follow complex instructions
- Reliable output generation

**Guidance**: Test with the models that will actually use the converted architecture in production.

## Platform-Specific Notes

### Claude Projects

Claude Projects provide native support for JIT architecture:
- **Instructions**: Core prompt with routing logic
- **Project Files**: JIT files loaded on-demand
- **Memory**: Cross-conversation context persistence

**Optimal setup**:
- Keep Instructions concise with clear triggers
- Upload JIT files as markdown for easy parsing
- Use file naming conventions that signal content

### API Implementations

For API-based implementations:
- Consider system prompt caching for core prompts
- Implement retrieval logic in application code
- Monitor actual token usage to validate efficiency gains

### Other Platforms

JIT principles apply across platforms, but implementation varies:
- Some platforms support file attachments
- Others require inline context
- Adapt architecture to platform capabilities

## Cost-Benefit Analysis

### When JIT Architecture Provides Value

✅ **Good candidates**:
- Long prompts with situationally-relevant sections
- Multi-workflow systems with distinct paths
- Prompts with extensive examples or edge cases
- High-volume applications where token savings matter

❌ **Poor candidates**:
- Short, focused prompts (<500 tokens)
- Highly interdependent instructions
- Prompts where all content is usually relevant
- Low-volume applications where complexity cost exceeds savings

### ROI Calculation Framework

```
Potential Savings = (Current Tokens - Projected Tokens) × Usage Volume × Token Cost

Implementation Cost = Development Time + Testing Time + Maintenance Overhead

ROI = Potential Savings / Implementation Cost
```

*Note: Actual values depend on specific use case and implementation quality.*

## Recommendations Summary

1. **Start with analysis**: Use capable models to understand your prompt before converting
2. **Match model to phase**: Different conversion phases have different requirements
3. **Test with production models**: Validate on the models that will actually use the architecture
4. **Iterate based on results**: Refine routing logic based on observed retrieval patterns
5. **Consider platform constraints**: Adapt implementation to your target platform

## Further Resources

- [Evaluation Framework](evaluation-framework.md) - Systematic testing methodology
- [Theory](theory.md) - Theoretical foundations
- [Examples](../examples/) - Sample conversions

---

*This guidance is intended to help you make informed decisions about model selection. Optimal choices depend on your specific context, requirements, and constraints.*
