# infinity60-qmk

QMK keymap for an Input Club Infinity 60% (non-LED, Kiibohd bootloader, MK20DX128).
The old Kiibohd Configurator (configurator.input.club) is gone, so this is built with QMK.

## Keymap `leon`
Based on QMK's `default` keymap for `input_club/infinity60/rev1`.
- Caps Lock position: tap = Esc, hold = Ctrl (`LCTL_T(KC_ESC)`)
- Bottom row: Left Ctrl added bottom-left, Menu and Right Ctrl added bottom-right
- Fn (`MO(1)`, 1u key right of the right Shift): vim arrows on H/J/K/L,
  Home/End on `;` `'`, PgUp/PgDn on `[` `]`, F1-F12 on the number row,
  Caps Lock on Tab, volume on A/S/D

## Build
```sh
git clone https://github.com/qmk/qmk_firmware && cd qmk_firmware
cp -r <this repo>/keymaps/leon keyboards/input_club/infinity60/keymaps/
qmk compile -kb input_club/infinity60/rev1 -km leon
```
On macOS, `arm-none-eabi-gcc@8` (with newlib) and `arm-none-eabi-binutils` must be on PATH;
the newer `arm-none-eabi-gcc` formula has no libc and fails on `stdint.h`.

## Flash
Press the reset button on the back of the PCB (paperclip), then:
```sh
dfu-util -d 1c11:b007 -D firmware-leon.bin
```
`firmware-leon.bin` is the prebuilt binary. The bootloader cannot be read back with
`dfu-util -U`, so there is no backup of the original firmware; the bootloader itself is untouched.
