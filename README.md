# pod-selkies-desktop

The `selkies-desktop` candy of the OpenCharly candy library, as a standalone
repo (the candy de-submodule cutover, kind-prefixed naming). It is the **labwc
flavor** of the browser-accessible Selkies streaming desktop — the shared
`selkies-core` spine plus the labwc nested compositor and its desktop UI.

## What it provides

`selkies-desktop` is a **metalayer**: it installs nothing of its own. Its
observable effect is that the labwc-flavor binaries and configs from every
composed candy coexist on the built image, and the labwc desktop daemons reach a
supervised RUNNING state at deploy.

It composes, by pinned `@github` ref:

| Composed candy | Role |
|---|---|
| `pod-selkies-core` | The shared spine: pixelflux WebRTC transport, Chrome/CDP, `wl-*` tooling, fonts, a11y, terminal recording, sshd |
| `pod-labwc` | The nested Wayland compositor (this flavor's defining piece) |
| `pod-waybar-labwc` | The bottom status bar |
| `pod-swaync` | The notification daemon |
| `layer-pavucontrol` | The GTK audio mixer the waybar audio module launches |

The KDE sibling is `selkies-kde-desktop`; both share `selkies-core` unchanged and
differ only in the nested compositor.

## How to use it

Typically composed by a distro box rather than used directly:

```yaml
my-desktop:
  candy:
    - '@github.com/opencharly/pod-selkies-desktop:<tag>'
```

```bash
charly box build my-desktop
charly start my-desktop
```

## Verification

The candy's `check:` plan asserts the labwc, pavucontrol, waybar, swaync,
google-chrome-stable, and pipewire binaries, the labwc-flavor waybar config, and
— at deploy scope — the `waybar` panel and `swaync` notifier services running,
plus the `swaync` and `pavucontrol` packages.

## Layout

- `charly.yml` — the `selkies-desktop:` candy entity (description, pinned
  `candy:` composition, `plan`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `CHANGELOG/` — per-CalVer history.
- `README.md` — this user overview.

## Related

- Closest family skill: `/charly-selkies:selkies-desktop-layer` — the labwc
  Selkies streaming-desktop metalayer composition. This candy has no `skill:`
  entity of its own (recorded on
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291)).
- `/charly-selkies:selkies-kde-desktop` — the KDE sibling flavor.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
