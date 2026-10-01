# Auto Saramed & Auto Moon's Eyrie

Ported from Project Rain (`reference/project-rain/src/automation/persistent_tasks/auto_saramed.lua`
and `auto_mooneyrie.lua`) into a new hub module, `Features/Automation/PveFarm`, built the same way
as `TitusFarm`. It uses the hub's own pieces: ServerHop, PersistentData, AntiAFK, Finder, InputClient
and the Toggles. Its saved state (`pfdata`) is resumed from `Lycoris.init` after a hop or dungeon teleport.

**Untested in game.** It compiles (`luau-compile`) and lints clean (`luau-analyze`), nothing more.

## UI: Auto tab → "Saramed & Moon's Eyrie"
- **Start Auto Saramed** (double-click), with sliders for **Minimum Health** (25%) and
  **Attach To Mob Distance** (8). These values are saved with the farm when it starts.
- **Start Auto Moon's Eyrie** (double-click)
- **Stop PvE Farm**. The on-screen overlay also has a Stop button, plus stage, cycle count and elapsed time.

It won't start while the Titus Farm or Auto Ferryman still has saved state. Stop those first.

## Auto Saramed
1. **Eastern Luminant:** if water or hunger is under 25%, it eats Pomar / Mushroom Soup / Bread from
   your inventory, collects Pomars, and drinks at the nearest well. Carnivores skip food. Then it flies
   (high in the sky) to Malisae and picks "Enter alone."
2. **Inside Saramed:** you need a Pickaxe; the farm waits until you have one. Each floor it presses
   the nearest drill switch, then kills every mob (attached above it, or below buncles and knights)
   using the hub's left click. Then it mines Magma Ore until the fuel bar is full, using auto-deposit
   via touch, and opens the floor chest.
3. At max depth (2.00), or when health drops under the minimum, it uses the radio to ride back up
   and rests at the campfire until it's at 50% HP.
4. Hungry or thirsty with no food left in the dungeon: it walks to the exit and resets (dies) to
   go refill in the overworld.

## Auto Moon's Eyrie
1. Below 35% HP: it flies to the campfire near Moon's Eyrie and rests until it's at 50%.
2. It flies to Moon's Eyrie, opens the Moonseye door ("[Interact]") and fights the moonknight from
   above. It jumps higher while the knight's kick animation plays, and gives up if the knight takes
   no damage for 20s. Then it picks up loot drops, opens the chest, and kills any second knight.
3. If it's in danger it flies up until the danger timer runs out, then server hops. **One knight per server.**

## Shared behaviour
- Turns on Fly, NoClip, NoFallDamage and NoStun, and puts them back how they were on stop.
- Server hops if a player is within 200 studs of you or your destination.
- **Watchdog:** if a stage takes longer than 4 minutes, it hops. After 3 errors in a row, it stops.
- **Chest loot is left to Auto Loot.** Turn on Auto Loot and set its filters for what you want
  kept. The farm closes the chest after 5s.
- If you die without leaving the server, it waits for respawn and carries on.

## Differences from Project Rain
- Bread crafting (wheat → bread) was not ported. It only eats existing food, Pomars and well water.
- In the Etrean Luminant it stops. Rain auto-teleports to the Eastern Luminant using its own teleport feature.
- Rain's `aa_bypass` flag, disconnect-handler hop and webhook were not ported.
- Timeouts were added everywhere Rain waited forever.
