# Bedrock Server Layout

## Canonical Directory Structure

A typical Minecraft Bedrock Dedicated Server directory layout:

```
bedrock-server/
├── AGENTS.md
├── bedrock_server
├── server.properties
├── behavior_packs/
├── resource_packs/
├── worlds/
└── mods/
```

## behavior_packs/

Contains all installed **Behavior Packs**.

Includes:

* Vanilla packs from the official Bedrock server distribution
* Custom behavior packs provided by addons

### Safety Rule

Vanilla behavior packs provided by the official server distribution **must never be modified or deleted**.

## resource_packs/

Contains all installed **Resource Packs**, including:

* Textures
* Models
* Animations
* UI assets

Vanilla resource packs are treated as read-only.

## worlds/

Each subdirectory represents a single world.

Relevant configuration files:

* `world_behavior_packs.json`
* `world_resource_packs.json`

These files determine which packs are enabled per world.

## mods/

A staging directory for unprocessed addon archives.

Rules:

* The AI may scan and extract from this directory
* The AI must not treat this directory as an installed state
* Files may remain here after installation unless explicitly removed
