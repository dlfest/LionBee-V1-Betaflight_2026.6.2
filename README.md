# LionBee V1 — Betaflight 2026.6.2 custom firmware

Community custom build for the **NewBeeDrone LionBee V1 (AT32F435G)**, based on Betaflight 2026.6.2.

> This is an unofficial community build, not an official NewBeeDrone or Betaflight release. Flash and test at your own risk. Remove propellers for initial bench testing.

## v30 status

v30 is the current tested baseline. It has been bench tested and flight tested indoors without GPS.

### Main fixes and defaults

- onboard SPI ExpressLRS / SX1280 support restored on AT32F435G
- ELRS timer compatibility fix
- no personal ELRS UID or bind phrase compiled into the firmware
- craft name: `LionBee`
- maximum arm angle: `180`
- factory-derived LionBee PID/rate/filter defaults
- DShot600 + bidirectional DShot compatibility
- factory motor direction, motor pole count and idle defaults
- QMC5883L compass defaults
- GPS support on UART5
- barometer DPS310
- analog MAX7456 OSD
- RTC6705 analog VTX
- default VTX: Raceband 1 / 5658 MHz / 25 mW
- factory LED defaults
- factory-derived OSD layout
- no custom delayed/repeated VTX restart logic

## ExpressLRS privacy

This public build deliberately **does not contain the developer/test pilot's ELRS bind phrase or personal UID**.

The firmware reset default for `expresslrs_uid` is zero. If you flash with **Full Chip Erase ON**, you will need to bind your receiver again. If you flash with **Full Chip Erase OFF**, an existing stored binding may remain in FC configuration; that does not mean the UID is compiled into this firmware.

`CLI_V30_FACTORY_TUNE_APPLY_NO_UID.txt` can be used to apply the v30 tune while deliberately leaving `expresslrs_uid` untouched.

## Flashing

Use Betaflight Configurator and flash the LionBee v30 HEX.

For a clean installation:
1. Remove propellers.
2. Back up your current configuration.
3. Flash the v30 HEX with Full Chip Erase enabled.
4. Reconnect and bind ExpressLRS again.
5. Calibrate the accelerometer.
6. Verify receiver channels, motor order/direction, VTX and sensors before installing propellers.
7. Test GPS/Position Hold outdoors with a valid GPS fix and enough open space.

If preserving an existing ELRS binding/configuration is more important, flash without Full Chip Erase and use the no-UID CLI tune file as needed.

## Verification

Expected v30 build usage:
- FLASH1: 552665 B / 992 KB (54.41%)
- RAM: 109448 B / 192 KB (55.67%)

HEX SHA-256:

`9d642276e5d4d44bac20da3fe4e2fc58590c16e2b92ee69c5171ca9ccdc60938`

BIN SHA-256:

`58362db6c092c1e20152305929fe263fa6db7b4623e790add68fa4358f838185`

The source/build verification also checks that the previous personal ELRS UID byte sequence is absent and that no LionBee VTX recovery/restart code remains.

## Source modifications

The target config is in `target_config/LIONBEE_V1_config_v30.h`. The v30 source patch is intended to be applied to the matching Betaflight 2026.6.2 source tree.

This build includes LionBee-specific AT32 RX_SPI/ExpressLRS and DShot compatibility changes plus factory-derived reset defaults for the board. Defaults are applied through Betaflight parameter-group reset paths rather than rewriting saved configuration on every boot.

## License

GPL-3.0. This project contains modifications derived from Betaflight and is distributed under the repository's GPL-3.0 license.

## Upstream

Based on Betaflight 2026.6.2. This repository is an independent community project and is not affiliated with or endorsed by NewBeeDrone or the Betaflight project.
