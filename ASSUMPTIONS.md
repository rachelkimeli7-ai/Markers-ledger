# ASSUMPTIONS.md

# System Assumptions

This document outlines the assumptions made during the implementation of the Makerspace Asset Ledger system.

---

# General Assumptions

- All timestamps are provided in ISO-8601 compatible format.
- Events are processed chronologically after sorting by timestamp.
- If two events share the same timestamp, `event_id` is used as the tie-breaker.
- All item IDs are assumed to be unique.
- All event IDs are assumed to be unique unless explicitly detected otherwise.
- The system assumes all input files exist and are readable.

---

# Inventory Assumptions

- Inventory records define the initial system state before any events are processed.
- Items with `checked_out` status must include:
  - a valid holder
  - a valid due date
- Items marked `available` or `maintenance` should not have:
  - active holders
  - due dates
- Empty string values for holder or due date are treated as missing values.

---

# Event Processing Assumptions

- Events are ignored if validation fails.
- Invalid events do not stop system execution.
- Unknown event actions are ignored unless explicitly handled.
- Item state changes occur immediately after successful event processing.
- Only successfully processed events affect inventory state.

---

# Actor Assumptions

- Student actor IDs begin with:
```txt id="a1"
s