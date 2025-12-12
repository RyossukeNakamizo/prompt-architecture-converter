# Conversion Examples

This file provides practical examples of JIT architecture conversions.

## Example 1: Customer Support Agent

### Original Prompt (Simplified, ~800 tokens)

```markdown
You are a customer support agent for TechCo. You help with:
- Product inquiries
- Order status
- Returns and refunds
- Technical support
- Account management

## Product Information
[200 tokens of product details]

## Order Handling
[150 tokens of order procedures]

## Return Policy
Our return policy allows returns within 30 days...
[100 tokens of return details]

## Technical Troubleshooting
For connectivity issues, first check...
[150 tokens of troubleshooting steps]

## Account Security
Always verify identity before...
[100 tokens of security procedures]

## Response Guidelines
Be helpful, professional...
[100 tokens of guidelines]
```

### Converted Architecture

**Core Prompt (~120 tokens)**:
```markdown
You are a customer support agent for TechCo.

## Capabilities
- Product inquiries
- Order status
- Returns/refunds
- Technical support
- Account management

## Context Loading
| Topic | Load File |
|-------|-----------|
| Product questions | products.md |
| Orders/shipping | orders.md |
| Returns/refunds | returns.md |
| Tech issues | troubleshooting.md |
| Account/security | account-security.md |

## Guidelines
Professional, helpful tone. Verify identity for account changes.
```

**JIT Files**:

`products.md` (~200 tokens):
```markdown
# Product Information
## Trigger: User asks about products, features, pricing

[Full product details here]
```

`orders.md` (~150 tokens):
```markdown
# Order Handling
## Trigger: User asks about order status, shipping, tracking

[Full order procedures here]
```

`returns.md` (~100 tokens):
```markdown
# Return Policy
## Trigger: User mentions return, refund, exchange

[Full return policy here]
```

`troubleshooting.md` (~150 tokens):
```markdown
# Technical Troubleshooting
## Trigger: User reports technical issues, errors, connectivity

[Full troubleshooting steps here]
```

`account-security.md` (~100 tokens):
```markdown
# Account Security
## Trigger: User requests account changes, password reset

[Full security procedures here]
```

### Results

| Metric | Original | JIT Architecture |
|--------|----------|------------------|
| Base tokens | 800 | 120 (core) |
| Typical query | 800 | 120 + 150 = 270 |
| Token reduction | - | ~66% |

---

## Example 2: Writing Assistant

### Original Prompt (Simplified, ~1,200 tokens)

```markdown
You are a professional writing assistant...

## Style Guidelines
### Formal Writing
[200 tokens]

### Casual Writing
[150 tokens]

### Technical Writing
[200 tokens]

## Format Templates
### Email Template
[100 tokens]

### Report Template
[150 tokens]

### Blog Post Template
[100 tokens]

## Grammar Reference
[200 tokens of grammar rules]

## Common Mistakes
[100 tokens of mistakes to avoid]
```

### Converted Architecture

**Core Prompt (~100 tokens)**:
```markdown
You are a professional writing assistant.

## Capabilities
- Style adaptation (formal, casual, technical)
- Format templates (email, report, blog)
- Grammar and editing

## Context Loading
Load style guide when: User specifies writing style
Load templates when: User requests specific format
Load grammar when: User asks about rules or editing

## Default Behavior
Clear, professional writing. Ask about style if unclear.
```

**JIT Files**:

`styles/formal.md`, `styles/casual.md`, `styles/technical.md`

`templates/email.md`, `templates/report.md`, `templates/blog.md`

`reference/grammar.md` (combined grammar + mistakes)

### Results

| Scenario | Original | JIT | Reduction |
|----------|----------|-----|-----------|
| Formal email | 1,200 | 100+200+100 = 400 | 67% |
| Casual blog | 1,200 | 100+150+100 = 350 | 71% |
| Grammar check | 1,200 | 100+200 = 300 | 75% |

---

## Example 3: Code Review Assistant

### Original Prompt (~2,000 tokens)

```markdown
You are a code review assistant...

## Language-Specific Guidelines
### Python
[300 tokens]

### JavaScript
[300 tokens]

### Java
[250 tokens]

## Review Criteria
### Security
[200 tokens]

### Performance
[200 tokens]

### Readability
[150 tokens]

## Common Patterns
[400 tokens of patterns and anti-patterns]

## Response Format
[200 tokens of format instructions]
```

### Converted Architecture

**Core Prompt (~80 tokens)**:
```markdown
You are a code review assistant.

## Process
1. Identify language
2. Load relevant guidelines
3. Review for security, performance, readability
4. Provide actionable feedback

## Context
Load language-specific file based on detected language.
Load review-criteria when performing detailed review.
```

**JIT Files**:

`languages/python.md`, `languages/javascript.md`, `languages/java.md`

`criteria/security.md`, `criteria/performance.md`, `criteria/readability.md`

`patterns/common-patterns.md`

### Results

| Scenario | Original | JIT | Reduction |
|----------|----------|-----|-----------|
| Python review | 2,000 | 80+300+200 = 580 | 71% |
| JS security focus | 2,000 | 80+300+200 = 580 | 71% |
| Quick pattern check | 2,000 | 80+400 = 480 | 76% |

---

## Conversion Summary

| Example | Original | Core | Typical Usage | Reduction |
|---------|----------|------|---------------|-----------|
| Support Agent | 800 | 120 | 270 | 66% |
| Writing Assistant | 1,200 | 100 | 350-400 | 67-71% |
| Code Review | 2,000 | 80 | 480-580 | 71-76% |

## Key Takeaways

1. **Larger prompts benefit more**: Higher absolute savings
2. **Task diversity enables JIT**: More distinct paths = more savings
3. **Core prompt should be minimal**: Focus on routing, not content
4. **File organization matters**: Logical groupings improve retrieval

---

*Note: Token counts are illustrative. Actual results depend on specific content and implementation.*
