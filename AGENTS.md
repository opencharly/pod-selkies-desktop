# AGENTS.md — pod-selkies-desktop

Standalone candy repo for the `selkies-desktop` candy — the labwc flavor of the
browser-accessible Selkies streaming desktop: the shared `selkies-core` spine
plus the labwc compositor and its desktop UI. It is a metalayer (composes pinned
`@github` candies, installs nothing of its own). The candy lives in `charly.yml`
at the repo root.

Canonical files:

- `charly.yml` — the `selkies-desktop:` candy entity (description, pinned
  `candy:` composition, `plan`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:selkies-desktop-layer` — the closest family skill: the labwc
  Selkies streaming-desktop metalayer composition, the labwc desktop, and the
  browser-accessible remote desktop. **This candy has no `skill:` entity of its
  own** — the gap is recorded on
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).
- `/charly-selkies:selkies-core` — the shared spine this metalayer composes.
- `/charly-selkies:selkies-kde-desktop` — the KDE sibling flavor.
- `/charly-check:check` — the check/R10 framework: the `check:` step verbs and
  `charly check run <bed>`.
- `/charly-pod:pod` — the `kind: pod` / deploy schema reference (this candy is
  composed into a box; tree-position nesting, volumes, ports).
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs, service declarations).
- `/charly-internals:git-workflow` — before any git/PR action.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The live R10 witness is a composing box's `check` bed; the candy's own `check:`
  steps assert the labwc, pavucontrol, waybar, swaync, google-chrome-stable, and
  pipewire binaries, the labwc-flavor waybar config, and — at deploy scope — the
  `waybar` and `swaync` services running.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no**
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.

## Modify this repo

- Edit the `selkies-desktop:` candy entity in `charly.yml`; there is no `skill:`
  entity in this repo (the gap is tracked on opencharly/opencharly#291).
- The `candy:` list is **pinned `@github` refs, not bare names** — these candies
  are standalone repos, so a bare name resolves only inside a project that has
  them in scan range. Keep the pins at merged tags.
- This metalayer installs nothing of its own: its `plan:` asserts the composed
  candies' artifacts coexist on the built image. A composition change is a
  `candy:` pin change, not a new install step.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
