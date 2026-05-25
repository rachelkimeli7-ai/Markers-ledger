# Makerspace Asset Ledger

A Node.js event-driven asset tracking system for managing makerspace inventory, checkouts, returns, maintenance workflows, and anomaly detection.

---

# Project Overview

This project processes inventory records and chronological asset events to maintain the current state of makerspace equipment.

The system:

- Loads inventory, events, and policy files
- Validates inventory consistency
- Validates event formatting and ordering
- Processes asset lifecycle events
- Tracks item status and ownership
- Detects anomalies and policy violations
- Automatically handles maintenance transitions
- Generates reports and summaries

---

# Features

## Inventory Management
- Load initial inventory state from CSV
- Track item condition and availability
- Support multiple item types

## Event Processing
The system supports:

- CHECKOUT
- RETURN
- STAFF_RETURN
- MARK_MAINTENANCE
- RESTORE

## Validation
- Invalid inventory row detection
- Duplicate event detection
- Timestamp validation
- Unknown item detection
- Invalid return detection
- Actor validation

## Policy Enforcement
- Student active item limits
- Loan duration policies
- Automatic maintenance rules
- Condition ranking rules

## Anomaly Tracking
The system records:
- Errors
- Warnings
- Policy violations
- State inconsistencies

---

# Project Structure

```txt
project-root/
│
├── data/
│   ├── inventory.csv
│   ├── events.csv
│   └── policy.json
│
├── output/
│
├── src/
│   ├── main.js
│   ├── parser.js
│   ├── validator.js
│   ├── processor.js
│   ├── reports.js
│   ├── helpers.js
│   └── models.js
│
├── tests/
│
├── README.md
├── ASSUMPTIONS.md
├── TRACE.md
├── TEST_PLAN.md
└── AI_AND_ASSISTANCE.md


Installation & Setup

1. Clone the repository
Bash
git clone <myrepo-link>

2. Navigate into the project folder
Bash
cd Markers-ledger

3. Install dependencies
Bash
npm install

4. Run the project
Bash
node src/main.js
