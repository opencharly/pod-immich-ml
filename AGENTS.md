# AGENTS.md — pod-immich-ml

Standalone candy repo for the `immich-ml` candy — the Immich machine-learning
backend (face recognition, smart search) on `3003`. The candy lives in
`charly.yml` at the repo root.

Canonical files:

- `charly.yml` — the `immich-ml:` candy entity (description, `require`, `env`,
  `port`, `volume`, `var`, `service`, `plan`) and its `skill:` entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-immich:immich-ml` — the owning skill: box properties, the candy stack,
  and verification. Load before editing, building, deploying, or troubleshooting
  this candy.
- `/charly-immich:immich` — the CPU-only base server this backend composes on
  (`require: pod-immich`).
- `/charly-pod:pod` — the `kind: pod` / deploy schema reference (this candy is
  composed into a box; tree-position nesting, volumes, ports).
- `/charly-check:check` — the check/R10 framework: the `check:` step verbs and
  `charly check run <bed>`.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs, `var:`, service declarations).
- `/charly-internals:git-workflow` — before any git/PR action.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The live R10 witness is a composing box's `check` bed; the candy's own `check:`
  steps assert the venv interpreter, the `immich_ml` module, the `uv` binary, the
  model-cache dir, the running `immich-ml` service, and the live `/ping` `pong` on
  `3003`.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no**
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.

## Modify this repo

- Edit the `immich-ml:` candy entity in `charly.yml`; the `skill:` entity in the
  same file is the owning skill's source — a candy change and its skill change
  land together.
- The Immich version pin is the `IMMICH_VERSION` var; keep it in step with the
  `pod-immich` sibling so the server and the ML backend build from one release.
- The venv is built with `uv pip install ".[cpu]"`; a GPU variant belongs in the
  CachyOS sibling, not here.
- The `models` volume at `~/.immich/models` is the persistent model cache; keep
  it in step with `TRANSFORMERS_CACHE`.
- The `skill:` entity is the source for `/charly-immich:immich-ml`; never edit the
  generated `SKILL.md` — regenerate it.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
