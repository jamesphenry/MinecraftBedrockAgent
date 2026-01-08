# Overview

## Purpose

`AGENTS.md` is an instruction and constraint file used to guide AI agents when interacting with a Minecraft Bedrock Dedicated Server filesystem.

Its primary goals are to:

* Make AI behavior predictable and repeatable
* Prevent destructive or unsafe filesystem operations
* Encode Bedrock-specific domain knowledge
* Remove ambiguity from addon installation, modification, and world enabling

AI agents must treat `AGENTS.md` as an authoritative source of truth.

## Scope

This document applies specifically to:

* Minecraft Bedrock Dedicated Server environments
* Filesystem-level addon management
* Behavior Pack (BP) and Resource Pack (RP) installation and control

It does not define gameplay behavior, pack content, or addon correctness beyond structural validity.

## Design Principles

1. **Explicit over implicit**
   If a rule is not written, the AI must not assume it.

2. **Safety-first defaults**
   Production worlds and vanilla packs are preserved unless explicitly overridden.

3. **Idempotency**
   Repeating the same instruction must not introduce duplication or corruption.

4. **Explainability**
   The AI must be able to explain what it changed and why.

5. **Separation of concerns**
   Installation, enabling, disabling, and deletion are distinct operations.
