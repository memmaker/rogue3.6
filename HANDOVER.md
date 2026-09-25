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
