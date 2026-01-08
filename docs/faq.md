# FAQ

## Why does this exist?

Because Minecraft Bedrock addon management is chaos.

There is:

* No standard addon structure
* No enforced naming rules
* No reliable indicators of pack type

This system brings **order without rewriting addons**.

---

## Do addons follow a standard format?

No.

Some addons:

* Nest packs three directories deep
* Use unicode symbols in folder names
* Mislabel behavior packs as resource packs
* Include multiple packs in one archive

The AI adapts instead of assuming.

---

## Does this modify vanilla Bedrock files?

No.

Vanilla and chemistry packs are:

* Never modified
* Never deleted
* Never renamed

This is enforced by `AGENTS.md`.

---

## Can this break my world?

The system is designed to prevent that.

Safeguards include:

* UUID duplicate detection
* Manifest validation
* World-specific enabling
* Clear reporting before destructive actions

---

## Can I undo changes?

Yes.

You can:

* Disable addons without deleting them
* Re-enable previously installed packs
* Remove addons cleanly

---

## Does this require mods or plugins?

No.

This works with:

* Vanilla Bedrock Dedicated Server
* Any AI agent capable of reading instructions

---

## Does it generate UUIDs for addons?

Never.

All UUIDs come directly from `manifest.json`.

If a UUID is missing or invalid, the AI reports the issue.

---

## Can I use this with OpenCode, Cursor, Aider, etc?

Yes.

Any AI that respects `AGENTS.md` can use this system.
