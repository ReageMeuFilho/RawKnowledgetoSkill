# FIN-002: Bank Reconciliation

## Purpose

To reconcile bank transactions against ledger entries, propose matches, identify exceptions, and produce a posting plan with a complete audit trail. This skill is fundamental to ensuring financial accuracy and trust account compliance across STR, LTR, and HOA verticals.

## Inputs

- **Bank Transaction Data**: A list of transactions from a bank statement (CSV, OFX, or API feed), including transaction ID, date, amount, and description.
- **Ledger Entries**: A list of corresponding transactions from the property management ledger, including entry ID, date, amount, memo, and GL account.
- **Reconciliation Policies**: Rules defining match tolerances (e.g., amount variance, date window) and approval requirements for posting adjustments.

## Outputs

- **Reconciliation Summary**: A high-level overview including matched/unmatched counts and total amounts.
- **Proposed Matches**: A list of suggested pairings between bank and ledger transactions with a confidence score.
- **Exception Report**: A detailed list of all unmatched or partially matched items, categorized by type (e.g., unmatched bank, unmatched ledger, amount mismatch).
- **Posting Plan**: A set of proposed journal entries to resolve exceptions (e.g., recording bank fees, interest, or correcting posting errors).
- **Audit Log**: An immutable record of all actions taken during the reconciliation process.

## Deterministic Steps

1.  **Ingest Data**: Load bank transactions and ledger entries for the specified reconciliation period.
2.  **Apply Matching Rules**: Iterate through bank transactions and apply matching logic:
    *   **Exact Match**: Find ledger entries with the same date and amount.
    *   **Fuzzy Match**: Use defined tolerances to find potential matches within a date range and amount threshold.
    *   **Reference Match**: Match based on check numbers, transaction IDs, or reference codes in the description.
3.  **Propose Matches**: For each potential match, calculate a confidence score based on the strength of the matching criteria.
4.  **Identify Exceptions**: Flag all bank transactions and ledger entries that do not have a high-confidence match.
5.  **Categorize Exceptions**: Classify exceptions into types (e.g., bank-side only, ledger-side only, duplicate, amount mismatch).
6.  **Generate Posting Plan**: For common exceptions (e.g., bank fees, interest), propose corresponding journal entries based on predefined rules.
7.  **Produce Summary and Audit Trail**: Generate the final reconciliation summary, exception report, and a complete audit log of the process.

## Policies & Guardrails

- **Segregation of Duties**: The user initiating the reconciliation should not be the same user who approves the final posting plan.
- **Three-Way Reconciliation (for Trust Accounts)**: For property management trust accounts, the reconciliation must validate three checkpoints: the bank statement balance, the bank ledger balance in the system, and the sum of all individual trust liability balances.
- **Locking Periods**: Once a reconciliation is finalized and approved, the corresponding accounting period should be locked to prevent unauthorized changes.

## Failure Modes

- **Incomplete Data**: Fails if bank transaction data or ledger entries are missing for the period.
- **Sync Errors**: Fails if the connection to the bank feed API is down or returns corrupted data.
- **Ambiguous Matches**: If multiple ledger entries could match a single bank transaction, flag for manual review.

## Acceptance Criteria

- The final reconciled balance must equal the adjusted bank statement balance.
- All transactions must be either matched or listed as an exception.
- The posting plan must balance (debits equal credits).

## Telemetry

- **Execution Time**: Time taken to complete the reconciliation process.
- **Automation Rate**: Percentage of transactions automatically matched.
- **Exception Rate**: Percentage of transactions flagged as exceptions.
- **Manual Intervention Rate**: Percentage of exceptions that require manual resolution.
