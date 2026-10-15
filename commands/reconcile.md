---
description: Reconcile a bank/card CSV or XLSX workbook against a general ledger
argument-hint: "[bank-file] [gl-file]"
---

# Reconcile Bank vs. General Ledger

Run a reconciliation for: `$ARGUMENTS`

## Instructions

1. Locate the bank statement file and the general ledger file from `$ARGUMENTS` (or search the workspace for CSV/spreadsheet files if not specified).
2. Compare all transactions between the two sources:
   - Identify matched items.
   - List **Deposits in Transit** and **Outstanding Checks/Payments** (in GL, not on Bank).
   - List **Unrecorded Bank Transactions** (on Bank, not in GL, such as service charges, interest, or missed receipts).
   - Highlight any **Amount Discrepancies** (same date/reference, different dollar amount) or **Potential Duplicates**.
3. Produce a standard **Bank Reconciliation Schedule** showing Adjusted Bank Balance vs. Adjusted Book Balance, plus any required adjusting journal entries.
