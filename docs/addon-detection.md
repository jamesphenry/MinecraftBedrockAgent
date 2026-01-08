# Addon Detection and Classification

## Supported Archive Types

AI agents may encounter addons packaged as:

* `.mcaddon`
* `.mcpack`
* `.zip` (including renamed `.mcaddon` / `.mcpack` files)

There is no enforced internal standard.

## .mcaddon Files

Typically contain multiple packs in a single archive.

Common layouts include:

* `bp/` for behavior packs
* `rp/` for resource packs

Rules:

* All contained packs must be detected
* Each pack must be extracted independently
* Pack contents must be installed into the correct destination directory

## .mcpack Files

Contain exactly one pack.

Pack type must be determined by:

* Manifest `type` field
* Directory contents
* Known file indicators

## Behavior Pack Indicators

Common indicators include:

* Directories: `entities/`, `items/`, `functions/`, `scripts/`, `recipes/`
* Manifest types: `data`, `script`

## Resource Pack Indicators

Common indicators include:

* Directories: `textures/`, `models/`, `animations/`, `ui/`, `sounds/`
* Manifest type: `resources`

## Unicode Handling

Addon filenames and internal paths may contain unicode characters.

Rules:

* Unicode characters must be removed from installed folder names
* Internal file contents must not be modified
* Resulting folder names should remain readable and traceable
