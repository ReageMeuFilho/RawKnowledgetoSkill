# Evals for FIN-002: Bank Reconciliation

- **Test Case 1: Perfect Match**
  - **Objective**: Verify that the skill can correctly match all transactions when the bank and ledger data are identical.
  - **Setup**: Provide identical bank and ledger files.
  - **Assertion**: `exception_count` should be 0 and `matched_count` should equal the number of transactions.

- **Test Case 2: Unmatched Bank Transaction (Bank Fee)**
  - **Objective**: Verify that the skill correctly identifies a bank transaction with no corresponding ledger entry and proposes a posting.
  - **Setup**: Bank file contains a transaction not present in the ledger file (e.g., a bank service charge).
  - **Assertion**: The unmatched transaction should be in the `exceptions` list, and a corresponding journal entry should be in the `posting_plan`.

- **Test Case 3: Unmatched Ledger Transaction (Outstanding Check)**
  - **Objective**: Verify that the skill correctly identifies a ledger entry with no corresponding bank transaction (e.g., an outstanding check).
  - **Setup**: Ledger file contains a transaction not present in the bank file.
  - **Assertion**: The unmatched transaction should be in the `exceptions` list, and the `posting_plan` should be empty for this item.

- **Test Case 4: Amount Mismatch**
  - **Objective**: Verify that the skill identifies transactions where the amounts do not match within the tolerance.
  - **Setup**: A bank transaction and ledger entry have slightly different amounts.
  - **Assertion**: The pair should be listed in the `exceptions` with type `AMOUNT_MISMATCH`.

- **Test Case 5: Date Mismatch (Within Tolerance)**
  - **Objective**: Verify that the skill correctly matches transactions where the dates are slightly different but within the defined tolerance.
  - **Setup**: A bank transaction and ledger entry have dates that are a few days apart but within the `match_tolerance_days`.
  - **Assertion**: The pair should be in the `matches` list.
