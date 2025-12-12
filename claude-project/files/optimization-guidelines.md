# Optimization Guidelines

This file provides strategies for maximizing token efficiency and system performance in JIT architectures.

## Token Optimization Strategies

### Strategy 1: Ruthless Deduplication

**Problem**: Same information repeated across sections

**Solution**:
1. Identify repeated content across original prompt
2. Create single source of truth
3. Reference instead of repeat

**Example**:

Before (repeated 3 times):
```
Remember: Always verify customer identity before 
making any account changes. Required verification 
includes: full name, last 4 of SSN, date of birth.
```

After (single reference):
```
Core prompt: "Follow identity-verification protocol"
JIT file: Contains full verification procedure once
```

### Strategy 2: Implicit vs. Explicit

**Problem**: Stating what capable models already know

**Solution**:
- Remove obvious instructions
- Trust model capabilities
- Only specify non-obvious requirements

**Example**:

Before:
```
When the user says hello, respond with a greeting.
Be polite in your responses. Use proper grammar
and punctuation. Spell words correctly.
```

After:
```
Maintain professional, helpful tone.
```

### Strategy 3: Hierarchy Compression

**Problem**: Verbose nested structures

**Solution**:
- Flatten where possible
- Use tables for structured data
- Eliminate unnecessary nesting

**Example**:

Before (47 tokens):
```
Customer tiers:
- Bronze tier:
  - Discount: 5%
  - Support: Email only
  - Returns: 14 days
- Silver tier:
  - Discount: 10%
  - Support: Email + Chat
  - Returns: 30 days
- Gold tier:
  - Discount: 15%
  - Support: Priority
  - Returns: 60 days
```

After (35 tokens):
```
| Tier | Discount | Support | Returns |
|------|----------|---------|---------|
| Bronze | 5% | Email | 14 days |
| Silver | 10% | Email+Chat | 30 days |
| Gold | 15% | Priority | 60 days |
```

### Strategy 4: Conditional Loading

**Problem**: Loading all context regardless of need

**Solution**:
- Classify tasks at conversation start
- Load only relevant context
- Defer edge case loading until needed

**Implementation**:
```
Task classification:
- Simple query → Core only
- Standard process → Core + relevant workflow
- Complex case → Core + workflow + edge cases
```

### Strategy 5: Progressive Detail

**Problem**: Front-loading all detail

**Solution**:
- Start with summary
- Expand only when needed
- Let model request detail

**Example**:
```
Core: "For returns, follow standard return policy."
JIT 1: Basic return procedure
JIT 2: Exception handling (load only if needed)
JIT 3: Escalation procedures (load only if needed)
```

## Structural Optimization

### File Granularity

**Too coarse** (single large file):
- Loads unnecessary content
- Loses JIT benefits

**Too fine** (many tiny files):
- Routing complexity increases
- Risk of missing needed content

**Optimal** (4-6 files for most systems):
- Logical groupings
- Clear boundaries
- Manageable routing

### Naming for Context

File names provide semantic value at no token cost:

❌ `file1.md`, `procedures.md`, `stuff.md`
✅ `returns-workflow.md`, `vip-handling.md`, `shipping-exceptions.md`

### Header Efficiency

**Verbose header**:
```markdown
# This File Contains the Complete and Comprehensive 
# Documentation for Handling Customer Returns and 
# Exchanges Including All Edge Cases
```

**Efficient header**:
```markdown
# Returns & Exchanges
```

## Trigger Optimization

### Specific > Generic

**Generic trigger** (over-fires):
```
Load when: customer has a question
```

**Specific trigger** (precise):
```
Load when: user mentions "return", "refund", 
           "exchange", or "send back"
```

### Keyword Lists

Maintain efficient keyword matching:

```markdown
## Trigger Keywords
Returns: return, refund, exchange, send back, 
         money back, defective
Shipping: ship, delivery, track, arrive, ETA
Account: password, login, account, access, verify
```

### Negative Triggers

Prevent false positives:

```
Load shipping-info.md when:
- User mentions shipping or delivery
- BUT NOT when discussing past deliveries 
  (load order-history.md instead)
```

## Performance Monitoring

### Metrics to Track

| Metric | Target | Warning |
|--------|--------|---------|
| Core prompt size | <200 tokens | >300 tokens |
| Avg JIT files loaded | 1-2 | >3 |
| False positive rate | <10% | >20% |
| Functionality gaps | 0 | Any |

### Optimization Cycle

1. **Measure**: Track actual token usage
2. **Analyze**: Identify patterns in JIT loading
3. **Adjust**: Refine triggers and content
4. **Verify**: Confirm functionality preserved
5. **Repeat**: Continuous improvement

### Warning Signs

🚩 **Over-loading**: Same files loaded every conversation
- Consider: Move content to core

🚩 **Under-loading**: Expected files not triggered
- Consider: Refine trigger conditions

🚩 **Thrashing**: Many files loaded then unused
- Consider: More specific triggers

🚩 **Gaps**: Functionality missing
- Consider: Missing triggers or content

## Common Pitfalls

### Premature Optimization
Don't optimize until you have:
- Working baseline
- Measured token usage
- Identified actual pain points

### Over-Engineering
Simple solutions often outperform complex ones:
- Fewer files with clear boundaries
- Straightforward triggers
- Minimal routing logic

### Neglecting Maintenance
JIT systems require ongoing attention:
- Update when requirements change
- Monitor for drift
- Document changes

## Optimization Checklist

Pre-deployment:
- [ ] Core prompt under 200 tokens
- [ ] Each JIT file has clear trigger
- [ ] No duplicate content across files
- [ ] All functionality covered

Post-deployment:
- [ ] Monitor actual loading patterns
- [ ] Track false positive/negative rates
- [ ] Gather user feedback
- [ ] Iterate based on data

---

*For implementation details, see `conversion-workflow.md`.*
