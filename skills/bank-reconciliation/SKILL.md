---
name: bank-reconciliation
description: Use this skill when the user wants to reconcile bank statements, credit card statements, or payment processor exports against a general ledger or check register. Automatically matches transactions, flags discrepancies, and formats a standard bank reconciliation schedule.
---

# Bank & Credit Card Reconciliation

Use this skill to reconcile external bank or credit card statements (CSV, TSV, Excel, or text) against internal general ledger (GL) records.

## Workflow

1. **Inspect Input Files**:
   - Identify the **Bank Statement** file and the **General Ledger / Register** file.
   - Normalize date formats (`YYYY-MM-DD`), strip currency symbols/commas, and align sign conventions (ensure deposits/withdrawals have consistent signs across both files).

2. **Match Transactions**:
   - **Exact Matches**: Same amount and date within ±3 business days, or matching check/reference number.
   - **Fuzzy / Split Matches**: Multiple GL entries summing to a single bank batch deposit, or matching vendor names with slight clearing delays.
   - **Discrepancies**: Same reference/vendor and date, but transposed digits or penny differences.

3. **Categorize Unmatched Items**:
   - **Deposits in Transit**: Recorded in the GL, not yet cleared on the bank statement.
   - **Outstanding Checks / Payments**: Recorded in the GL, not yet cleared on the bank statement.
   - **Unrecorded Bank Items**: On the bank statement, missing from the GL (e.g., bank fees, interest income, ACH auto-pay, unrecorded receipts).

4. **Produce Reconciliation Schedule**:
   Output a clear summary table:
   - **Bank Side**: Ending Bank Balance + Deposits in Transit - Outstanding Checks = **Adjusted Bank Balance**
   - **Book Side**: Ending GL Balance + Unrecorded Credits (Interest/Deposits) - Unrecorded Debits (Fees/Charges) = **Adjusted Book Balance**
   - **Unreconciled Difference**: Must equal `$0.00` (or clearly isolate the remaining discrepancy to investigate).
   - Provide proposed **Adjusting Journal Entries** for unrecorded bank items.
