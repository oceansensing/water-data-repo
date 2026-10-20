# water-data-repo

The world's **lakes** and the Americas' **rivers**, as vector tiles: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Publishing since 2026-10-20**, daily at 08:29 UTC. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

Two products, each a pyramid of Mapbox vector tiles (uncompressed, extent 4096, Web Mercator, the XYZ scheme) with an index naming every tile to zoom 8 and a root naming its version, R2's alone: **`lakes`** (`lakes.json`, `map/land/lakes/`), zooms 2 to 10, one polygon layer `lakes` — HydroLAKES v1.0's 1,427,688 lakes and reservoirs of 10 ha and more, each with its id, name (where it has one), type (lake, reservoir, controlled lake), area, mean depth, volume, surface elevation and country, the low zooms thinned to the largest lakes (1,000 km² and more at zooms 2-3, 100 at 4-5, 10 at 6-7, every lake from 8); and **`rivers`** (`rivers.json`, `map/land/rivers/`), zooms 2 to 11, one line layer `rivers` — HydroSHEDS v2's streams of North and South America, every stream draining 1 km² and more, each with its reach's id, Strahler order and upstream area, the low zooms thinned by upstream area (100,000 km² and more at zooms 2-3, 10,000 at 4-5, 1,000 at 6-7, 100 at 8-9, 10 at 10, every stream at 11) and drawn there as rivers between their own confluences. A set's version is its tiles' own hash, so an unchanged rebuild publishes nothing new.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

**HydroLAKES v1.0** (2016; the polygons' file geodatabase, `HydroLAKES_polys_v10.gdb.zip`, from data.hydrosheds.org) and **HydroSHEDS v2**'s river network (RIV, 1 arc-second, released for North and South America 2026-07-07; `<continent>_RIV_1s_v2r0.gdb.zip`), HydroLAKES by Mathis Messager, Bernhard Lehner and colleagues (McGill University), HydroSHEDS v2 by Bernhard Lehner and colleagues (its technical documentation prepared on behalf of Confluvio Inc.; its elevation DLR's TanDEM-X). Both are **CC BY 4.0**; notwithstanding the free license, the authors ask that the data not be redistributed in whole in its original format on other websites without their written permission — these tiles are neither the whole data set nor its format, and the original files are never published here. HydroSHEDS v2 carries no discharge. Citations: Messager, M.L., Lehner, B., Grill, G., Nedeva, I., Schmitt, O. (2016): Estimating the volume and age of water stored in global lakes using a geo-statistical approach. Nature Communications 7: 13603, https://doi.org/10.1038/ncomms13603; Lehner, B., Roth, A., Huber, M., Anand, M., Thieme, M. (2022): A sharper look at the world's rivers and catchments. Eos 103, https://doi.org/10.1029/2022EO220167; https://www.hydrosheds.org. The data are provided as is, without warranty. Terms read 2026-10-20.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: none it depends on.

**Which document gets what, and what "update docs" means across all
thirty-two repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all thirty-two, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
