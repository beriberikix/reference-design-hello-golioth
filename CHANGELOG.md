<!-- Copyright (c) 2023 Golioth, Inc. -->
<!-- SPDX-License-Identifier: Apache-2.0 -->

# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Add support for the Aludel Elixir (`aludel_elixir_ns`) board.

### Fixed

- Fix typo (`app_sensors_read_and_steam` → `app_sensors_read_and_stream`)
- Fix RPC registration error handling
- Fix an issue on boards using LTE connectivity where the Golioth Client was not
  started automatically (see
  https://github.com/golioth/reference-design-template/pull/92 for details).

### Changed

- Change `app_sensors_init` to `app_sensors_set_client`. On cellular boards,
  `app_sensors_set_client` is not guaranteed to run before
  `app_sensors_read_and_stream`, so any sensor initialization should moved to a
  separate function (e.g. `app_sensors_init`) that runs before
  `app_sensors_read_and_stream`.
- Upgrade to Golioth Firmware SDK at v0.11.0

### Removed

- Remove unused `click-i2c` alias from nRF DK boards.

## [template_v2.0.0] - 2024-02-21

### Breaking Changes

- Migrate to Golioth Firmware SDK at v0.10.0
    - All header file and API call names have changed
    - Many Golioth Kconfig symbols have changed
    - OTA firmware update code is greatly simplified

### Added

- GitHub Actions workflows to build release binaries

### Changed

- Firmware version number is now passed as a symbol in the prj.conf file and not as a build argument
- Use LTE Link handler from Golioth Common Library
    - The majority of LTE Link handler callback is logging so this has been reused from the common
      library
    - An additional callback is registered in the application just to service on-connect events
- Board definitions related to Ostentus face place moved to a common file that may be included when
  needed

## [template_v1.2.0] - 2023-11-08

### Added
- GitHub workflow to create draft release and add compiled binaries to it.

### Changed
- Update to most recent Golioth Zephyr SDK release v0.8.0 which uses:
  - nRF Connect SDK v2.5.0(NCS)
  - Zephyr v3.5.0
- Upgrade `golioth/golioth-zephyr-boards` dependency to [`v1.0.1`](https://github.com/golioth/golioth-zephyr-boards/tree/v1.0.1)
- Dependencies use https instead of ssh GitHub URLs
- libostentus removed from code base and included as a Zephyr module
- renamed app_work.c/h to app_sensors.c/h

### Fixed
- Fix build error when `CONFIG_LIB_OSTENTUS=n` on the `aludel_mini_v1_sparkfun9160` board.

## [template_v1.1.0] - 2023-08-18

### Breaking Changes
- Golioth services (RPC, Settings, etc.) now use zcbor instead of qcbor
- golioth-zephyr-boards repo now included as a module
  - Remove `golioth-boards` directory
  - Remove `golioth-boards` from .gitignore
  - Remove `zephyr/module.yml`
- zephyr-network-info repo no included as a module
  - Remove `src/network_info` directory
  - Remove `network_info/` from .gitignore
  - Remove `add_subdirectory(src/network_info)` from CMakeLists.txt

### Changed
- update to most recent Golioth Zephyr SDK release v0.7.1 which uses:
  - nRF Connect SDK v2.4.1 (NCS)
  - Zephyr v3.3.99-ncs1-1
- update DFU flash.c/flash.h files
- update board config for nrf9160dk_nrf9160_ns and aludel_mini_v1_sparkfun9160_ns
- update LTE link control: Disable samples/common link control and use in-app link control to start
  connection asynchronously

### Fixed
- main.c: return int from main()
- battery_monitor.c: use void as initialization param
- main.c: use LOG_ERR() instead of printk() for button errors

## [template_v1.0.1] - 2023-07-14

### Fixed
- Turn on Golioth LED when connected
- Correctly reset `desired` endpoints when `example_int1` is changed by itself
- Fix deadlock behavior when running `set_log_level` RPC multiple times
- Add missing license info
- Removed unused dependencies
- Code formatting
- Typos
- Document forking/merging recommendations

## [template_v1.0.0] - 2023-07-11

### Added
- Initial release
- Support for aludel_mini_v1_sparkfun9160 (custom Golioth board)
- Support for nrf9160dk_nrf9160_ns (commercially available)
