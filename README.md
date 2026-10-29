# Mwangi Compendium

A Foundry VTT module for the **Pathfinder 2e** system containing homebrew items made for our campaign in the Mwangi Expanse. It is hosted on [The Forge](https://forge-vtt.com/) and installed in our game via manifest URL.

The module adds a single Item compendium, **GG Items**, which contains the weapons, equipment, spells, actions and effects handed out during the campaign. Item names and descriptions are partly in German.

## Requirements

- Foundry VTT **v12**
- Game system **Pathfinder 2e** (`pf2e`)
- Optional: [Automated Animations](https://foundryvtt.com/packages/autoanimations) (with [Sequencer](https://foundryvtt.com/packages/sequencer) and an animation library like JB2A) for the custom attack and spell animations

## Installation

Install the module with this manifest URL:

```
https://github.com/Hydrair/mwangi-compendium/releases/latest/download/module.json
```

- **The Forge:** *My Foundry* → *Game Configuration* → *Add-on Modules* → *Install Module* → paste the manifest URL
- **Self-hosted Foundry:** *Setup* → *Add-on Modules* → *Install Module* → paste the manifest URL

Then enable **Mwangi Compendium** in your world under *Manage Modules*. Players get Observer access to the compendium, Assistant GMs get Owner access.

## Contents

Each item lives in its own folder in the compendium, together with its linked actions, feats and effects.

### Weapons

| Item | Level | Rarity | Included |
| --- | --- | --- | --- |
| Feuriger Zornschnitter | 8 | Unique | Infernoschutz (action), Lavarüstung, Magmarüstung (effects) |
| Solariswerfer | 5 | Unique | Solarfeuer (action), Solarflare (effect) |
| Schattenbogen | 10 | Unique | Schattennova (spell) |
| Takahashi's Sternenkatana | 10 | Unique | Sternenschimmer (spell) |
| Umbralklingen | 10 | Unique | Schattenschleier (spell), Concealed (condition) |

### Consumables

| Item | Level | Rarity | Included |
| --- | --- | --- | --- |
| Drachenformtrank | 0 | Unique | Verwandlung: Grüner Drache (effect) |

### Immergruen

| Item | Level | Rarity | Included |
| --- | --- | --- | --- |
| Bracers of Tactical Mastery | 3 | Uncommon | Tactical Precision, Reposition (actions), feat, effect |
| Hunter's Stone | 3 | Uncommon | Favored Quarry, Tracking Sense (actions), feat, effects |
| Mindwoven Circlet | 3 | Uncommon | Concentration (action), Mind Reading (spell), feat, effect |
| Relic of the Veiled Fates | 3 | Uncommon | Foresight, Deal with the Ancestors (actions), feat, effects |

## Development

The compendium is stored as YAML in `src/packs/` so changes can be reviewed in git. The compiled LevelDB pack that Foundry loads lives in `dist/packs/`.

```bash
npm install
```

| Script | What it does |
| --- | --- |
| `npm run pullYMLtoLDB` | Compiles the YAML files in `src/packs/` into `dist/packs/` |
| `npm run pushLDBtoYML` | Extracts packs from `foundryImport/` (a copy of the pack exported from Foundry) into YAML in `src/packs/` |

Typical workflow:

1. Edit items in Foundry, then copy the `gg-items` pack folder from your Foundry data into `foundryImport/`
2. Run `npm run pushLDBtoYML` to update the YAML files
3. Run `npm run pullYMLtoLDB` to rebuild `dist/packs/`
4. Commit your changes

Item images go into `dist/img/`.

## Releasing

Pushing a tag that starts with `v` (for example `v1.2.8`) triggers the GitHub Action in `.github/workflows/assets.yml`. It sets the version and URLs in `module.json`, zips `module.json`, `packs/` and `img/`, and attaches `module.json` and `module.zip` to a GitHub release. Tags ending in `-beta` are ignored.

```bash
git tag v1.2.8
git push origin v1.2.8
```

After a release, update the module in Foundry/The Forge to get the new items.
