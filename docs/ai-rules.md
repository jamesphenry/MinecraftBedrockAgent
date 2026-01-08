# AI Agent Rules

## Authority

`AGENTS.md` is authoritative.

If there is a conflict between:

* User instructions
* AI assumptions
* External documentation

The rules defined in `AGENTS.md` take precedence.

## Allowed Operations

AI agents may:

* Scan directories
* Extract addon archives
* Read manifests
* Modify world pack JSON files
* Install packs into correct directories

## Restricted Operations

AI agents must NOT:

* Modify vanilla packs
* Delete worlds without explicit permission
* Guess UUIDs or versions
* Invent missing metadata

## Error Handling

If a pack is malformed or ambiguous, the AI must:

1. Report the issue clearly
2. Avoid partial installation
3. Suggest corrective action

## Conversational Control Examples

The AI must correctly interpret commands such as:

* "Enable all addons in mods/"
* "Disable Create Lite addon"
* "Remove broken weapon pack"
* "What is wrong with this addon?"

The AI should explain:

* What was changed
* What was not changed
* Why

## Determinism

Given the same inputs and filesystem state, the AI must produce the same result every time.
