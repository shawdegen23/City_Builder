# Golden State Builder

A 3D city-building game about the specific, peculiar difficulty of building a city **in California**.

It runs entirely in the browser — no build step, no server, no account. Each version is a single
self-contained HTML file that loads Three.js from a CDN and does everything else itself.

**Play:** open `index.html`, or visit the deployed site.

---

## The idea

Most city builders model zoning, traffic and budgets. This one also models the *legal* layer that
actually determines what gets built in California, because that's the part that makes California
hard. You don't just paint zones — you run a road out to raw land, subdivide it under the
Subdivision Map Act, survive environmental review and a neighbor appeal, and only then do houses
appear on lots.

Statutes in the simulation:

| Law | What it does in game |
| --- | --- |
| **Prop 13** (1978) | Property tax capped at 1% of assessed value, 2%/yr growth until redevelopment |
| No-and-low property tax cities | Incorporating after 1978 gets you ~14 cents on the property-tax dollar — so you chase retail |
| **Bradley-Burns** | The 1% local sales tax, unlocked only by incorporating |
| **Prop 218** | New taxes require a vote — Measure T goes on the ballot |
| **Subdivision Map Act** (Gov. 66410) | 5+ lots need a Tentative Tract Map and a hearing; 4 or fewer get a Parcel Map |
| **CEQA** (1970) | Categorical Exemption to Mitigated Negative Declaration to full EIR, by size and sensitivity |
| **Quimby Act** (Gov. 66477) | Park fees per dwelling unit, collected at map recordation |
| **RHNA** | State housing targets — miss them and the Builder's Remedy overrides your zoning |
| **SB 9 / ADU law** | Lot splits and accessory units raise capacity |
| **SB 35** | Ministerial approval for multifamily infill — skips CEQA entirely |
| **SB 100** (2018) | 100% carbon-free retail electricity by 2045, with penalties for falling behind |
| **SGMA** (2014) | Groundwater basins have a sustainable yield; pumping past it is capped and wasted |
| **AB 2097** (2022) | No parking minimums near major transit — that land becomes housing instead |
| **SB 743** (2013) | Near transit, CEQA measures vehicle miles travelled instead of traffic delay |
| **Coastal Act** | The Coastal Commission adds review inside the coastal zone |

Plus the things that do not care about statutes: wildfire seasons, earthquakes, atmospheric-river
floods, multi-year droughts and heat waves.

## Four regions

| Map | County | Character |
| --- | --- | --- |
| Dry Creek Valley | El Dorado | Oak foothills, a year-round river, geothermal, hard fire seasons |
| Tule Flats | San Joaquin | Flat farmland on a canal — cheap land, winter floods, deep droughts |
| Punta Gaviota | San Luis Obispo | Marine terraces, Coastal Commission review, 2.3x quake risk, desalination |
| Yucca Wash | San Bernardino | High Mojave — the best sun and wind in the country, almost no water |

## Version history

| File | Volume | Adds |
| --- | --- | --- |
| `v5.html` | 5 — Public Transit | Bus routes, light rail, commuter + high-speed rail, AB 2097 and SB 743 TOD mechanics |
| `v4.html` | 4 — Housing, Power & Water | R-1/R-2/R-3/Mixed-Use zoning, six energy sources, five water sources, day/night toggle |
| `v3.html` | 3 — Subdivision | The Subdivision Map Act end to end, auto-generated tract streets and platted lots |
| `v2.html` | 2 — Four Californias | Region select, save/load, elections, land value and traffic overlays, bridges |
| `v1.html` | 1 — Dry Creek Valley | The original: Prop 13, CEQA, RHNA, wildfires, earthquakes, drought |

`index.html` is `v5.html` plus a link to the archive, so the site root plays the latest build.
`versions.html` lists them all.

## Controls

- **Drag** to pan, **right-drag** to rotate, **scroll** to zoom, **WASD** to pan, **Esc** to deselect
- Hover anything with the Select tool to inspect it
- Save your city to a file and load it back — saves are version-specific
- Toggle the day/night cycle, or enter photo mode

## Getting started in game

1. Lay a **road** out toward land you want
2. **Subdivide** — drag a rectangle that touches that road, pick a zoning designation, file the Tentative Map
3. Add **water** and **power** before the map records, or nothing will build
4. When the Final Map records, streets and lots appear and buildings go up
5. At 350 residents you can incorporate — unlocking sales tax, and handing you the full cost of running a city

## Deploying

Static site, no build. Any host works. On Vercel: no build command, no output directory.
`vercel.json` enables clean URLs so `/versions` works as well as `/versions.html`.

## Tech

Three.js r128 via CDN. Everything else — terrain generation, simulation, UI — is plain JavaScript
in one file per version. Terrain is value-noise fBm; buildings, vehicles and infrastructure are
procedural geometry.
