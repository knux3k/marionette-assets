# Marionette CC0 asset pool

Public pool of CC0 (public domain) assets for the [Marionette](https://github.com/knux3k/marionette)
game engine: textures, models, materials and sounds that anyone may use for anything, with no
credit required.

Every asset folder in `assets/` holds its files and an `asset.json` that records where the asset
came from and the proof that it is CC0: made for the project (and how), or taken from a CC0
library (Poly Haven, ambientCG, Kenney, Quaternius) with its page, download URLs and checks.
`index.json` lists every asset. Nothing owned, bought, licensed under other terms, or generated
by an AI provider is accepted (rules: engine `docs/ai/ASSETS-AND-LICENSES.md`, decision 0041).

## Use it from the engine

Clone this repository, then point the engine at it in one of three ways:

- per operation: `"pool": "<path to this checkout>"`
- environment: `MARIONETTE_POOL=<path>`
- user config file: `"cc0_pool": "<path>"`

Then `asset_search` looks here after the project's files and your owned library, and
`pool_fetch` copies an asset into a project:

```sh
marionette op asset_search '{"query": "bricks"}'
marionette op pool_fetch '{"id": "red-bricks"}'
```

## Layout

- `pool.json`: marks the folder as a pool (`marionette.cc0_pool/1`).
- `assets/<id>/asset.json`: kind, name, tags, files with SHA-256, main file, source, license
  (`CC0-1.0`) and proof (`marionette.pool_asset/1`).
- `index.json`: one entry per asset, written by `pool_index`.

CI runs the engine's `pool_verify` on every push and pull request. Adding assets:
[CONTRIBUTING.md](CONTRIBUTING.md).

## License

Everything here is dedicated to the public domain under CC0 1.0 Universal ([LICENSE](LICENSE)).
Assets from online libraries were published under CC0 by their libraries; their creators are
recorded in each `asset.json` as a courtesy.
