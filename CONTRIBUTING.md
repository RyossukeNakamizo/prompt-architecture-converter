# Contributing to Prompt Architecture Converter

Thank you for your interest in contributing! This project benefits greatly from community input, especially empirical validation data.

## How to Contribute

### Reporting Issues

If you encounter problems or have suggestions:

1. Check existing issues to avoid duplicates
2. Create a new issue using the appropriate template
3. Provide as much context as possible

### Contributing Examples

We especially welcome real-world conversion examples:

1. **Fork the repository**
2. **Create your example** in `examples/real-world/`
3. **Include measurements** using our evaluation framework
4. **Submit a pull request**

#### Example Submission Format

```markdown
# [Domain/Use Case] Conversion Example

## Overview
- Original prompt size: X tokens
- Converted core prompt: Y tokens
- Number of JIT files: N
- Measured reduction: Z%

## Context
[Brief description of the use case]

## Original Prompt (Anonymized)
[Sanitized version of original prompt]

## Converted Architecture
[Core prompt and JIT files]

## Results
[Measured outcomes using evaluation framework]

## Observations
[What worked well, challenges encountered]
```

### Contributing Code

For framework improvements:

1. **Open an issue first** to discuss proposed changes
2. **Fork and create a feature branch**
3. **Make your changes** with clear commits
4. **Submit a pull request** with description

### Documentation Improvements

Documentation PRs are always welcome:

- Fix typos and clarify explanations
- Add examples and use cases
- Improve organization and navigation
- Translate to other languages

## Guidelines

### Code of Conduct

- Be respectful and constructive
- Focus on the work, not the person
- Help others learn and contribute

### Quality Standards

For example contributions:
- Use the evaluation framework consistently
- Anonymize any proprietary content
- Provide accurate measurements
- Document limitations and caveats

### Commit Messages

Use clear, descriptive commit messages:

```
Add: New example for [domain]
Fix: Correct calculation in evaluation rubric
Update: Clarify trigger design in documentation
```

## Recognition

Contributors will be recognized in:
- Release notes
- README acknowledgments
- Example attributions (if desired)

## Questions?

Open an issue with the `question` label if you need clarification on anything.

---

Thank you for helping improve this framework!
