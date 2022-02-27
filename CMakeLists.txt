# Copyright (c) 2022 Cypress Semiconductor Corporation.
# Copyright (c) 2020 Linumiz
# SPDX-License-Identifier: Apache-2.0

zephyr_library_named(modules_hal_infineon)

## Add PDL sources for XMC devices
add_subdirectory_ifdef(CONFIG_HAS_XMCLIB XMCLib)

## Add abstraction-rtos sources
add_subdirectory_ifdef(CONFIG_SOC_FAMILY_CAT1 abstraction-rtos)

## Add mtb-hal-cat1 sources for CAT1 devices
add_subdirectory_ifdef(CONFIG_SOC_FAMILY_CAT1A mtb-hal-cat1)

## Add mtb-pdl-cat1 sources for CAT1 devices
if (CONFIG_SOC_FAMILY_CAT1A OR CONFIG_SOC_FAMILY_PSOC6)
  add_subdirectory(mtb-pdl-cat1)
endif()

## Add core-lib sources for CAT1 devices
if (CONFIG_SOC_FAMILY_CAT1A OR CONFIG_SOC_FAMILY_PSOC6)
  add_subdirectory(core-lib)
endif()

## Add whd-bsp-integration for CYW43xx WIFI devices
add_subdirectory_ifdef(CONFIG_WIFI_CYW43XXX whd-bsp-integration)
