# Little Stereo

Little Stereo adds per-output stereo controls to Omarchy's audio panel. Reverse
left and right channels for speakers that are physically arranged the other
way around, adjust balance, and let Little Stereo remember both settings for
each output device.

![Little Stereo audio controls](docs/little-stereo-controls.png)

## Features

- Reverse stereo channels before audio reaches the selected output, including
  Bluetooth devices.
- Remember stereo reversal independently for every output.
- Adjust balance against the audible left and right sides, even when stereo is
  reversed.
- Keep the selected master volume stable while changing balance.
- Show compact reversal and balance indicators on affected outputs.

## Install

```bash
omarchy plugin add https://github.com/erikabel/little-stereo --enable --yes
omarchy plugin disable omarchy.audio
```

Little Stereo replaces the built-in audio bar widget, so the built-in
`omarchy.audio` widget should be disabled while Little Stereo is enabled.

## Remove

Reset Little Stereo's saved settings and generated WirePlumber configuration
before removing the plugin:

```bash
~/.config/omarchy/plugins/io.github.erikabel.little-stereo/scripts/little-stereo cleanup
omarchy plugin remove io.github.erikabel.little-stereo
omarchy plugin enable omarchy.audio
```

The cleanup command restarts WirePlumber and the Omarchy shell so the normal
audio path is restored immediately.

## How it works

Settings are saved under `~/.config/omarchy/audio`. Stereo reversal is applied
with a generated WirePlumber filter rule, upstream of the selected physical or
Bluetooth output. Balance uses per-channel PipeWire volume while preserving the
chosen master level.

This project is based on Omarchy's built-in Audio plugin and is distributed
under the MIT License.
