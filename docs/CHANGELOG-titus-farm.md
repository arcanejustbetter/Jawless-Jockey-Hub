# Changelog: Titus Farm port & script fixes (2026-09-29)

All changes are in `Preprocessed_Bundled (2).lua`. None of this has been tested in game yet.

## Copied over from version (3)

- `start:FireServer()` → `start:FireServer(true)` in the 4 EchoFarm / Depths "Requesting start" calls.
- **Direct dodge (`InputClient.dodge`)**: now gets the `Dodge` remote from `CharacterHandler.Requests` and sends `dodge:FireServer("roll" | "waterdash", { ancient, spin_attack, in_air })` instead of `dodge:FireServer("roll", nil, nil, false)`.
- **Feint release**: `feintReleaseRemote:FireServer()` (no arguments).
- **End Slide**: `serverSlideStop:FireServer()` instead of `FireServer(false)`.
- **`DEBUGGING_MODE`**: set to `false` in all 4 modules.

Branding, folder names and the log prefix were left as Jawless Jockey Hub.

## New: Titus Farm (ported from Project Rain)

New module `Features/Automation/TitusFarm`, added to the **Auto** tab as a **Titus Farm** section:

- **Start Relic Farm**: enters the Titus dungeon, sits under Titus until the fight ends, loots the relics picked in **Relics To Loot**, then dies and hops to a new server. Refills water if it's low and deposits anything in **Bank At 25** once you hold 25+. Stops if the bank is full.
- **Start Echo Farm**: creates a character (Merit spawn, Sword, all modifiers), runs Titus, loots everything, uses the Idol and the Enchant Stone, then wipes the slot and repeats. Needs the Fort Merit spawn unlocked.
- **Stop Titus Farm**, plus a status overlay showing the stage, cycles, elapsed time and a Stop button.

How it works:
- Built on the hub's own `ServerHop`, `Wipe`, `PersistentData` (`tfdata`) and `AutoLoot`, and its Fly / NoClip / NoFallDamage / PathfindBreaker toggles.
- Resumes automatically after every hop or wipe; this is hooked into `Lycoris.init`.
- Hops if a player is within 200 studs or the fight takes over 30 s. After 3 errors in a row it stops.

Not ported:
- Project Rain's Discord webhook, the echoes-per-minute counter, the relic farm's "Wipe Character" option, and the `no_one_bit` and `jesus` features.

## Backups

These were kept locally and are not in this repo:
- `Preprocessed_Bundled (2).backup.lua`: the original, before any changes.
- `Preprocessed_Bundled (2).before-titus.lua`: after the fixes, before the Titus Farm.
