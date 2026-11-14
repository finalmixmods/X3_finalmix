# How to play Mega Man X3 Co-op

This repository contains a patch, not the game. To play, you need your own legally obtained copy of **Mega Man X3 (USA)** for the SNES. No ROMs are provided or linked here.

## 1. Check your ROM

The patch only works on Mega Man X3 (USA), unheadered, 2 MB (2,097,152 bytes):

- CRC32: `FA0FE671`
- SHA-1: `b226f7ec59283b05c1e276e2f433893f45027cac`

If your file is 2,097,664 bytes, it has a 512-byte header. Remove the header first (Rom Patcher JS has a "remove header" option).

## 2. Apply the patch

Download `MMX3_Coop_v0.31.6.bps` from the [Releases](../../releases) page, then use one of these:

### In your browser (easiest)

1. Open [Rom Patcher JS](https://www.marcrobledo.com/RomPatcher.js/).
2. For **ROM file**, choose your Mega Man X3 ROM. The page shows its CRC32, so you can check step 1 here.
3. For **Patch file**, choose `MMX3_Coop_v0.31.6.bps`.
4. Click **Apply patch** and save the new file.

### On your computer

1. Download [Flips](https://github.com/Alcaro/Flips) (Windows, Linux; Mac users can use Rom Patcher JS).
2. Open Flips and click **Apply Patch**.
3. Pick `MMX3_Coop_v0.31.6.bps`, then your ROM.
4. Choose where to save the patched game.

Keep your original ROM. Patching makes a new file and doesn't change the original.

## 3. Pick an emulator

Mega Man X3 uses the Cx4 chip, so use an emulator that supports it:

- **snes9x**
- **bsnes**
- **Mesen**
- **RetroArch**, with the snes9x or bsnes core

For co-op, set up two controllers (or a controller and keyboard) as player 1 and player 2.

**Slowdown with two players?** Running two characters is a lot for the SNES CPU, so busy parts of some stages slow down in co-op. If your emulator has a **CPU overclock** option (Snes9x, bsnes and Mesen do; look in the emulation or hack settings), turn it on and most of the slowdown goes away.

## 4. Controls

| What | How |
|---|---|
| Play as X or Zero | Pick **X** or **ZERO** after GAME START |
| Player 2 joins as Zero (as X in a Zero game) | Press **Start on controller 2** during a stage |
| Player 2 leaves | **Select on controller 2** (no life lost) |
| Computer helper (Zero, or X in a Zero game) | Pause with **Start**, press **L**. Press **L** in the pause menu again to send him away |
| Zero's black armor (double damage) | **L or R** on Zero's controller (co-op, Boss Rush, VS). In a Zero game he earns black with his armor parts instead |
| Zero's weapons (Zero game, solo only) | **L / R** |
| Switch between X and Zero | **Select on controller 1** in a stage (the partner switches too) |
| Auto-charge on/off | **X** on either controller |
| Boss Rush, VS mode | On the title menu (VS mode: pick the arena and the music after the players). **B** goes back a menu |
| VS secret: start in the Ride Armor | Press **Select** on the VS MODE screen (a sound plays), then pick **1P VS CPU** |

The full list, and what each mode does, is in the [PATCH_NOTES](PATCH_NOTES.md).

## Troubleshooting

- **"Checksum mismatch" or the patch won't apply:** your ROM is a different version, such as the Japanese Rockman X3 or a re-release, or it still has a header. The patch only works on the unheadered USA version.
- **Black screen or the game won't start:** your emulator may not support the Cx4 chip. Try one of the emulators listed above.
- **The game slows down with two players:** turn on your emulator's CPU overclock option (see step 3).
- **Player 2 can't join:** check that a second controller is set up as player 2 in your emulator's input settings, then press Start on it during a stage, not on a menu.

---

Mega Man X3 © CAPCOM CO., LTD. This is a free fan project, not affiliated with or endorsed by Capcom. Support Capcom by buying the official release: Mega Man X3 is included in Mega Man X Legacy Collection.
