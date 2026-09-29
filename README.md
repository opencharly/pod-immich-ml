# pod-immich-ml

The `immich-ml` candy of the OpenCharly candy library, as a standalone repo
(kind-prefixed naming). It ships the Immich machine-learning backend for face
recognition and smart-search inference.

## What it provides

Installs the `uv` Python package manager, builds a dedicated virtualenv at
`/opt/immich/machine-learning/.venv`, and installs the `immich_ml` module from
the pinned Immich source release. A supervised `immich-ml` service runs
`python -m immich_ml`, exposing the ML inference API on port `3003` (its `/ping`
endpoint answers `pong`) so the Immich server can offload face detection and CLIP
smart-search embedding to this backend.

| Property | Value |
|---|---|
| Service | `immich-ml` (priority 40, `restart: always`) |
| Port | `3003` (ML inference API, `/ping`) |
| Requires | `pod-immich` |
| Volume | `models` at `~/.immich/models` |
| Env | `IMMICH_MACHINE_LEARNING_ENABLED=true`, `IMMICH_MACHINE_LEARNING_URL=http://127.0.0.1:3003`, `MACHINE_LEARNING_*`, `TRANSFORMERS_CACHE=~/.immich/models` |
| Var | `IMMICH_VERSION` (default `v2.7.5`) |

This candy composes on `pod-immich`; the ML venv is CPU-only (`uv pip install
".[cpu]"`). A CachyOS GPU sibling (`cachyos.immich-ml`) lives in the
`distro-cachyos` submodule on the `cachyos.nvidia` base.

## How to use it

```bash
charly box build immich-ml
charly config setup immich-ml
charly start immich-ml
# Immich UI on http://localhost:2283, ML backend on :3003
```

## Layout

- `charly.yml` — the `immich-ml:` candy entity plus its `skill:` entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-immich:immich-ml` — the box properties, the candy stack,
  and verification.
- `/charly-immich:immich` — the CPU-only base server this backend composes on.
- `/charly-languages:python-ml` / `/charly-distros:cuda` — the ML runtime stack in
  the GPU variant.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
