# Extraction Patterns

This file catalogs common patterns for extracting content from monolithic prompts into JIT files.

## Pattern 1: Workflow Extraction

### Identifies
Sequential procedures, step-by-step processes, decision trees

### Indicators
- Numbered steps
- "First... then... finally..." language
- Conditional branches
- Flow keywords (proceed, continue, if)

### Extraction Strategy

**Original** (embedded in main prompt):
```
When handling returns:
1. Verify purchase within 30 days
2. Check item condition
3. If damaged, route to supervisor
4. If acceptable, process refund
5. Send confirmation email
```

**Extracted** (returns-workflow.md):
```markdown
# Returns Processing Workflow

## Trigger
Load when: User mentions "return", "refund", or "exchange"

## Procedure
1. Verify purchase within 30 days
2. Check item condition
3. If damaged, route to supervisor
4. If acceptable, process refund
5. Send confirmation email

## Notes
- Supervisor escalation threshold: damage >$100
- Confirmation email template: use standard-return-confirmation
```

**Core prompt reference**:
```
For return requests → Load returns-workflow.md
```

## Pattern 2: Example Consolidation

### Identifies
Scattered examples, demonstrations, sample inputs/outputs

### Indicators
- "For example..." 
- "Such as..."
- Input/output pairs
- Demonstration scenarios

### Extraction Strategy

**Original** (scattered throughout):
```
...when formatting names, capitalize properly. 
For example: "john smith" → "John Smith"
...
...when parsing dates, use ISO format.
For example: "March 15, 2024" → "2024-03-15"
...
```

**Extracted** (formatting-examples.md):
```markdown
# Formatting Examples

## Trigger
Load when: User requests formatting help or examples

## Name Formatting
| Input | Output |
|-------|--------|
| john smith | John Smith |
| JANE DOE | Jane Doe |
| o'brien | O'Brien |

## Date Formatting
| Input | Output |
|-------|--------|
| March 15, 2024 | 2024-03-15 |
| 15/03/24 | 2024-03-15 |
| 2024.03.15 | 2024-03-15 |

## Edge Cases
[Additional examples for tricky scenarios]
```

## Pattern 3: Edge Case Isolation

### Identifies
Exception handling, special cases, rare scenarios

### Indicators
- "However, if..."
- "In the rare case..."
- "Exception:"
- "Special handling for..."

### Extraction Strategy

**Original** (interspersed):
```
Process orders normally, but if the customer is 
flagged as VIP, apply 10% discount automatically.
...
Standard shipping is 5-7 days, but for Alaska/Hawaii
add 3 additional days to estimates.
...
```

**Extracted** (special-cases.md):
```markdown
# Special Cases & Exceptions

## Trigger
Load when: Processing orders for flagged accounts 
           OR shipping to non-continental US

## VIP Handling
- Automatic 10% discount
- Priority queue for support
- Extended return window (60 days)

## Regional Shipping
| Region | Additional Days |
|--------|-----------------|
| Alaska | +3 |
| Hawaii | +3 |
| Puerto Rico | +5 |
| International | Variable |
```

## Pattern 4: Domain Knowledge Extraction

### Identifies
Reference information, terminology, background context

### Indicators
- Glossaries
- Technical definitions
- Industry-specific content
- Background explanations

### Extraction Strategy

**Original** (front-loaded):
```
You are a financial advisor assistant. Key terms:
- APR: Annual Percentage Rate, the yearly interest...
- AUM: Assets Under Management, total market value...
- Basis Point: 1/100th of a percentage point...
[continues for many paragraphs]
```

**Extracted** (financial-glossary.md):
```markdown
# Financial Terminology

## Trigger
Load when: User asks about financial terms
           OR using technical financial language

## Core Terms

### APR (Annual Percentage Rate)
The yearly interest rate charged on borrowed money 
or earned on investments, expressed as a percentage.

### AUM (Assets Under Management)
Total market value of investments managed by a 
financial institution on behalf of clients.

### Basis Point
One hundredth of a percentage point (0.01%).
Example: 50 basis points = 0.50%

[Additional terms...]
```

## Pattern 5: Constraint Separation

### Identifies
Rules, limitations, guardrails, compliance requirements

### Indicators
- "Never..."
- "Always..."
- "Must..."
- "Do not..."

### Extraction Strategy

**Original** (scattered):
```
...never share personal information...
...always verify identity before account changes...
...do not provide specific medical advice...
...must log all escalations...
```

**Extracted** (constraints.md):
```markdown
# Operating Constraints

## Trigger
Load when: Handling sensitive requests
           OR when constraint verification needed

## Privacy Constraints
- Never share personal information with third parties
- Mask account numbers in all displays
- Require identity verification for data access

## Compliance Requirements
- Log all escalations within 24 hours
- Maintain audit trail for financial transactions
- Follow regional data retention policies

## Content Restrictions
- Do not provide specific medical advice
- Do not offer legal opinions
- Redirect tax questions to qualified professionals
```

## Pattern 6: Output Template Extraction

### Identifies
Response formats, structured outputs, templates

### Indicators
- Format specifications
- Template structures
- Required fields
- Layout requirements

### Extraction Strategy

**Original** (embedded):
```
When providing product recommendations, format as:

**[Product Name]**
Price: $X.XX
Rating: ★★★★☆ (X/5)
Key Features:
- Feature 1
- Feature 2
Availability: [In Stock/Limited/Out of Stock]
```

**Extracted** (output-templates.md):
```markdown
# Output Templates

## Trigger
Load when: Generating structured responses

## Product Recommendation Template
```
**[Product Name]**
Price: $X.XX
Rating: ★★★★☆ (X/5)
Key Features:
- [Feature 1]
- [Feature 2]
- [Feature 3]
Availability: [Status]
```

## Order Confirmation Template
[Template here]

## Error Response Template
[Template here]
```

## Anti-Patterns to Avoid

### Over-Fragmentation
❌ Creating too many small files
✅ Group related content logically

### Hidden Dependencies
❌ JIT files that require other JIT files
✅ Make each file self-contained or document dependencies

### Ambiguous Triggers
❌ "Load when relevant"
✅ "Load when user mentions 'return' or 'refund'"

### Lost Context
❌ Extracting without header/usage information
✅ Always include trigger conditions and usage notes

---

*For complete examples, see `examples.md`.*
