---
description: Perform Budget vs. Actual or period-over-period variance analysis
argument-hint: "[financials-file]"
---

# Financial Variance Analysis (Flux Analysis)

Analyze financial variances for: `$ARGUMENTS`

## Instructions

1. Read the target financial statement or CSV file specified in `$ARGUMENTS` (or ask the user which file/columns to compare).
2. For each line item, calculate:
   - **Dollar Variance ($)**: `Actual - Budget` (or `Current Period - Prior Period`)
   - **Percentage Variance (%)**: `(Variance / Base) * 100`
   - **Favorable / Unfavorable (`F` / `U`)**: Remember that higher revenue is Favorable (`F`), while higher expense is Unfavorable (`U`).
3. **Materiality Filtering**:
   - Flag all material variances (default threshold: **>= 10%** AND **>= $1,000**, unless the user specifies otherwise).
4. **Output**:
   - Summary table of all line items with `$`, `%`, and `F/U` indicators.
   - Executive summary calling out the top drivers of variance and specific questions to ask department heads or the client.
