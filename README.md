# Jawless Jockey Hub

- `JawlessJockeyHub.lua`: the bundled hub script (luabundle). Each module is registered with `__bundle_register("Path/Name", ...)`, and the entry point is `__root` → `Lycoris.init`.
- `docs/`: changelogs and session notes.
  - `docs/CHANGELOG-titus-farm.md`: the Titus Farm port and the fixes copied over from the older build.
  - `docs/session-2026-09-29-titus-farm.md`: the full conversation behind those changes.
  - `docs/CHANGELOG-saramed-eyrie.md`: the Auto Saramed and Auto Moon's Eyrie port.
- `reference/project-rain/`: Project Rain open-source code, kept as a reference for porting features. It is not loaded by the hub.
