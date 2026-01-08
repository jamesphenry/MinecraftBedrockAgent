# Security

This document describes the security and safety measures built into the Bedrock Addon Management system.

---

## Principle of Least Destruction

The system prioritizes:

* Disabling over deleting
* Validating before modifying
* Explaining before acting

Destructive actions require **explicit user intent**.

---

## Vanilla Pack Protection

Files provided by the official Bedrock server distribution:

* Are treated as **read-only**
* Cannot be modified or deleted
* Are excluded from scans and operations unless explicitly overridden

---

## UUID Integrity

All pack UUIDs:

* Are read directly from `manifest.json`
* Are never generated or guessed
* Are checked for duplicates across all worlds

This prevents collisions and world corruption.

---

## World Isolation

Operations are scoped to specific worlds:

* No global enabling by default
* No accidental deletion across worlds
* Explicit world selection is required for changes

---

## Deterministic Behavior

Given identical inputs and filesystem state, AI agents will:

* Perform the same actions
* Produce the same results
* Avoid non-deterministic behavior

This ensures repeatability and accountability.

---

## Auditability

AI agents must report:

* What was changed
* What was not changed
* Why decisions were made

Audit logs can be reviewed by humans or automated systems.

---

## Failure Safety

If an addon is malformed or ambiguous:

* Installation halts
* No partial changes occur
* User is informed with a detailed report

Failing safely is preferred over guessing or proceeding blindly.
