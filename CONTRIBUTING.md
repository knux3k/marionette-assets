# Adding assets

Assets enter the pool only through the engine's operations, which run every admission rule and
write the record. Never add, edit or rename files under `assets/` by hand: `pool_verify` (run by
CI) refuses files that do not match their records.

1. Clone this repository and build the engine CLI from
   [knux3k/marionette](https://github.com/knux3k/marionette).
2. Add the asset:
   - Made for the project (drawn, modelled, recorded or computed by you, with no AI provider):
     `marionette op pool_add '{"pool": "<checkout>", "path": "<file or folder>", "kind": "texture",
     "name": "...", "origin": "made", "method": "how it was made"}'`
   - From an online CC0 library: Poly Haven and ambientCG by id,
     `marionette op pool_ingest '{"pool": "<checkout>", "library": "polyhaven", "source_id": "..."}'`;
     Kenney and Quaternius by an archive URL on their site, or `pool_add` with `"origin":
     "online"`, `library` and `page` for an archive you downloaded.
   Use `"dry_run": true` first to see what would be added.
3. `marionette op pool_index '{"pool": "<checkout>"}'`, then
   `marionette op pool_verify '{"pool": "<checkout>"}'`.
4. Commit the new `assets/<id>/` folder and `index.json` together and open a pull request.

## What is refused

- Anything matching an asset in an owned library, or carrying a license declaration
  (`*.license.json`).
- License files that name any license other than CC0 or public domain (CC BY, NonCommercial,
  ShareAlike, GPL, "all rights reserved", store terms).
- Generated assets (`*.provenance.json`, or copies of generated files), unless the person who
  generated them writes a `<name>.cc0.json` dedication themselves. Tools and agents never write
  dedications or declarations.
- Online assets from a library that is not known to publish under CC0, or downloaded from
  outside that library's domains.

Never put names, personal paths or machine details in records or commit messages.
