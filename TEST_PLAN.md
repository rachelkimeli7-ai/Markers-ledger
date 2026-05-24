# Test Plan

## Objective

The purpose of this testing plan is to confirm that the Makerspace Asset Ledger system operates correctly under normal and edge-case conditions.

The tests focus on verifying that the application:

- reads and validates input files correctly
- processes events in chronological order
- updates inventory state accurately
- enforces policy rules
- tracks active student loans
- identifies and records anomalies
- produces correct output files

---

# Core Test Scenarios

| Scenario | Expected Outcome |
|---|---|
| Repeated event ID | Event rejected with BAD_EVENT_FORMAT anomaly |
| Invalid timestamp format | Event ignored and anomaly recorded |
| Checkout for nonexistent item | UNKNOWN_ITEM anomaly generated |
| Attempt to checkout unavailable item | ITEM_NOT_AVAILABLE anomaly generated |
| Student exceeds borrowing limit | ITEM_LIMIT_REACHED anomaly generated |
| Missing policy for item type | UNKNOWN_LOAN_POLICY anomaly generated |
| Return attempted on available item | RETURN_NOT_ALLOWED anomaly generated |
| Student reports improved condition | Warning generated and original condition retained |
| Staff-assisted return | STAFF_RETURN_USED warning recorded |
| Returned item marked damaged | Item automatically moved to maintenance |
| Maintenance item restored | Item status updated to available |
| Out-of-order CSV events | Events processed according to timestamps |

---

# Validation Checks Performed

The following validations were manually confirmed:

- inventory rows loaded successfully
- malformed inventory rows detected
- duplicate event IDs rejected
- malformed timestamps detected
- chronological sorting functioning correctly
- condition ranking rules enforced
- maintenance transitions functioning correctly
- restore workflow functioning correctly

---

# Output Verification

The following generated files were reviewed and verified:

| Output File | Verification |
|---|---|
| final_state.csv | Final inventory state accurate |
| anomalies.csv | All warnings and errors recorded |
| student_summary.csv | Student item counts correct |
| run_summary.md | Processing summary generated correctly |

---

# Event Processing Verification

## CHECKOUT
Verified that:
- only available items can be checked out
- due dates are calculated correctly
- student borrowing limits are enforced

---

## RETURN
Verified that:
- only current holders can return items
- condition reports update item state correctly
- damaged items enter maintenance automatically

---

## STAFF_RETURN
Verified that:
- only staff actors may perform staff returns
- warning entries are generated correctly
- item ownership clears properly

---

## Maintenance Workflow
Verified that:
- maintenance actions change item status correctly
- restore actions return items to available state

---

# Edge Conditions Tested

The system was tested against several edge cases including:

- invalid inventory records
- duplicate events
- malformed timestamps
- unknown items
- invalid returns
- unknown condition reports
- maintenance recovery
- missing holder values
- policy inconsistencies

---

# Manual Trace Validation

Special attention was given to the required trace events:

- e006
- e020
- e030
- e043
- e049

These events were manually reviewed to verify:
- state transitions
- anomaly generation
- chronological ordering
- maintenance behavior

---

# Test Result Summary

The testing process confirmed that the system:

- maintains consistent inventory state
- processes events correctly
- enforces configured policies
- handles invalid input safely
- records anomalies accurately
- supports the full asset lifecycle