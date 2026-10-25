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
