# Agent Instructions

This file contains patterns and instructions for common tasks.

## Minecraft Bedrock Addon Installation

### Overview

Minecraft Bedrock addons (`.mcaddon` and `.mcpack` files) should be installed in appropriate pack folders:
- **Behavior Packs** → `behavior_packs/`
- **Resource Packs** → `resource_packs/`

**IMPORTANT**: Never modify or delete existing behavior packs and resource packs that come from the bedrock-server-1.21.131.1.zip installation. These are the base game files and should remain untouched.

### Naming Convention

Each addon should be installed in a folder named after its source file (without the extension), with unicode characters removed. The folder name should match the original addon file name for easy identification.

**Examples:**
- `BSCompass4.4.mcaddon` → `BSCompass4.4/` in both `behavior_packs/` and `resource_packs/`
- `✦ waypoint pocket ⟦v1.1⟧ (BH) ▸ MCPE ⟦1.21.130⟧.mcaddon` → `Waypoint Pocket BH v1.1/` in `behavior_packs/` (unicode removed)
- `✦ waypoint pocket ⟦v1.1⟧ (RS) ▸ MCPE ⟦1.21.130⟧.mcaddon` → `Waypoint Pocket RS v1.1/` in `resource_packs/` (unicode removed)

### Addon Types

**`.mcaddon` files** typically contain both behavior and resource packs:
- Often have separate `bp/` and `rp/` directories
- Extract `bp/` contents to `behavior_packs/[AddonName]/`
- Extract `rp/` contents to `resource_packs/[AddonName]/`

**`.mcpack` files** contain either behavior or resource packs (not both):
- Check the manifest to determine pack type
- Extract to `behavior_packs/[AddonName]/` or `resource_packs/[AddonName]/` accordingly

### Pack Type Indicators

**Behavior Pack indicators:**
- Directory names containing `bp/`, `BH`, or `B`
- Behavior pack files usually contain: `entities/`, `items/`, `recipes/`, `scripts/`, `functions/`
- Manifest type: `"data"` or `"script"`

**Resource Pack indicators:**
- Directory names containing `rp/`, `RS`, or `R`
- Resource pack files usually contain: `textures/`, `models/`, `animations/`, `ui/`, `sounds/`
- Manifest type: `"resources"`

**Duplicate addons:**
- Behavior pack version: `BP`, `BH`, or `B` suffix
- Resource pack version: `RP`, `RS`, or `R` suffix
- Example: `Addon BP 1.21.130` and `Addon RP 1.21.130`

### Unicode Character Removal

When addon filenames contain unicode characters, remove them from the installed folder name:

**Common unicode characters to remove:**
- ✦ (U+2726)
- ⟦ (U+27E6)
- ⟧ (U+27E7)
- ▸ (U+25B8)
- § (color codes in manifest names)

**Example transformation:**
- `✦ waypoint pocket ⟦v1.1⟧ (BH) ▸ MCPE ⟦1.21.130⟧.mcaddon` → `Waypoint Pocket BH v1.1`

### Installation Steps

1. **Check for conflicts**: Verify target folders don't already exist
   ```bash
   ls -d behavior_packs/[AddonName] resource_packs/[AddonName]
   ```

2. **Extract to temp location**: Use temporary directory to handle nested structures
   ```bash
   mkdir -p /tmp/addon
   unzip -q -o [AddonName].mcaddon -d /tmp/addon
   ```

3. **Identify pack type**: Check directory structure or manifest
   ```bash
   ls /tmp/addon/
   # Look for bp/, rp/, B, R, BH, RS indicators
   unzip -l [AddonName].mcaddon | grep manifest.json
   ```

4. **Copy to destination**: Extract to appropriate pack folder
   ```bash
   mkdir -p "behavior_packs/[AddonName]" "resource_packs/[AddonName]"
   cp -r /tmp/addon/[BehaviorDir]/* "behavior_packs/[AddonName]/"
   cp -r /tmp/addon/[ResourceDir]/* "resource_packs/[AddonName]/"
   ```

5. **Flatten nested structures**: Remove unnecessary nested directories
   ```bash
   cd "behavior_packs/[AddonName]/NestedDir"
   mv * ..
   rmdir "behavior_packs/[AddonName]/NestedDir"
   ```

6. **Remove unicode characters**: Extract from unicode-named directories
   ```bash
   cp -r /tmp/addon/"#U2726 Waypoint..."/* "behavior_packs/Waypoint Pocket BH v1.1/"
   ```

7. **Verify installation**: Ensure manifest.json exists in each pack
   ```bash
   ls behavior_packs/[AddonName]/manifest.json
   ls resource_packs/[AddonName]/manifest.json
   ```

8. **Clean up**: Remove temporary extraction directories
   ```bash
   rm -rf /tmp/addon
   ```

### Verification

After installation, verify that:
- Each extracted pack has a `manifest.json` file
- Pack names match the source file names (with unicode removed)
- No duplicate pack names exist (except vanilla/chemistry packs)
- All required directories are present based on pack type

### Enabling Packs for Worlds

To make addons active in a specific world, you need to enable them in the world's pack configuration files:

1. **Extract UUIDs and versions**: Get pack identifiers from manifests
   ```bash
   python3 -c "import json; f='path/to/manifest.json'; d=json.load(open(f)); print(d['header']['uuid'], d['header']['version'])"
   ```

2. **Add to world configuration**: Edit `worlds/[WorldName]/world_behavior_packs.json` for behavior packs and `worlds/[WorldName]/world_resource_packs.json` for resource packs

3. **Format for entries**: Each pack entry follows this format:
   ```json
   {
     "pack_id": "uuid-here",
     "version": [major, minor, patch]
   }
   ```

4. **Example using Python**:
   ```python
   import json

   # Read existing packs
   with open('worlds/Bedrock level/world_behavior_packs.json', 'r') as f:
       packs = json.load(f)

   # Add new pack
   packs.append({
       "pack_id": "5f0558a1-338a-44d4-ad9b-ee5a773ace35",
       "version": [0, 0, 1]
   })

   # Write back
   with open('worlds/Bedrock level/world_behavior_packs.json', 'w') as f:
       json.dump(packs, f, indent=2)
   ```

5. **Duplicate prevention**: Check if pack UUID already exists before adding to avoid duplicates

### Common Issues

**Nested directory structures**: Some archives have additional version subdirectories that should be flattened.

**Unicode characters**: Use `unzip -l` to view the actual paths, as some tools may display unicode differently.

**Multiple packs in one file**: `.mcaddon` files often contain both behavior and resource packs that need to be extracted separately.

**Manifest location**: Always check where `manifest.json` is located within the archive structure.

### Complete Installation Workflow

1. Extract addon from mods folder to `behavior_packs/` and/or `resource_packs/`
2. Fix unicode characters in folder names if needed
3. Verify manifest.json exists in each installed pack
4. Extract UUID and version from each pack's manifest.json
5. Add pack entries to world's `world_behavior_packs.json` and/or `world_resource_packs.json`
6. Verify packs are active by checking world configuration files
