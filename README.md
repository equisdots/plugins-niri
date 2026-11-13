# equisdots · plugins-niri

Niri-specific plugins for the equisdots desktop. These plugins implement the
same user-facing features as the shared `equisdots/plugins` implementations,
but use the niri session scripts and protocols. They are consumed by
`equisdots/niri-meta`, which deploys the `plugins-niri` version of a plugin
instead of the shared one when both exist.

## plugins/screenshots

The niri screenshots + recording plugin. It keeps the standard plugin contract
(`plugin.json`, `ui/`, `bar/`, the Plugins panel, enable/disable) but routes all
capture and recording to:

- `~/.config/niri/scripts/niri_screenshot.sh` for area/full screenshots,
  the selection overlay, QR scanning and the recording choices;
- `~/.config/niri/scripts/niri_record.sh` (gpu-screen-recorder) for recording.

The shared Hyprland plugin (`equisdots/plugins`) is not used on niri. The niri
keybinds in `equisdots/niri` call the same scripts directly.

## Deployment

```
niri-meta
  └── clones equisdots/plugins-niri into ~/.local/share/equisdots-niri/plugins-niri
  └── deploy_default_plugins prefers plugins-niri/plugins/<id> over the hub
  └── after the shell overlays, re-deploys the plugins-niri plugins so an old
      overlay backup can never restore the Hyprland implementation
```

This repository is intentionally separate from `equisdots/plugins`: the niri
plugin may duplicate UI files when niri needs a different backend, and that
duplication must not leak into the Hyprland plugin.

## License

AGPL-3.0-or-later — see [LICENSE](LICENSE). Copyright (C) 2026 xscriptor <x@xscriptor.com>.

This repository is licensed under the GNU Affero General Public License, version 3 or any later version. If you modify the software and let users interact with it over a network, you must offer them the corresponding source.

No license was declared for releases before 2026-11-13; this license applies from this change.

Third-party components, fonts, icons, images, sounds, vendored code and other assets keep their original licenses and are not covered by this license. See THIRD-PARTY.md / CREDITS.md where present.
