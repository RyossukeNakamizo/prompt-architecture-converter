# Prompt Architecture Converter

![Status](https://img.shields.io/badge/status-experimental-yellow)
![Validation](https://img.shields.io/badge/validation-pending-orange)

A framework for converting monolithic system prompts into modular Just-in-Time (JIT) architectures, based on Anthropic's context engineering research.

## Status: Experimental Framework

⚠️ **Important**: This is an experimental framework. Token reduction estimates (70-95%) are theoretical targets based on architectural principles, not empirically validated results.

## Overview

Context is a finite resource for AI agents. Anthropic's research demonstrates that LLMs experience "context rot" as token count increases—the model's ability to accurately recall information decreases with context length.

JIT architecture maintains lightweight references and loads context on-demand. As described in Anthropic's engineering documentation, agents can "maintain lightweight identifiers (file paths, stored queries, web links, etc.) and use these references to dynamically load data into context at runtime."

## Theoretical Performance Targets

| Metric | Target Range | Notes |
|--------|--------------|-------|
| Core prompt size | 150-200 tokens | Design goal |
| Token reduction | 70-95% | Varies by use case |
| JIT files | 4-6 files | Optimal range for most applications |

*These are architectural targets. Empirical validation planned for future releases.*

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    Original Monolithic Prompt                │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ All instructions, examples, edge cases, workflows   │    │
│  │ loaded upfront regardless of relevance              │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                              ↓
                    JIT Architecture Conversion
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                    JIT Architecture                          │
│  ┌──────────────┐    ┌──────────────────────────────────┐   │
│  │ Core Prompt  │    │        JIT Files (on-demand)     │   │
│  │ (minimal)    │───▶│  • workflows.md                  │   │
│  │              │    │  • examples.md                   │   │
│  │ Triggers +   │    │  • edge-cases.md                 │   │
│  │ Routing      │    │  • domain-knowledge.md           │   │
│  └──────────────┘    └──────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

## Key Concepts

### Just-in-Time Context Retrieval

Rather than pre-loading all information, JIT systems maintain lightweight identifiers and retrieve context dynamically. This approach:
- Preserves attention budget for relevant information
- Enables progressive disclosure of context
- Aligns with cognitive load management principles

### Progressive Disclosure

Agents incrementally discover relevant context through exploration. Each interaction yields signals (file names, structures, timestamps) that inform the next decision, allowing understanding to build layer by layer.

### Hybrid Strategy

The framework supports combining pre-computed retrieval with autonomous exploration—using upfront loading for critical context while enabling just-in-time retrieval for situational needs.

## Quick Start

### Using Claude Projects

1. Create a new Claude Project
2. Add the core prompt from `claude-project/instructions.md` to Project Instructions
3. Upload JIT files from `claude-project/files/` to Project Files
4. Test with sample conversions

### Conversion Process

1. **Analyze** your existing monolithic prompt
2. **Identify** separable components (workflows, examples, edge cases)
3. **Extract** into modular JIT files with clear triggers
4. **Design** routing logic in the core prompt
5. **Validate** functionality preservation

## Repository Structure

```
prompt-architecture-converter/
├── README.md                     # This file
├── LICENSE                       # MIT License
├── CONTRIBUTING.md               # Contribution guidelines
├── claude-project/
│   ├── instructions.md           # Core prompt for Claude Projects
│   └── files/                    # JIT files to upload
│       ├── conversion-workflow.md
│       ├── extraction-patterns.md
│       ├── optimization-guidelines.md
│       └── examples.md
├── docs/
│   ├── theory.md                 # Theoretical foundations
│   ├── evaluation-framework.md   # Evaluation methodology
│   └── model-guidance.md         # Model selection guidance
├── examples/
│   ├── before-after/             # Conversion examples
│   └── real-world/               # Community contributions
└── evaluation/
    ├── test-cases.md             # Test case templates
    └── scoring-rubric.md         # Evaluation criteria
```

## Validation Status

This framework has not yet been empirically validated. We welcome community contributions:

- [ ] Conversion case studies with measured token counts
- [ ] Before/after functionality comparisons
- [ ] Performance benchmarks across different prompt types
- [ ] Edge case documentation

## Validation Roadmap

- [x] v1.0: Framework release (current)
- [ ] v1.1: Community-contributed test cases
- [ ] v1.2: Empirical validation on 5+ real-world prompts
- [ ] v2.0: Validated performance benchmarks

## Contributing

We welcome contributions. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Particularly valuable contributions:
- Real-world conversion examples with measured results
- Edge cases and failure modes
- Alternative architectural patterns
- Documentation improvements

## Disclaimer

This framework is released as an experimental tool for the AI engineering community. The architectural patterns are derived from Anthropic's published research on context engineering, but specific performance claims have not been independently validated.

## License

MIT License - See [LICENSE](LICENSE) for details.

## References

- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) (2025)
- [Anthropic: Building effective AI agents](https://www.anthropic.com/research/building-effective-agents) (2024)
- [Microsoft Research: LLMLingua - Compressing Prompts for Accelerated Inference](https://arxiv.org/abs/2310.05736) (2023)
