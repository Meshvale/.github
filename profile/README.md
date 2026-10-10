# Meshvale

Tools and libraries for working with 3D polygon meshes.

Meshvale is an Apache-2.0 toolkit in early development. Geometry, Interchange and Repair have working C++20 and optional Python interfaces. The first implemented file workflow repairs explicitly selected duplicate faces in OBJ/MTL assets, rechecks the result and publishes a verified new bundle with a machine-readable report. Stable releases and package-index distributions are forthcoming.

## Try the development workflow

Start with [Repair's OBJ commands](https://github.com/Meshvale/meshvale-repair/blob/main/docs/cli.md) and [installed command example](https://github.com/Meshvale/meshvale-repair/blob/main/examples/python/obj_commands.py). Build the exact public development dependencies described by the product; there is no package-index installation yet. The same operation is available through a reusable Python API, a single-asset command and an ordered batch command.

The operation preserves supported polygon loops and face-corner attributes while removing only the duplicates you select. OBJ resources are carried as opaque bytes and verified during publication. Reports identify what was checked, changed or left unresolved; this is a targeted repair, with [documented preservation and format limits](https://github.com/Meshvale/meshvale-repair/blob/main/docs/obj-workflow.md).

## Products

| Repository | Purpose |
|---|---|
| [meshvale-geometry](https://github.com/Meshvale/meshvale-geometry) | Development polygon/attribute storage, topology inspection, native editing and owned Python snapshots |
| [meshvale-interchange](https://github.com/Meshvale/meshvale-interchange) | Development OBJ/MTL read/write, resource snapshots and verified bundle publication |
| [meshvale-repair](https://github.com/Meshvale/meshvale-repair) | Development targeted duplicate removal, independent verification, Python API and OBJ single/batch commands |
| [meshvale-simplify](https://github.com/Meshvale/meshvale-simplify) | Planned mesh reduction with stated preservation criteria |
| [meshvale-validate](https://github.com/Meshvale/meshvale-validate) | Planned standalone asset checks, coverage and validation policies |

The implemented storage, OBJ adapter and duplicate operation support triangles, quads, n-gons and mixed polygon meshes within their product contracts. glTF/GLB, additional repairs and a supported release platform matrix remain in development.

## Get involved

Start with the relevant product README and its issues. See the [contribution guide](https://github.com/Meshvale/.github/blob/main/CONTRIBUTING.md) for the current checks and how to propose a change.

Public repositories use [Apache-2.0](https://github.com/Meshvale/.github/blob/main/LICENSE). Each repository includes its own license and attribution notices.
