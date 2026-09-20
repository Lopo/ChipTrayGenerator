# Chip Tray Generator

A single-file, parametric generator for stackable, 3D-printable storage trays for retro processors and chips:
PGA / LGA CPUs (386 to Athlon 64 / LGA 775), QFP and PLCC chips, and DIP chips in channels.

**Use it online:** https://lopo.github.io/ChipTrayGenerator/ — or download `index.html` and open it locally.
No build, no server; three.js is loaded from a CDN for the preview.

[![Chip Tray Generator](docs/screenshot.png)](docs/screenshot-full.png)

## What it does

- Pick a package, set rows × columns, walls, floor, pocket depth and print tolerance.
- Live WebGL preview (rotate / zoom / pan, isometric, top and bottom views).
- **OpenSCAD export** (`.scad`, fully parametric, exact geometry, engraved label) and a quick **STL export** straight from the preview.
- **Stacking:** every tray has a 2 mm rim on top and a matching recess underneath, so trays nest.
  Tray heights may differ; only the outer size must match. Turn on **Fixed outer format** to give trays for different
  packages the same footprint — pockets are centred and the leftover goes into the outer wall. "Max pockets that fit"
  fills the format.

## How the chips are held

| Family | Support | Why |
|---|---|---|
| Ceramic PGA (386, 486, Pentium, K6, Athlon) | central pedestal inside the pin-free centre, push-out hole | pins hang free, nothing touches them |
| FC-PGA 370 | edge ledge under the substrate rim, or a hollow pedestal | Intel puts capacitors on the underside inside a 17.78 mm square |
| Socket 423 / 478 / 604 / 754 / 939 / AM2 / AM3 / LGA | edge ledge only | underside is covered by capacitors or lands |
| QFP / PLCC | pad under the plastic body, leads float | same principle as JEDEC shipping trays |
| DIP | centre rail between the pin rows, chips end to end in a channel | same principle as a shipping tube |

The generator warns when a support would touch pins, capacitors or lead feet.

## Where the numbers come from

Package sizes and pin-free centres are taken from manufacturer datasheets, not guessed:

| Package | Source |
|---|---|
| PGA132 (386DX) | Intel 386DX datasheet 231630 (14×14 @ 2.54 mm, 3 rows, 1.36") |
| PGA168 (486) | Intel packaging databook (1.75", 44.19–45.21 mm) |
| SPGA296/321 (Socket 5/7) | Intel Pentium datasheet 241997 Tab. 19; Intel AP-579 Socket 7 pin-side view; AMD K6-2 datasheet 21850 Tab. 73 / Fig. 113 |
| PPGA / FC-PGA 370 | Intel Pentium III PGA370 datasheet 245264 Tab. 35 / Fig. 23, 31 |
| Socket A 462 | AMD Athlon XP Model 8 datasheet 25175 Tab. 21 / Fig. 14, 17 |
| Socket 423, 478, 604, 754/939/940, AM2/AM3, LGA 775 | Intel / AMD published package sizes; underside treated as populated |
| QFP / PLCC | JEDEC MS-022, MS-026, MS-018, MS-016, MO-069 |
| DIP | JEDEC MS-001 (0.3"), MS-011 (0.6"), MO-016 class (0.9") — maximum body lengths |

Pedestal sizes for the older PGAs were read off the pinout drawings (pin-free centre minus one pin diameter of margin).
The mobile / late-desktop entries use conservative defaults because their substrate rim is narrow; keep the tolerance
at 0.3 mm or less there, as the tool tells you.

## Printing notes

- Default tolerance is +0.5 mm per pocket; measure one printed pocket and adjust.
- Supports are 4 mm high for PGA (pin length is 3.05–3.30 mm), 1.5 mm for QFP/PLCC, 4 mm for DIP.
- The OpenSCAD export is a clean manifold. The STL from the preview is a union of touching solids, which slicers
  accept, but use the SCAD output when you want to edit anything.
- Nothing here has been verified on a printed tray for every package yet — if you print one, please report back.

## License

MIT — see `LICENSE`. three.js (MIT) is loaded from cdnjs / jsDelivr at runtime.
