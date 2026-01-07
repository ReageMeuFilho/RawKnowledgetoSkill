# Examples for FIN-002: Bank Reconciliation

## Example 1: Basic Reconciliation

**Scenario**: A simple reconciliation with a few transactions that match perfectly.

**Input**:
- `bank_transactions.csv` with 3 transactions.
- `ledger_entries.csv` with 3 corresponding transactions.

**Expected Output**:
- `summary`: `matched_count: 3`, `exception_count: 0`
- `matches`: 3 matched pairs.
- `exceptions`: Empty array.
- `posting_plan`: Empty array.

## Example 2: Reconciliation with Bank Fee

**Scenario**: A reconciliation where the bank statement includes a monthly service fee that is not yet recorded in the ledger.

**Input**:
- `bank_transactions.csv` with a $15 bank fee.
- `ledger_entries.csv` without the corresponding fee.

**Expected Output**:
- `summary`: `exception_count: 1`
- `exceptions`: 1 exception for the unmatched bank fee.
- `posting_plan`: A proposed journal entry to record the $15 bank fee expense.

## Example 3: Reconciliation with Amount Mismatch

**Scenario**: A transaction is recorded in the ledger with a typo in the amount.

**Input**:
- Bank transaction for $100.50
- Ledger entry for $100.05

**Expected Output**:
- `summary`: `exception_count: 1`
- `exceptions`: 1 exception for the amount mismatch.
- `posting_plan`: A proposed journal entry to correct the ledger amount.
