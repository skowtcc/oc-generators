# oc-generators

Data for the OC (original character) generators on [skowt.cc](https://skowt.cc). Pick a game, roll, and you get a random set of traits to build a character from: element, weapon, faction, looks, personality and so on.

## Games

-   Genshin Impact (`games/genshin-impact.json`)
-   Honkai: Star Rail (`games/honkai-star-rail.json`)
-   Zenless Zone Zero (`games/zenless-zone-zero.json`)
-   Project Sekai (`games/project-sekai.json`)

## Layout

```
shared/    options every game uses, in three groups
  identity.json      Gender, Pronouns, Age, Height
  appearance.json    Hair Type, Hair Style, Hair Color, Eye Color, Aesthetic
  personality.json   Personality Type
games/     one file per game
schema/    JSON Schemas for both kinds of file
```

Each option has a name and the entries a roll can pick from. A game file adds its display name, the shared groups it uses, and only its own options:

```json
{
    "$schema": "../schema/game.schema.json",
    "name": "Genshin Impact",
    "shared": ["identity", "appearance", "personality"],
    "options": [
        {
            "name": "Element",
            "entries": ["Pyro", "Hydro", "Electro"]
        }
    ]
}
```

A game's full list is its own options plus the options of every group in `shared`.

`schema/game.schema.json` and `schema/shared.schema.json` describe the files (JSON Schema 2020-12). Each file points at its schema through `$schema`, so editors validate as you type.

Game-specific lists only include released content.

## Use on skowt.cc

skowt.cc pulls this repo in as a git submodule and imports the JSON at build time. Clone skowt.cc with `git clone --recurse-submodules` to get it.

## License

Anyone can use this data in their own projects. Please credit [skowt.cc](https://skowt.cc) if you do.
