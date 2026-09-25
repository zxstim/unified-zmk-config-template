# Sofle ZMK config

ZMK firmware for my Sofle (nice!nano controllers, ZMK v0.3), built by GitHub Actions.

- `config/sofle.keymap`: my four layers (default / lower / raise / adjust), as they were in ZMK Studio, with
  two changes:
  - LOWER and RAISE also tell the Mac when they're held (F16–F19), so
    [zmkaid](../zmkaid), the on-screen layer overlay, can show the right layer.
  - RAISE's Undo / Cut / Copy / Paste send ⌘Z / ⌘X / ⌘C / ⌘V.
- `config/sofle.conf`: OLED displays, encoders and RGB underglow on.
- `build.yaml`: left half (with ZMK Studio), right half, and `settings_reset` for recovery.

## Build

Push to GitHub. The **Actions** tab runs "Build ZMK firmware"; when it finishes, download the `firmware`
artifact (a zip of `.uf2` files). In a fork, Actions starts disabled: open the Actions tab and enable it once.

## Flash

For each half, one at a time:

1. Plug the half into the Mac with USB.
2. Quickly press its reset button twice. A drive called `NICENANO` appears.
3. Drag the matching file onto it: `sofle_left-nice_nano_v2-zmk.uf2` for the left half,
   `sofle_right-nice_nano_v2-zmk.uf2` for the right. The drive disappears when it's done.

Then, with the left half plugged in by USB, open ZMK Studio and click **Restore Stock Settings**. Studio keeps its
own saved copy of the keymap, which otherwise overrides the one in this repo.

## If something goes wrong

- **Halves don't talk to each other, or Bluetooth misbehaves:** flash `settings_reset-nice_nano_v2-zmk.uf2` to
  both halves, then flash the normal files again, then re-pair Bluetooth with the Mac.
- **Back to the original firmware:** drag the backups in `../sofle-backups/` onto each half the same way
  (see its README).
