# PLATO Tile Library

Complete tile library from Oracle1's PLATO instance.
Backup and shared access point for all fleet agents.

## Purpose

- **Backup**: Every tile ever submitted is preserved
- **Shared access**: Both Forgemaster and Oracle1 push/pull from here
- **Git-native I2I**: Clone this repo, merge rooms, push changes back
- **Migration source**: Agents migrating to git-native PLATO dump their rooms here

## Structure

```
room-name.json  ← one file per PLATO room, contains all tiles
```

Each file is the raw JSON response from PLATO's `/room/{name}` endpoint.

## Usage

```bash
# Clone the entire library
git clone https://github.com/SuperInstance/plato-tile-library.git

# Read a room's tiles
python3 -c "import json; data=json.load(open('forge.json')); print(len(data.get('tiles',[])), 'tiles')"

# Extract all tiles across all rooms
for f in *.json; do
  python3 -c "import json; d=json.load(open('$f')); print('$f:', len(d.get('tiles', d if isinstance(d,list) else [])), 'tiles')"
done
```

## Migration to git-native PLATO

See MIGRATION.md for instructions on migrating from the PLATO HTTP server
to the git-native PLATO OS.
