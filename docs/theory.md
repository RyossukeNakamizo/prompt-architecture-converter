# Theoretical Foundations

This document outlines the theoretical basis for JIT prompt architecture, based on published research on context engineering and LLM behavior.

## Core Principles

### Context as Finite Resource

Anthropic's research identifies that LLMs, despite handling large context windows, experience performance degradation as token count increases—a phenomenon termed "context rot." This stems from fundamental architectural constraints:

**Attention Budget Constraints**
- Transformers enable every token to attend to every other token, creating n² pairwise relationships
- As context grows, the model's ability to capture these relationships gets stretched thin
- Models have more training experience with shorter sequences than longer ones

**Implication**: Context must be treated as a finite resource with diminishing marginal returns.

### Just-in-Time Context Retrieval

Rather than pre-processing all relevant data upfront, JIT approaches maintain lightweight identifiers and dynamically load data at runtime.

From Anthropic's engineering documentation:

> "Agents built with the 'just in time' approach maintain lightweight identifiers (file paths, stored queries, web links, etc.) and use these references to dynamically load data into context at runtime using tools."

**Key Benefits**:
1. **Storage efficiency**: Only relevant context consumes attention budget
2. **Metadata signals**: File names, folder hierarchies, and timestamps provide contextual hints
3. **Progressive disclosure**: Understanding builds layer by layer

### The Goldilocks Zone

Effective prompts must navigate between two failure modes:

| Extreme | Characteristic |
|---------|----------------|
| Too Specific | Hardcoded, brittle logic that creates fragility |
| Too Vague | High-level guidance that fails to provide concrete signals |

The optimal approach provides strong heuristics that are specific enough to guide behavior yet flexible enough to adapt to novel situations.

## Architectural Principles

### Minimal High-Signal Context

The guiding principle from Anthropic's research:

> "Good context engineering means finding the smallest possible set of high-signal tokens that maximize the likelihood of some desired outcome."

This translates to:
- Core prompts should contain only essential routing logic
- Detailed instructions loaded on-demand when relevant
- Examples retrieved based on task classification

### Hybrid Retrieval Strategy

Effective agents may employ hybrid approaches:

> "The most effective agents might employ a hybrid strategy, retrieving some data up front for speed, and pursuing further autonomous exploration at its discretion."

**Framework Implementation**:
- Critical context (core workflow, primary constraints) loaded upfront
- Situational context (specific examples, edge cases) retrieved JIT
- Exploration enabled for novel situations

### Separation of Concerns

Tools and context components should follow clean design principles:
- Self-contained and robust to error
- Minimal overlap in functionality
- Clear, unambiguous intended use

## Theoretical Token Reduction Model

### Hypothesis

If a monolithic prompt contains:
- **Essential instructions**: Required for every interaction (~20% of tokens)
- **Situational context**: Needed for specific task types (~60% of tokens)
- **Edge cases**: Rarely needed (~20% of tokens)

Then JIT architecture should theoretically reduce average token usage by:
- **Best case**: 70-95% (simple, well-classified tasks)
- **Typical case**: 40-60% (mixed task complexity)
- **Worst case**: 0-20% (tasks requiring most context)

### Assumptions

This model assumes:
1. Tasks can be reliably classified at conversation start
2. JIT triggers accurately identify needed context
3. Retrieval overhead is minimal compared to context savings
4. Model performance is preserved with modular context

*Note: These are hypotheses requiring empirical validation.*

## Limitations and Open Questions

### Known Limitations

1. **Retrieval Latency**: Dynamic loading may introduce delays
2. **Classification Errors**: Incorrect task routing loads wrong context
3. **Context Dependencies**: Some instructions may require others as prerequisites
4. **Platform Constraints**: Not all LLM platforms support modular context loading

### Open Research Questions

- What is the optimal granularity for JIT file decomposition?
- How do different models respond to modular vs. monolithic context?
- What classification strategies minimize routing errors?
- How does JIT architecture interact with model context caching?

## References

### Primary Sources

- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) (2025)
- [Anthropic: Building effective AI agents](https://www.anthropic.com/research/building-effective-agents) (2024)

### Related Research

- [Microsoft Research: LLMLingua - Compressing Prompts for Accelerated Inference](https://arxiv.org/abs/2310.05736) (2023)
- Context window utilization studies (needle-in-haystack benchmarks)

---

*This document presents theoretical foundations. Empirical validation is ongoing.*
