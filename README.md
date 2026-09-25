# Rogue 3.6 — RVIP port

Upstream: Rogue 3.6.4 (Toy, Arnold, Wichman; Berkeley 1981), from the Roguelike
Restoration Project: https://github.com/RoguelikeRestorationProject/rogue3.6/tree/f36912c

**Our changes:** https://github.com/memmaker/rogue3.6/compare/f36912c...master
(commit 1 is the untouched upstream; everything after it is ours).

- `port:` builds on macOS/arm64 and WebAssembly, curses shim (`port/`) with
  an X11 frontend, NetHack tiles (`port/mktiles.py`); fixes an upstream
  out-of-bounds write when restoring a save (`rs_read_daemons`).
- `RVIP:` auto-explore (`x`), `<`/`>` walk to known stairs, Enter command
  menu, inventory with a cursor, sound events (`rvip.c` + small hooks).
- `web:` browser build (`web/build.sh`), played at https://ruzzoli.de/roguelikes/rogue36/

Build: `make rogue36-x11` (XQuartz), `./play.sh`; web: `sh web/build.sh`, `web/deploy.sh`.
Notes for the next person: `HANDOVER.md`. Process: `~/Games/RVIP.md`, `~/Games/rogue2wasm.md`.
