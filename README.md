# FICSIT Companion

A single-file production suite for **Satisfactory v1.0**, with v1.2 experimental changes tracked. No install, no server, no dependencies — open `index.html` in any browser and start planning.

![Satisfactory](https://img.shields.io/badge/Satisfactory-v1.0%20%2B%201.2%20EXP-f5a623?style=flat-square) ![Recipes](https://img.shields.io/badge/recipes-vanilla%20base-00d4ff?style=flat-square) ![Format](https://img.shields.io/badge/format-single%20HTML-39d98a?style=flat-square)

**Live:** [Here](https://fromchaosimportcalm.github.io/ficsit-companion/)

---

## What's in it

Four tabs, one persistent left panel, one shared recipe database. Every tab reads from the same data — change a recipe once, all tabs update automatically.

### ⚙ Planner

Back-calculates the full production chain from any target output rate. The resolver walks the entire dependency tree back to raw ore extraction, accounting for every intermediate step.

- **Milestone presets** for Phase 1–5 with sensible default rates
- **Custom targets** — any item, any rate, addable individually or stacked on top of a preset
- **Selectable alt recipes** — switch any recipe in your chain to an alternate; machine counts, raw resources, and power figures all update immediately
- **Machine counts** shown as both exact fractional (for overclocking) and ceiling integer (for building)
- **Clock % hint** — for each ceiling machine, shows what percentage to run it at to hit exact output
- **Group by** production layer, machine type, or flat list
- **Raw resource totals** with world node supply data — shows percentage of the world's total supply your chain consumes, and approximate Mk.3 miner count needed
- **Belt / pipe mark hints** — flags any flow rate in the chain that exceeds a conveyor or pipe tier
- **Power breakdown** by machine type
- **Game Mode multipliers** (v1.2) — Recipe Cost and Power Consumption multipliers with amber highlighting on affected values
- **Share plan** — encodes your full configuration (targets, alt selections, game mode settings) into the URL; paste the link to share or reload your exact plan
- **Reset / Clear Results** buttons

### 📋 Reference

A full recipe browser derived directly from the Planner's recipe database — no separate data to maintain, always in sync.

- Every vanilla recipe from raw extraction through Phase 5, including all oil, steel, and aluminium chains
- Alt recipe counts and notes on relevant entries, loop notes on recycling chains
- Expandable cards with full scaled input/output rates
- Scale multiplier to preview rates at any production multiple
- Filter by production layer, machine type, or free-text search
- ALT RECIPES ONLY filter

### 🚛 Logistics

Throughput calculator for all three vehicle types. Select your vehicle on the left and the controls and results adapt accordingly.

**Train**
- Configure cargo type (solid/fluid), cars per train, and round-trip frequency
- Add item routes to get exact train counts per item at your target rate
- Stack-size-aware: uses per-item stack sizes (screws: 200, motors: 50, etc.)
- Belt and pipe speed reference showing equivalent train throughput per conveyor/pipe mark

**Truck** *(fluid trucks new in v1.2)*
- Solid truck: 32 stacks capacity (same as freight car, single unit)
- Fluid truck: 2,000 m³ capacity (v1.2) — requires road network
- Configure cargo type and round-trip frequency; item route results the same as trains

**Drone**
- Configure route distance in km and number of drones on the route
- Round-trip time calculated automatically at 120 km/h
- 4 inventory slot capacity per drone, stack-size-aware
- Fluid items filtered out (drones carry solid cargo only)
- Battery consumption estimate per trip per drone

### ⚡ Power

Generator sizing tool.

- Enter a total MW load directly, or build it from named loads
- **Import from Planner** — pulls the current planner result's power figure in one click, no transcription needed
- Generators split into **practical** (recommended at your load scale) and **reference only** (impractical at scale, shown dimmed)
- Total output capacity and surplus shown per generator type, not just count
- Load breakdown bar chart when multiple named loads are active
- Fuel consumption reference with per-load totals for your specific MW target (coal, turbofuel, uranium/plutonium rods)

---

## v1.2 Game Mode support

The Planner left panel includes a **Game Mode** section with the two multipliers that meaningfully affect production chain planning:

| Multiplier | Effect in tool | Options |
|---|---|---|
| Recipe Cost | Scales raw resource consumption in results | ×0.25 / ×0.5 / ×0.75 / ×1 / ×1.25 / ×1.5 / ×1.75 / ×2 |
| Power Consumption | Scales all machine MW figures | ×0.25 / ×0.5 / ×0.75 / ×1 / ×2 / ×5 |

The Recipe Cost multiplier is applied at the display layer, not inside the resolver. Machine counts and output rates are determined by vanilla recipe ratios and don't change with recipe cost — what changes is how much raw material each machine consumes. At ×1.75, the raw resource section shows the vanilla rate struck through with the multiplied rate in amber. World node supply percentages and miner counts are always calculated against vanilla demand, so the comparison stays meaningful regardless of what multiplier is active.

Non-default values are highlighted in amber throughout the results. A header badge shows which multipliers are active at a glance.

**Space Elevator Deliverable Cost multiplier is intentionally omitted.** That multiplier scales the total quantity you need to deliver to complete a phase — it doesn't affect production rates. Since this tool works in items-per-minute rather than total delivery quantities, the multiplier has no meaningful effect on the chain calculations. Adjust your custom target rates manually if you want to account for it.

**Randomised nodes (v1.2):** the world node supply figures in the Planner's raw resource section reflect vanilla v1.0 node counts. If you're playing with randomised nodes enabled, these figures won't apply to your save — treat them as reference only.

---

## World node data

The raw resource section shows how much of the world's total supply your production chain requires, based on vanilla v1.0 node counts from the [Satisfactory Calculator interactive map](https://satisfactory-calculator.com/en/interactive-map).

| Resource | Impure | Normal | Pure | Max extraction (Mk.3 / 100%) |
|---|---|---|---|---|
| Iron Ore | 39 | 42 | 46 | 9,330/min |
| Copper Ore | 13 | 29 | 13 | 3,330/min |
| Limestone | 15 | 50 | 29 | 6,030/min |
| Coal | 15 | 31 | 16 | 4,770/min |
| Crude Oil | 10 | 12 | 8 | 1,680 m³/min |
| Bauxite | 5 | 6 | 6 | 1,470/min |
| Raw Quartz | 3 | 7 | 7 | 1,470/min |
| Caterium Ore | 0 | 9 | 8 | 1,500/min |
| Sulfur | 6 | 5 | 5 | 1,230/min |
| Uranium | 3 | 2 | 0 | 210/min |
| SAM | 10 | 6 | 3 | 1,230/min |
| Nitrogen Gas | — | — | 36 wells | ~5,400/min (est.) |

These figures are for vanilla node placement. Randomised nodes mode (v1.2) will produce different distributions.

---

## Recipe coverage

| Chain | Coverage |
|---|---|
| Raw extraction | All miners, extractors, resource wells |
| Basic materials | Iron/copper/steel/aluminium ingots, plates, rods, wire, cable, concrete, silica, quartz |
| Oil chain | Plastic, rubber, fuel, diluted fuel (Blender), turbofuel, recycled plastic/rubber loop, HOR sinks |
| Aluminium chain | Alumina solution (incl. Sloppy Alumina), scrap, ingots, Alclad sheets, casings |
| Components | All L2–L3 components through supercomputers, high-speed connectors, cooling systems, fused frames |
| Phase 3–4 parts | All milestone deliverables through thermal propulsion rockets and assembly director systems |
| Phase 5 | Full SAM → reanimated SAM → dark matter → quantum encoder chain, all four deliverables |

---

## Alternate recipes included

Notable alts with full correct rates, all selectable in the Planner:

- **Ingots** — Pure variants (Refinery + water) for iron, copper, caterium; alloy variants (Foundry) for iron and copper; solid/coke/compacted variants for steel
- **Wire** — Fused Wire (3×), Iron Wire
- **Cable** — Coated Cable, Insulated Cable
- **Plastic / Rubber** — Recycled Plastic, Recycled Rubber (closes the HOR loop)
- **Fuel** — Diluted Fuel (Blender, 2.5× output from HOR), Liquid Biofuel
- **Alumina Solution** — Sloppy Alumina (2× throughput, no silica byproduct)
- **Aluminum Scrap** — Electrode Aluminum Scrap (uses petroleum coke instead of coal)
- **Circuit Boards** — Electrode, Caterium, Silicon variants
- **Computers** — Crystal Computer, Caterium Computer
- **Heavy Modular Frames** — Heavy Flexible Frame, Heavy Encased Frame
- **Radio Control Unit** — Radio Connection Unit (3× output — one of the best alts in the game)
- **Batteries** — Classic Battery (no liquids, simpler logistics)
- **Reinforced Iron Plates** — Adhered, Bolted, Stitched variants
- **Dark Matter Crystals** — Dark Matter Crystallization (no coal required)
- **Ficsite Ingots** — Iron, Caterium, and Aluminium metal variants
- And more across most recipe tiers

---

## Sharing plans

The **⎘ SHARE PLAN** button in the Planner encodes your current configuration — targets, alt recipe selections, and game mode multipliers — into the page URL. Copy and share the URL and anyone who opens it gets your exact plan loaded and auto-calculated.

State is also saved to the URL on every CALCULATE, so browser back/forward navigates through your planning history.

---

## Usage

```
1. Visit https://fromchaosimportcalm.github.io/ficsit_companion
   — or —
   Download index.html and open it in any modern browser
2. No install, no server, no internet required after first load
```

---

## Updating recipes

All recipe data lives in a single clearly-marked block near the top of the JavaScript:

```js
//  SINGLE SOURCE OF TRUTH — edit here, all tabs update automatically
```

**Update a rate** — find the item in `RECIPE_DB`, change the `rate` value in its `in` or `out` array.

**Add an alternate recipe** — append a new object to the item's array. Index 0 is always vanilla; alternates follow in any order. The Planner's alt panel picks it up automatically.

**Add a new item** — add an entry to `RECIPE_DB` with `machine`, `layer`, `in`, `out`, `mw`, and `icon` fields.

**Add a raw resource** — add an entry to `RAWS` with `icon` and an optional `note`. The resolver treats it as a chain terminator with no upstream dependencies.

**Add world node data** — add an entry to `WORLD_NODES` with `i` (impure), `n` (normal), `p` (pure) node counts. The raw resource section will automatically show supply percentages.

---

## Known limitations

- **Logistics tab — round trip frequency**: the tool cannot calculate travel time from track distance or road topology. Measure your actual round trip in-game and enter it manually. For drones, the tool estimates from distance at 120 km/h which is approximate.

- **Game Mode — Recipe Cost**: machine counts, clock percentages, and output rates are shown at vanilla values regardless of the recipe cost multiplier, because those figures are determined by output rate not input cost. Only the raw resource section reflects the multiplied consumption. This is intentional — the resolver is pure vanilla maths and the multiplier is applied at display time only.

- **Recycled loops**: the Plastic/Rubber recycling loop (Recycled Plastic + Recycled Rubber alt recipes) creates a circular dependency. The resolver breaks the cycle using visited sets, which means Fuel is treated as a raw input rather than a produced item when those alts are active. Plan the loop ratios manually using the Reference tab. This is a known architectural limitation documented intentionally rather than papered over.

- **Byproduct credits**: the resolver is conservative — it does not net off useful byproducts (e.g. Silica from standard Alumina Solution) against downstream demand. Raw resource totals may be overstated when byproduct-producing vanilla recipes are in use. Switching to a byproduct-free alt (e.g. Sloppy Alumina) is the clean solution.

- **Nuclear chain**: uranium/plutonium fuel rods and waste processing are in the Reference tab but the waste management loop (Uranium Waste → Non-Fissile Uranium → Plutonium) is not fully modelled in the Planner resolver. Plan the waste loop manually.

- **Geothermal / Alien Power Augmenters**: shown in the Power tab with standard generator counts. Actual geothermal output varies by geyser tier; augmenters require an active Phase 5 SAM chain. Treat these as reference figures.

- **Randomised nodes (v1.2)**: world node supply figures reflect vanilla placement. With randomised nodes enabled, actual supply distribution in your save will differ.

- **Space Elevator multiplier (v1.2)**: intentionally not modelled. See the v1.2 Game Mode section above for the reasoning.

---

## Tech

Single HTML file — no framework, no build step, no runtime dependencies beyond Google Fonts.

- **Fonts**: Barlow + Barlow Condensed + Share Tech Mono via Google Fonts (internet required on first load; cached thereafter)
- **Logic**: vanilla ES6+ JavaScript
- **Styling**: CSS custom properties, no framework
- **State persistence**: URL hash encoding (base64 JSON) — no backend, no cookies

Tested in Chrome 124+, Firefox 125+, Edge 124+.

---

## Contributing

Recipe errors, wrong rates, or missing alternates are easy to fix — search for the item name in the `RECIPE_DB` block. PRs welcome. Please include a source (patch notes, wiki link, or in-game screenshot) for any rate changes so the data stays verifiable.

---

*Not affiliated with Coffee Stain Studios. Satisfactory is a trademark of Coffee Stain Studios AB.*
