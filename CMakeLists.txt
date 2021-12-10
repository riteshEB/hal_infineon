# Copyright (c) 2021 Cypress Semiconductor Corporation.
#
# SPDX-License-Identifier: Apache-2.0


## Add PDL sources for XMC devices
add_subdirectory_ifdef(CONFIG_HAS_XMCLIB XMCLib)

## Add PDL, HAL, and other sources for CAT1A devices
if(CONFIG_SOC_FAMILY_CAT1)
  # Add core-lib
  zephyr_include_directories(core-lib/include/)
endif()

if(CONFIG_SOC_FAMILY_CAT1A)
  # Add mtb-hal-cat1
  zephyr_include_directories(mtb-hal-cat1/include/)
  zephyr_include_directories(mtb-hal-cat1/COMPONENT_PSOC6HAL/include/)
  zephyr_include_directories(mtb-hal-cat1/COMPONENT_PSOC6HAL/COMPONENT_CAT1A/include/)

  FILE(GLOB hal_sources mtb-hal-cat1/COMPONENT_PSOC6HAL/source/*.c)
  target_sources(app PRIVATE ${hal_sources})

  FILE(GLOB hal_sources mtb-hal-cat1/COMPONENT_PSOC6HAL/COMPONENT_CAT1A/source/pin_packages/*.c)
  target_sources(app PRIVATE ${hal_sources})

  FILE(GLOB hal_sources mtb-hal-cat1/COMPONENT_PSOC6HAL/COMPONENT_CAT1A/source/triggers/*.c)
  target_sources(app PRIVATE ${hal_sources})

  # Add mtb-pdl-cat1
  zephyr_include_directories(mtb-pdl-cat1/cmsis/include/)
  zephyr_include_directories(mtb-pdl-cat1/drivers/include/)
  zephyr_include_directories(mtb-pdl-cat1/devices/COMPONENT_CAT1A/include/)
  zephyr_include_directories(mtb-pdl-cat1/devices/COMPONENT_CAT1A/include/ip/)

  zephyr_library_sources(mtb-pdl-cat1/devices/COMPONENT_CAT1A/source/cy_device.c)
  zephyr_library_sources(mtb-pdl-cat1/drivers/source/TOOLCHAIN_GCC_ARM/cy_syslib_gcc.S)

  FILE(GLOB pdl_sources mtb-pdl-cat1/drivers/source/*.c)
  target_sources(app PRIVATE ${pdl_sources})

  # Add CM0P image
  # PSoC 6 Cortex M0+ DeepSleep prebuilt image
  if(CONFIG_SOC_PSOC6_CM0P_SLEEP)
    if(CONFIG_SOC_DIE_PSOC6_01)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SLEEP/psoc6_01_cm0p_sleep.c)
    elseif(CONFIG_SOC_DIE_PSOC6_02)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SLEEP/psoc6_02_cm0p_sleep.c)
    elseif(CONFIG_SOC_DIE_PSOC6_03)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SLEEP/psoc6_03_cm0p_sleep.c)
    elseif(CONFIG_SOC_DIE_PSOC6_04)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SLEEP/psoc6_04_cm0p_sleep.c)
    endif()
  endif()

  # PSoC 6 Cortex M0+ Crypto server prebuilt image
  if(CONFIG_SOC_PSOC6_CM0P_CRYPTO)
    if(CONFIG_SOC_DIE_PSOC6_01)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_CRYPTO/psoc6_01_cm0p_crypto.c)
    elseif(CONFIG_SOC_DIE_PSOC6_02)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_CRYPTO/psoc6_02_cm0p_crypto.c)
    elseif(CONFIG_SOC_DIE_PSOC6_03)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_CRYPTO/psoc6_03_cm0p_crypto.c)
    elseif(CONFIG_SOC_DIE_PSOC6_04)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_CRYPTO/psoc6_04_cm0p_crypto.c)
    endif()
  endif()

  # PSoC 64 Cortex M0+ Secure prebuilt image
  if(CONFIG_SOC_PSOC6_CM0P_SECURE AND CONFIG_SOC_DEVICE_SECURE)
    if(CONFIG_SOC_DIE_PSOC6_01)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SECURE/psoc6_01_cm0p_secure.c)
    elseif(CONFIG_SOC_DIE_PSOC6_02)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SECURE/psoc6_02_cm0p_secure.c)
    elseif(CONFIG_SOC_DIE_PSOC6_03)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SECURE/psoc6_03_cm0p_secure.c)
    elseif(CONFIG_SOC_DIE_PSOC6_04)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_SECURE/psoc6_04_cm0p_secure.c)
    endif()
  endif()

  # PSoC 6 Cortex M0+ BLESS Controller prebuilt image
  if(CONFIG_SOC_PSOC6_CM0P_BLESS AND CONFIG_HAS_BLE)
    if(CONFIG_SOC_SERIES_PSOC6_S1)
      zephyr_library_sources(psoc6cm0p/COMPONENT_CM0P_BLESS/psoc6_cm0p_bless.c)
    endif()
  endif()
endif()