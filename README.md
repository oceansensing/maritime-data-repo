# maritime-data-repo

The United States' **maritime infrastructure**: shipping lanes, wind leases, turbines, cables, pipelines and platforms: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Publishing since 2026-11-20**, daily. `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

Seven products, each a root of every record (`<product>.json`: a polygon's or a line's shape as GeoJSON, a point's latitude and longitude, and what its source says of it) and the same records as a pyramid of Mapbox vector tiles beside it (uncompressed, extent 4096, Web Mercator, the XYZ scheme; `land/<product>/index.json` naming the version, the tiles' own hash, and every tile to zoom 8), R2's alone: **`shipping-lanes`**, zooms 3 to 10, the traffic lanes, separation zones, precautionary areas, safety fairways, recommended routes, areas to be avoided, particularly sensitive sea areas and right-whale seasonal management areas on NOAA's charts, each with its kind, the chart's theme, its name and the rule's text; **`wind-leases`**, zooms 3 to 12, the Bureau of Ocean Energy Management's offshore wind lease outlines, their lessees, projects, dates and acres; **`wind-planning-areas`**, zooms 3 to 10, BOEM's wind planning areas as history, their lease blocks joined into the areas they make, each said to be rescinded on July 30, 2025; **`wind-turbines`**, zooms 8 to 12, MarineCadastre's offshore wind turbines and substations, their farms and status; **`submarine-cables`**, MarineCadastre's submarine cable corridors, their systems, owners and status — the corridors themselves at zooms 10 and 11, their outlines as lines from 4 to 9; **`pipelines`**, zooms 5 to 12, the Bureau of Safety and Environmental Enforcement's oil and gas pipeline segments in the Gulf of America, every status kept with its code, one line a class of status, product and size to zoom 8; and **`platforms`**, zooms 6 to 12, BSEE's standing platform structures in the Gulf of America, each with its complex, area and block and, where BOEM's structures file names it, its name and type. A set's version is its tiles' own hash, so an unchanged rebuild publishes nothing new.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

Every source is a U.S. Government work in the public domain, read from its agency's own service: **NOAA's Office of Coast Survey**, *NavigationChartData / MarineTransportation*, *Shipping Lanes and Regulations* (`encdirect.noaa.gov`), from the NOAA Electronic Navigational Charts, updated weekly — the ENC User Agreement: *"You may download, use, and redistribute them without restriction"*; its service: *"Coast Survey ... shall incur no responsibility or liability as to the completeness or accuracy of this information"*. **The Bureau of Ocean Energy Management**, *Offshore Wind Lease Outlines* and *Offshore Wind Planning Areas (Rescinded July 30, 2025)* (`services7.arcgis.com`), and its *Platform Structures* file (`www.data.boem.gov`). **NOAA's Office for Coastal Management**, MarineCadastre.gov's *Offshore Wind Turbines* and *Submarine Cables* (`coast.noaa.gov`), under its notice: *"As required by 17 U.S.C. 403, third parties producing copyrighted works consisting predominantly of the material produced by U.S. government agencies must provide notice with such work(s) identifying the U.S. Government material incorporated and stating that such material is not subject to copyright protection."* **The Bureau of Safety and Environmental Enforcement**, *OCS Oil & Gas Pipelines* and *OCS Drilling Platforms* in BOEM's Gulf of America map service (`gis.boem.gov`, NAD83). None of it is the regulation it maps, and none of it is for navigation: a regulated area's rule is its text in the Code of Federal Regulations, and the charts and the Notices to Mariners are what a mariner navigates by. Terms read 2026-11-20.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `facilities-data-repo` and `aviation-data-repo` (points made the same way), `public-lands-data-repo` (polygons and lines on the same machinery).

**Which document gets what, and what "update docs" means across all
thirty-six repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all thirty-six, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
