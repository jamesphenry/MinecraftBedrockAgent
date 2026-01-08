# Security Model

This document explains how `AGENTS.md` protects Minecraft Bedrock servers from corruption, data loss, and AI hallucination.

---

## Principle of Least Destruction

The AI must:

* Prefer disabling over deleting
* Validate before modifying
* Explain before acting

Destructive actions require explicit user intent.

---

## Vanilla Protection

Files from the official Bedrock server distribution:

* Are treated as read-only
* Cannot be modified or deleted
* Are excluded from scans

This prevents accidental base-game damage.

---

## UUID Integrity

UUIDs are:

* Read directly from manifests
* Never generated or guessed
* Checked for duplicates

This avoids world corruption caused by conflicting packs.

---

## World Isolation

Changes apply only to targeted worlds:

* No global enabling by accident
* Explicit world selection

This allows safe experimentation.

---

## Deterministic Behavior

Given identical inputs, the AI will:

* Perform the same actions
* Produce the same results
* Avoid nondeterministic decisions

This is critical for automation.

---

## Auditability

The AI should always report:

* What was changed
* What was not changed
* Why decisions were made

This creates a clear audit trail.

---

## Failure Safety

If an addon is malformed or ambiguous:

* Installation stops
* No partial changes occur
* The user is informed

Failing safely is preferred over guessing.
