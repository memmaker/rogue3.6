# Rogue 3.6.4 — RVIP handover (2026-09-25)

Ported after Rogue 5.4 (`~/Games/rogue5.4`) and the Advanced Rogue line;
3.6 is the ancestor of Advanced Rogue, so it has its data model
(`struct linked_list`, `OBJPTR`, `cw`/`mw`/`hw`, real map in `stdscr`).

- `rvip.c` = UltraRogue's version (linked lists) with 5.4's item actions
  (`P`/`R` rings, `c` call). Help list groups by first key.
- `port/tiles.c` = 5.4's (monsters by letter) with linked lists and
  `stdscr` as the floor map. `OBJPTR(x)->f` binds wrongly (no outer
  parentheses in the macro): write `(OBJPTR(x))->f`.
- Weapon/armour names are plain string arrays (`w_names`, `a_names`):
  `strings()` in `port/mktiles.py`.
- One status line: `-DWC_STATUS_ROWS=1`; no message window (`msgw` empty).
- `mdport.h`: no `crypt.h`/`term.h` on macOS/web; no setuid/fork on the web.
- **Upstream bug** (same as 5.4): `rs_read_daemons()` cleared `d_list[cnt]`
  after the loop. Moved inside. `mdport.c` had `return(1)` without `;` in
  a branch only the web build compiles.
- Prompt line (RVIP step 5 / W4, 2026-09-26): the live message row is shown in a
  box over the map by `RvipWM.prompt` (rvip-wm.js). A key hides it only while
  the game waits for a command, so a question stays up until answered.
  Here: `be_prompt(r)` from `msg_refresh()` in `port/wcurses.c` (row 0 text),
  `js_key(wc_cmd_prompt)` in `port/be_web.c`; `be_x11.c` has an empty stub.
