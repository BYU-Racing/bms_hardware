# Tractive Battery Module Voltage Sense, Thermal and Isolation Design Decisions
 
Oct 27, 2026 · @Rugby
 
## Scope
 
These decisions cover the BMS sense and balance connections, thermistor placement, the per-module FPC, and the busbar-to-case thermal and isolation stack for the BYU Racing accumulator (108S4P, nine 12S4P modules, about 454 V max). Each module has busbars on both cell end faces, so an FPC runs on both faces. Busbars are 0.005 in (0.127 mm) Ni200/201 shim, spot welded to the cells. The aluminum case is the only heat sink for the cells. Rule references are to the FSAE 2027 V1.0 rules.
 
## 1. Sense and balance joint
 
**Decision:** Each busbar has an integral thin strip that stays nearly flat, jogs up through a plated slot in the FPC, folds over onto a top pad, and is hand soldered there. The strip is pre-tinned with a nickel-rated flux before the busbars are welded to the cells.
 
**Why:**
 
- No extra welds on the pack, and no separate tab parts.
- The fold is a lap joint and a mechanical lock that keeps the FPC from lifting.
- The FPC sits flat and low, which the thermistors and gap pad need.
- Pre-tinning moves the hard soldering (nickel oxide, activated flux, long dwell) to the bench, before any cells are attached. On the pack it is a short tin-to-tin joint.
- EV.5.2.4 explicitly allows soldering BMS voltage sense connections, since they are not in the high current path.
**Rejected:** a 90 degree strip through a slot (fatigues at the bend root), lap soldering on the busbar through holes (heat goes straight into the cells), and nickel tabs welded onto the busbars (extra weld steps).
 
**Footprint:**
 
| Feature   | Spec                                                                                           |
|-----------|------------------------------------------------------------------------------------------------|
| Slot      | Strip width + 0.5 to 0.8 mm long, fab minimum width (about 0.5 to 0.6 mm), plated if available |
| Pad       | Strip width + 1 mm wide, 5 to 6 mm long, slot at the busbar end                                |
| Layers    | Pad on both layers, tied with 2 to 4 vias                                                      |
| Coverlay  | Overlaps pad edges by 0.2 to 0.3 mm                                                            |
| Stiffener | Under the pad with a matching slot, a couple mm past the pad                                   |
| Fuse      | On the stiffened area next to the pad: 250 mA inner taps, 500 mA end taps                      |
 
All of these are mechanical. Balance current is only about 130 mA (33 ohm at 4.2 V).
 
## 2. FPC architecture
 
**Decision:** One 2-layer FPC per module face, shaped as a lattice with a window over every cell footprint. The FPC has no copper hatch plane.
 
- **Spine** along the slave board edge, outside the cell footprints, ending at a locking connector or a soldered tail.
- **Branches** in the gaps between busbars, so they sit over no busbar and across no potential difference.
- **Short fingers** to each sense pad and thermistor paddle, over the busbar webs between cells, never over a cell terminal.
- **A cross-tie** along the far edge to hold the shape during install.
- **S-bends** (one full S, 3 to 4 mm wide, bend radius of at least 2 to 3 mm) in every finger and in the cross-tie, so each busbar can move independently. No vias, parts, stiffener or pour in the bends.
- **Bottom coverlay** over everything except the pads, so the FPC can't short to a busbar it lies on.
**Why:** The lattice keeps polyimide (0.12 W/m·K) out of the main heat path over the cell terminals and still gives one part per face to install and remove. A full-coverage FPC would have roughly tripled the busbar-to-case thermal resistance. The copper hatch would not help through-thickness heat flow, and a plane spanning several busbars could short cells through two coverlay defects.
 
## 3. Thermistors
 
**Decision:** There's one NTC per parallel group, 12 per module. Each NTC sits on a small paddle (about 5 x 6 mm) at the end of a finger, lying on the negative terminal busbar less than 10 mm from that group's negative-side spot weld. The paddles go on whichever face holds that group's negative terminal, so they're split across both FPCs. Each NTC goes on the top layer with an isolated copper island under it, and the FPC's own polyimide and coverlay isolate it from the busbar.
 
**Why:**
 
- EV.8.5.3 and EV.8.5.4 require measurement at the negative terminal, either directly or on its busbar less than 10 mm from the weld.
- EV.8.5.7 requires isolation, either between the sensor and the cell or in the sensing circuit. Isolating at the sensor keeps the NTC net off busbar potential.
- The gap pad clamps each paddle onto its busbar, so no extra lid features are needed.
- A paddle covers a negligible area, so the windows over the cells stay open.
## 4. Thermal path and isolation
 
