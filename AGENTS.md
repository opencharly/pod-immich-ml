# AGENTS.md — pod-immich-ml (retired)

This repo is **retired**: it ships no Immich machine-learning backend and no
skill. It was the `immich-ml` candy — the ML inference backend on port `3003`
that `pod-immich`'s server offloaded face detection and CLIP search to. Immich
v3.4.1 carries that backend in-process in the ONE `immich` image
(`opencharly/pod-immich`), so the candy, its two `skill:` entities and both
`.agents/skills/` files were deleted in the same cutover
([opencharly/pod-immich#12](https://github.com/opencharly/pod-immich/issues/12)).

Nothing is authored here now. Do not add a candy, a service, a `skill:` node or
prose: a change to Immich's ML behaviour is a change to the `immich` candy in
`opencharly/pod-immich`, in the same pull request as the entity it documents.
Archiving this GitHub repository is an operator action, tracked with the
class-wide retirement policy in
[opencharly/opencharly#600](https://github.com/opencharly/opencharly/issues/600).

Canonical files:

- `charly.yml` — the documentation-only carrier candy: a `true` no-op `run:`
  plus a `true` no-op `check:`. It exists only so this repo still validates as a
  project.
- `README.md` — user overview only; never agent guidance.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly. It is the only check this repo
  has; there is no live bed, no service and no image here.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.

## Modify this repo

- Don't. There is no candy, service, port, volume or skill node left to update.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
