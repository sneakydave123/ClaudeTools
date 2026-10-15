---
name: expense-categorizer
description: Use this skill when the user wants to categorize raw transactions, credit card exports, or receipts into a Chart of Accounts, identify tax-deductible categories, or flag missing documentation.
---

# Expense Categorizer & COA Mapper

Use this skill to classify raw transaction exports or receipt summaries into standard accounting categories.

## Default Chart of Accounts (COA) Mapping

If the workspace does not contain a custom Chart of Accounts file, use these standard categories:
- `6100 - Advertising & Marketing`
- `6200 - Bank & Merchant Fees`
- `6300 - Dues & Subscriptions (Software/SaaS)`
- `6400 - Insurance`
- `6500 - Legal & Professional Fees`
- `6600 - Meals & Entertainment` *(Flag 50% deductibility rule where applicable)*
- `6700 - Office Supplies & Equipment`
- `6800 - Rent & Utilities`
- `6900 - Travel & Lodging`
- `7000 - Uncategorized / Ask Client` *(Use when vendor purpose is ambiguous)*

## Workflow

1. **Read Transactions**: Load the provided CSV/text list of expenses (Date, Vendor/Description, Amount).
2. **Assign Categories & Confidence**:
   - Map each line item to an account code and name.
   - Assign a confidence level (`High`, `Medium`, `Review Needed`).
3. **Compliance & Documentation Flags**:
   - Flag any single expense **>= $75.00** that lacks a receipt reference.
   - Flag potential **Personal vs. Business** mixed expenses or ambiguous vendors (e.g., Amazon, Walmart, Venmo, PayPal) for client clarification.
   - Flag potential **Capital Expenditures (CapEx)** (e.g., hardware/equipment > $2,500) that may qualify for fixed asset capitalization or Section 179 / de minimis safe harbor.
4. **Output**:
   - Present a clean summary table grouped by category with subtotals and grand total.
   - Provide a list of items requiring receipts or client clarification.
   - Offer to export the categorized transactions to a new CSV file.
