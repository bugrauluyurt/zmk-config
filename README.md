# ZMK Config — PandaKB Lily58 Choc v2

ZMK firmware configuration for the [PandaKB](https://pandakb.com/) Lily58 split keyboard with nice!nano v2 controllers.

If you own a PandaKB Lily58 and are looking for a working ZMK config — this is it. The official firmware can be hard to track down, so this repo is set up to build out of the box via GitHub Actions.

## Hardware

| Component | Details |
|-----------|---------|
| Keyboard | PandaKB Lily58 Choc v2 (MX-compatible) |
| Controller | nice!nano v2 (x2) |
| Display | nice!view OLED (x2) |
| LEDs | WS2812 RGB underglow |
| Connectivity | Bluetooth 5.0 (BLE) |

## Features

- **3-layer keymap** — Default (QWERTY), Lower (symbols/nav), Raise (F-keys/BT/RGB)
- **OLED displays** — Custom status screen with gem/diamond animation on the right half
- **RGB underglow** — WS2812 with auto-off on idle, max brightness 60%
- **BLE optimization** — Increased TX power (+8 dBm) and experimental connection parameters for lower latency
- **Power management** — Idle timeout at 10 min, deep sleep at 15 min, external power toggle key
- **Media keys** — Play/pause and mute on the center thumb cluster
- **5 BT profiles** — Switch between paired devices with dedicated keys

## Keymap

### Layer 0 — Default

```
,-----------------------------------------.                    ,-----------------------------------------.
| ESC  |   1  |   2  |   3  |   4  |   5  |                    |   6  |   7  |   8  |   9  |   0  |BckSp |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
| Tab  |   Q  |   W  |   E  |   R  |   T  |                    |   Y  |   U  |   I  |   O  |   P  |  \|  |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
| GUI  |   A  |   S  |   D  |   F  |   G  |-------.    ,-------|   H  |   J  |   K  |   L  |   ;  |  '   |
|------+------+------+------+------+------|  P/P  |    | Mute  |------+------+------+------+------+------|
|LShift|   Z  |   X  |   C  |   V  |   B  |-------|    |-------|   N  |   M  |   ,  |   .  |   /  |RShift|
`-----------------------------------------/       /     \      \-----------------------------------------'
                  | LCTL | LAlt |LOWER | /Space  /       \Enter \  |RAISE | Left |Right |
                  |      |      |      |/       /         \      \ |      |      |      |
                  `----------------------------'           '------''--------------------'
```

### Layer 1 — Lower (symbols & navigation)

```
,-----------------------------------------.                    ,-----------------------------------------.
|   `  |   ~  |   @  |   #  |   $  |   %  |                    |   ^  |   &  |   (  |   )  |   -  |   =  |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
|      |      |      |      |      |      |                    |      |   [  |   ]  |   {  |   }  |  |   |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
|      |      |      |      |      |      |-------.    ,-------| PgUp |      |   <  |   >  |  Up  |      |
|------+------+------+------+------+------|       |    |       |------+------+------+------+------+------|
|LShift|      |      |      |      |      |-------|    |-------| PgDn |      |      | Left | Down |Right |
`-----------------------------------------/       /     \      \-----------------------------------------'
                  | LCTL | LAlt |LOWER | /Space  /       \Enter \  |RAISE | Home | End  |
                  |      |      |      |/       /         \      \ |      |      |      |
                  `----------------------------'           '------''--------------------'
```

### Layer 2 — Raise (F-keys, Bluetooth & RGB)

```
,-----------------------------------------.                    ,-----------------------------------------.
|BT_CLR| BT 0 | BT 1 | BT 2 | BT 3 | BT 4 |                  |EP_TOG|      |      |   _  |   +  | Del  |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
|RGBTOG|RGBEFF|RGB B+|RGB B-|RGB H+|RGB H-|                    |      |      |      |   [  |   ]  |  \   |
|------+------+------+------+------+------|                    |------+------+------+------+------+------|
|  F1  |  F2  |  F3  |  F4  |  F5  |  F6  |-------.    ,-------|      | Left | Down |  Up  |Right |      |
|------+------+------+------+------+------|       |    |       |------+------+------+------+------+------|
|  F7  |  F8  |  F9  | F10  | F11  | F12  |-------|    |-------|      |      |      |      |      |      |
`-----------------------------------------/       /     \      \-----------------------------------------'
                  |      |      |LOWER | /Space  /       \Enter \  |RAISE |      |      |
                  |      |      |      |/       /         \      \ |      |      |      |
                  `----------------------------'           '------''--------------------'
```

## Configuration Highlights

| Setting | Value |
|---------|-------|
| BLE TX Power | +8 dBm |
| BLE Experimental Conn | Enabled (lower latency) |
| RGB Max Brightness | 60% |
| RGB Auto-off on Idle | Yes |
| Battery Report Interval | 30s |
| Idle Timeout | 10 minutes |
| Sleep Timeout | 15 minutes |
| Right OLED Animation | Gem/diamond |

## How to Use

1. **Fork this repo** to your own GitHub account
2. **GitHub Actions** will automatically build the firmware on every push
3. Download the `.uf2` files from the Actions build artifacts
4. **Flash each half**: double-tap the reset button on the nice!nano to enter bootloader mode, then copy the corresponding `.uf2` file to the USB drive that appears
   - `Lily58_L-nice_nano_v2-zmk.uf2` for the left half
   - `Lily58_R-nice_nano_v2-zmk.uf2` for the right half
5. To clear BLE pairing issues, flash `settings_reset-nice_nano_v2-zmk.uf2` first, then re-flash the normal firmware

## Customization

- **Keymap**: Edit `config/Lily58.keymap`
- **Hardware settings**: Edit `config/Lily58.conf`
- **Build targets**: Edit `build.yaml`

Use the [ZMK Keymap Editor](https://nickcoutsos.github.io/keymap-editor/) for a visual way to edit your keymap.

## Dependencies

This config pulls in the following ZMK modules via `config/west.yml`:

| Module | Source | Purpose |
|--------|--------|---------|
| ZMK Firmware | [zmkfirmware/zmk](https://github.com/zmkfirmware/zmk) (v0.3) | Base firmware |
| PandaKB Module | [PandaKBLab/zmk-for-PandaKB](https://github.com/PandaKBLab/zmk-for-PandaKB) (`PandaKB_Lily58` branch) | Lily58 shield definitions for PandaKB |
| Nice OLED | [mctechnology17/zmk-nice-oled](https://github.com/mctechnology17/zmk-nice-oled) | OLED widgets, animations, battery display |

## Links

- [PandaKB](https://pandakb.com/) — Keyboard manufacturer
- [ZMK Firmware](https://zmk.dev/) — Documentation & guides
- [nice!nano v2](https://nicekeyboards.com/nice-nano/) — Wireless controller