**Decision:** Each busbar face that touches the outer aluminum case gets about 1 mm of Laird Tflex P300, with its polyimide liner facing the busbars. Internal walls between two modules are lined with Formex only. Standard Kapton tape stays out of the heat path.
 
| Interface                                                | Stack (busbar to wall)                                   | Role                                |
|----------------------------------------------------------|----------------------------------------------------------|-------------------------------------|
| Busbar face to outer case                                | Lattice FPC, Tflex P300 (liner toward busbars), aluminum | Heat path and isolation             |
| Busbar face to internal wall                             | Formex sheet                                             | Isolation and EV.5.2.3 barrier only |
| Side walls, corners, module terminals, case penetrations | Formex                                                   | Isolation where no pad reaches      |
 
**Why P300 (vs. the current P100 and Bergquist TGP 3000):**
 
- It has 3 W/m·K, about 2.5x P100's 1.2. Rth at 40 mil and 10 psi is 0.592 °C·in²/W, vs. 1.50 for P100.
- It's the same family and handling as P100, so it's close to a drop-in swap.
- The integrated polyimide liner resists burrs and gives a defined dielectric barrier. TGP 3000 would need a separate insulator.
- It's soft (Shore 00 of 30), so it can absorb the 0.3 to 0.5 mm steps from paddles, joints and folded strips.
- Its ratings are UL94 V-0, -40 to 125°C, and breakdown above 5 kV.
**Why Formex on the internal walls:** It gives a clear, inspectable EV.5.2.3 barrier between modules. It's cheap, foldable and non-hygroscopic. The tradeoff is accepted: cells are cooled from the outer-case end only, so there's no second heat path through the internal walls.
 
**Kapton MT contingency:** If testing shows P300 alone is not enough (liner cut-through at weld nuggets, solder joints or strip folds, or an inspector asking for a second barrier), add 1 mil Kapton MT film ([CS Hyde 18-1F-MT](https://catalog.cshyde.com/printitem/films/igh-performance-film-kapton-polyimide-film-type-mt/1-mil-kapton-mt-18-1f-mt-12x12)) on the aluminum under the pad. At 0.46 W/m·K it adds about 5% to the pad's resistance. Use bare film rather than the adhesive tape version.
 
## 5. Rules check and open items
 
| Rule                | Requirement                                                                  | How it's met                                                        |
|---------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------|
| EV.5.2.2.a          | Poles insulated from a conductive case wall, rated for max TS voltage        | P300 breakdown above 5 kV vs. about 454 V max                       |
| EV.5.2.2.c          | Conductive penetrations can't puncture the barrier                           | Formex or standoffs at every bolt or insert                         |
| EV.5.2.3            | Nonflammable (UL94 V-0) insulation between modules and on top of each module | Formex on internal walls, P300 (V-0) on outer faces                 |
| EV.5.2.4            | No soldering in the high current path                                        | Only the BMS sense joints are soldered, which is explicitly allowed |
| EV.7.2              | Insulation rated to at least 90°C, tape not the only insulation              | P300 is rated to 125°C, and no tape is relied on                    |
| EV.8.5.4 / EV.8.5.7 | NTC on the negative busbar less than 10 mm from the weld, isolated           | Paddle placement and FPC polyimide                                  |
 
**Open items:**
 
- [ ] Confirm the Formex grade's datasheet shows UL94 V-0, not only VTM-0 (F.1.18)
- [ ] Ask an inspector whether an NTC through FPC coverlay counts as "direct contact" (EV.8.5.4)
- [ ] Confirm the 3D printed cell holder material, if any module-to-module boundary relies on it (EV.5.2.3)
- [ ] Oversize the P300 several mm past every live feature at the module perimeter
- [ ] Check P300 for liner damage after the first assembly, and decide on the Kapton MT backer
- [ ] Size the case gaps for 20 to 30% compression of the P300 across the cell length tolerance
- [ ] Put the P300 and Formex datasheets and a per-wall stackup drawing in the ESF
**Sources:** [FSAE Rules 2027 V1.0](https://www.fsaeonline.com/cdsweb/gen/DocumentResources.aspx) (provided PDF), [Tflex P300 datasheet](https://www.farnell.com/datasheets/3190615.pdf), [Tflex P100 datasheet](https://www.laird.com/sites/default/files/2026-08/A17466-00%20-Tflex%20P100%20DS-03302026.pdf), [Kapton HN datasheet](https://docs.rs-online.com/c6e2/0900766b80659d8c.pdf), [Kapton MT](https://www.dupont.com/products/kapton-mt.html), [Formex GK datasheet](https://www.synflex.com/fileadmin/user_upload/01_SynFlex/PDF/Datenblaetter/Englisch/Formex_GK_EN.pdf), [Busbar shim (McMaster 9707K14)](https://www.mcmaster.com/9707K14/)
 
