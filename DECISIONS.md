# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-10-20 — Its own repository, R2 alone, the tiles carried by the cache

HydroLAKES and HydroSHEDS v2's rivers get a repository of their own (2026-10-20) and **publish to Cloudflare R2 alone**, as every new product since the site pipeline's D13: Pages carries its status alone. Their tiles — hundreds of thousands of files — are never committed: each product's tree is carried from run to run by this repository's cache and rebuilt only when its source changes.
