# pod-immich-ml — retired

> **RETIRED — this repo ships no Immich ML backend.** The `immich-ml` candy, its two
> `skill:` entities and its skill files are deleted.
>
> **Superseded by `opencharly/pod-immich`'s `immich` candy — the ML backend is now part
> of the `immich` image** ([opencharly/pod-immich#12](https://github.com/opencharly/pod-immich/issues/12)).

Immich v3.4.1 carries its machine-learning backend in the `immich` image itself: one
image, on the CachyOS GPU base, supervises the ML backend on port `3003` beside the Node
server on `2283`, with PostgreSQL + VectorChord + Redis and a `models` volume under
`~/.immich`, and reaches it over `http://127.0.0.1:3003`. One image and one candy mean a
separate ML image has nothing left to install, so this repo has nothing left to ship.

## What remains here

| Property | Value |
|---|---|
| Layer / candy | `pod-immich-ml` (documentation-only carrier) |
| Install content | none — a `true` no-op `plan:` |
| Service / port | none |
| Owns | nothing — 0 `skill:` entities |

Do not compose or reference this repo: use `opencharly/pod-immich` instead. What is left
is the carrier candy that records the retirement, so the repo still validates as a
project. **Archiving the GitHub repository is an operator action** — this repo does not
archive itself; the class-wide retirement policy is tracked in
[opencharly/opencharly#600](https://github.com/opencharly/opencharly/issues/600).

## Layout

- `charly.yml` — the retirement-recording documentation-only candy.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.
- `README.md` — this notice.
