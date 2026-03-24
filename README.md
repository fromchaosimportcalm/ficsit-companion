# FICSIT Companion

A single-file production suite for **Satisfactory v1.0** (with v1.2 experimental recipes tracked). No install, no server, no dependencies — open the HTML file in any browser and start planning.

![FICSIT Companion](https://img.shields.io/badge/Satisfactory-v1.0%20%2B%201.2%20EXP-f5a623?style=flat-square) ![Vanilla](https://img.shields.io/badge/recipes-vanilla%20base-00d4ff?style=flat-square) ![Single file](https://img.shields.io/badge/format-single%20HTML-39d98a?style=flat-square)

To run live, visit https://fromchaosimportcalm.github.io/ficsit_companion/

---

## What's in it

Four tabs, one persistent left panel, one shared recipe database. Every tab reads from the same data — change a recipe once and both the Planner and Reference update automatically.

### ⚙ Planner
Back-calculates the full production chain from any target output. Set a production rate for any item and the resolver walks the entire dependency tree back to raw ore extraction rates, accounting for all intermediate steps.

- **Milestone presets** for Phase 1–5 with sensible default rates
- **Custom targets** — any item, any rate, addable individually or on top of a milestone
- **Selectable alt recipes** — switch any recipe in your chain to an alternate variant; the resolver re-runs immediately and the machine count, raw resource, and power figures all update
- **Machine counts** shown as both exact fractional (for clocking) and ceiling integer (for building)
- **Clock % hint** — for each ceiling machine, shows what percentage to run it at to hit exact output
- **Group by** layer, machine type, or flat list
- **Power breakdown** by machine type
- **Reset / Clear Results** buttons

### 📋 Reference
A full recipe browser derived directly from the Planner's recipe database — no separate data to maintain.

- Every vanilla recipe from raw extraction through Phase 5
- Alt recipe notes and loop notes on relevant entries
- Expandable cards with full input/output rates
- Scale multiplier to preview rates at any production scale
- Filter by layer, machine type, or search by item/machine name
- ALT RECIPES ONLY filter

### 🚂 Train
Throughput calculator for your rail logistics.

- Configure freight type (solid/fluid), cars per train, and round-trip frequency
- Add item routes to get exact car counts per item at your target rate
- Stack-size-aware: uses per-item stack sizes (screws: 200, motors: 50, etc.)
- Belt and pipe speed reference table showing equivalent train throughput per mark
- Car capacity quick-reference

### ⚡ Power
Generator sizing tool.

- Enter a total MW load directly or build it from named loads
- **Import from Planner** — pulls the current planner result's power figure in one click
- Generator counts for every type at exact and +20% safety margin
- Load breakdown bar chart
- Fuel consumption reference table (coal, turbofuel, uranium/plutonium rods)

---

## Recipe coverage

All vanilla recipes from v1.0, including:

| Chain | Coverage |
|---|---|
| Raw extraction | All miners, extractors, wells |
| Basic materials | Iron/copper/steel/aluminium ingots, plates, rods, wire, cable, concrete, silica, quartz |
| Oil chain | Plastic, rubber, fuel, diluted fuel (Blender), turbofuel, recycled plastic/rubber loop |
| Aluminium chain | Alumina solution (incl. Sloppy Alumina alt), scrap, ingots, Alclad sheets, casings |
| Components | All L2–L3 components through supercomputers, HSCs, cooling systems, fused frames |
| Phase 3–4 parts | All milestone deliverables through thermal propulsion rockets and assembly director systems |
| Phase 5 | Full SAM → reanimated SAM → dark matter → QE chain, all four deliverables |

Alternate recipes are modelled with correct vanilla rates and selectable in the Planner. The reference tab flags which items have alts and how many.

---

## Alternate recipes included

Notable alts with full rate data:

- **Iron/Copper/Caterium ingots** — Pure variants (Refinery + water), alloy variants (Foundry)
- **Steel ingots** — Solid Steel, Coke Steel, Compacted Steel
- **Wire** — Fused Wire (3×), Iron Wire
- **Cable** — Coated Cable, Insulated Cable
- **Plastic / Rubber** — Recycled Plastic, Recycled Rubber (closes the HOR loop)
- **Fuel** — Diluted Fuel (Blender, correct v1.0 recipe), Liquid Biofuel
- **Alumina Solution** — Sloppy Alumina (2× throughput, recommended)
- **Circuit Boards** — all four variants (Electrode, Caterium, Silicon)
- **Computers** — Crystal Computer, Caterium Computer
- **Heavy Modular Frames** — Heavy Flexible Frame, Heavy Encased Frame
- **Radio Control Unit** — Radio Connection Unit (3× output, one of the best alts in the game)
- **Batteries** — Classic Battery (no liquids, simpler logistics)
- **Reinforced Iron Plates** — Adhered, Bolted, Stitched
- **Dark Matter Crystals** — Dark Matter Crystallization (no coal)
- **Ficsite Ingots** — Iron, Caterium, and Aluminium variants
- And more across most recipe tiers

---

## Usage

```
1. Download ficsit_companion.html
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. No internet connection required after the fonts load
```

That's it. No npm, no Python, no server.

---

## Updating recipes

All recipe data lives in a single clearly-marked block near the top of the JavaScript, starting with the comment:

```
//  SINGLE SOURCE OF TRUTH — edit here, both tabs update automatically
```

**To update a rate** — find the item in `RECIPE_DB` and change the `rate` value in its `in` or `out` array.

**To add an alternate recipe** — append a new object to the item's array. Index 0 is always vanilla; alternates follow. The Planner's alt panel will pick it up automatically.

**To add a new item** — add an entry to `RECIPE_DB` with the correct `machine`, `layer`, `in`, `out`, `mw`, and `icon` fields. If it's a raw resource with no recipe, add it to `RAWS` instead.

**To add a new raw resource** — add an entry to `RAWS` with `icon` and an optional `note`. The resolver will treat it as a chain terminator.

---

## Known limitations

- **Train tab**: requires you to measure round-trip frequency from your actual network. The tool cannot calculate travel time from track distance or topology.
- **Recycled loops**: the Plastic/Rubber recycling loop (Recycled Plastic + Recycled Rubber) creates circular dependencies. The resolver handles this by terminating at items already visited in each pass rather than looping infinitely, which means the loop byproducts (Fuel from HOR) are treated as raw inputs when the recycled recipes are selected. Plan the loop ratios manually using the Reference tab.
- **Alternate recipes**: selecting an alternate that introduces a new raw input (e.g. switching to Classic Battery to avoid liquids) will correctly update the raw resource totals. Switching to an alt that produces a useful byproduct (e.g. Alumina Solution producing Silica) does not credit that byproduct to downstream needs — the resolver is conservative and calculates everything independently.
- **Geothermal / Alien Power Augmenters**: listed in the Power tab for reference but counted as standard generators. Actual output depends on node tier and placement.
- **Nuclear waste**: the nuclear chain (uranium/plutonium fuel rods, waste processing) is in the Reference tab but not fully modelled in the Planner's resolver. The waste loop requires manual planning.
- **v1.2 experimental**: recipes marked in the reference notes. The base data reflects v1.0 vanilla. Update `RECIPE_DB` entries as patches stabilise.

---

## Tech

Single HTML file. No framework, no build step, no external scripts at runtime.

- Fonts: [Barlow](https://fonts.google.com/specimen/Barlow) + [Barlow Condensed](https://fonts.google.com/specimen/Barlow+Condensed) + [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) via Google Fonts (requires internet on first load; cached thereafter)
- All logic: vanilla ES6+ JavaScript
- All styling: CSS custom properties, no framework

Tested in Chrome 124+, Firefox 125+, Edge 124+.

---

## Contributing

If you spot a recipe error, wrong rate, or missing alternate, the data is easy to find and fix — search for the item name in the JS block. PRs welcome. Please include the source (patch notes, wiki link, or in-game verification) for any rate changes.

---

*Not affiliated with Coffee Stain Studios. Satisfactory is a trademark of Coffee Stain Studios AB.*
