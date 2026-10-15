---
description: Draft a balanced double-entry journal entry from a description or file
argument-hint: "[transaction description or file path]"
---

# Draft Double-Entry Journal Entry

Create a balanced accounting journal entry for: `$ARGUMENTS`

## Instructions

1. If `$ARGUMENTS` references a file in the workspace, read it first. If `$ARGUMENTS` is empty, ask the user to describe the transaction (e.g., prepaid insurance amortization, payroll accrual, fixed asset depreciation, deferred revenue recognition).
2. Present the journal entry in a structured markdown table:

| Account Code | Account Name | Debit ($) | Credit ($) | Memo / Line Description |
| :--- | :--- | ---: | ---: | :--- |

3. **Strict Accounting Rules**:
   - **Total Debits MUST strictly equal Total Credits** (`$0.00` out-of-balance). Show a `Total` row at the bottom of the table.
   - Indicate the normal balance and account type (`Asset`, `Liability`, `Equity`, `Revenue`, `Expense`) for each line.
   - Include a brief **Accounting Basis / GAAP Note** explaining why the entry is structured this way and whether a reversing entry is needed next period.
