# Copyright (c) 2022 Cypress Semiconductor Corporation.
#
# SPDX-License-Identifier: Apache-2.0

# Add mtb-pdl-cat1
zephyr_compile_definitions(${CONFIG_SOC_PART_NUMBER})
zephyr_include_directories(drivers/include)
zephyr_include_directories(devices/COMPONENT_CAT1A/include)
zephyr_include_directories(devices/COMPONENT_CAT1A/include/ip)
zephyr_include_directories(devices/COMPONENT_CAT1A/templates/COMPONENT_MTB)

zephyr_library_sources(devices/COMPONENT_CAT1A/source/cy_device.c)
zephyr_library_sources(drivers/source/TOOLCHAIN_GCC_ARM/cy_syslib_gcc.S)

zephyr_library_sources_ifdef(CONFIG_CPU_CORTEX_M4
devices/COMPONENT_CAT1A/templates/COMPONENT_MTB/COMPONENT_CM4/system_psoc6_cm4.c)
zephyr_library_sources_ifdef(CONFIG_CPU_CORTEX_M0PLUS
devices/COMPONENT_CAT1A/templates/COMPONENT_MTB/COMPONENT_CM0P/system_psoc6_cm0plus.c)

# Peripheral drivers
zephyr_library_sources_ifdef(CONFIG_SERIAL drivers/source/cy_scb_uart.c)
zephyr_library_sources_ifdef(CONFIG_ADC drivers/source/cy_sar.c)
zephyr_library_sources_ifdef(CONFIG_I2C drivers/source/cy_scb_i2c.c)
zephyr_library_sources_ifdef(CONFIG_SPI drivers/source/cy_scb_spi.c)
zephyr_library_sources_ifdef(CONFIG_COUNTER drivers/source/cy_tcpwm_counter.c)
zephyr_library_sources_ifdef(CONFIG_PWM drivers/source/cy_tcpwm_pwm.c)
zephyr_library_sources_ifdef(CONFIG_LPTIMER_INFINEON_CAT1 drivers/source/cy_mcwdt.c)
zephyr_library_sources_ifdef(CONFIG_RTC_INFINEON_CAT1 drivers/source/cy_rtc.c)
zephyr_library_sources_ifdef(CONFIG_SOC_FAMILY_PSOC6 drivers/source/cy_sysint.c)
if(CONFIG_SOC_PSOC6_CM0P_SECURE)
zephyr_library_sources_ifdef(CONFIG_SOC_PSOC6_CM0P_SECURE drivers/source/cy_pra.c)
zephyr_library_sources_ifdef(CONFIG_SOC_PSOC6_CM0P_SECURE drivers/source/cy_pra_cfg.c)
endif()

if(CONFIG_TRNG_INFINEON_CAT1)
zephyr_library_sources(drivers/source/cy_crypto.c)
zephyr_library_sources(drivers/source/cy_crypto_core_trng_v1.c)
zephyr_library_sources(drivers/source/cy_crypto_core_trng_v2.c)
endif()

if(CONFIG_SERIAL OR CONFIG_I2C OR CONFIG_SPI)
zephyr_library_sources(drivers/source/cy_scb_common.c)
endif()

if(CONFIG_ADC)
zephyr_library_sources(drivers/source/cy_sysanalog.c)
endif()

# Common part
zephyr_library_sources(drivers/source/cy_flash.c)
zephyr_library_sources(drivers/source/cy_gpio.c)
zephyr_library_sources(drivers/source/cy_ipc_drv.c)
zephyr_library_sources(drivers/source/cy_ipc_pipe.c)
zephyr_library_sources(drivers/source/cy_ipc_sema.c)
zephyr_library_sources(drivers/source/cy_prot.c)
zephyr_library_sources(drivers/source/cy_sd_host.c)
zephyr_library_sources(drivers/source/cy_sysclk.c)
zephyr_library_sources(drivers/source/cy_syslib.c)
zephyr_library_sources(drivers/source/cy_syspm.c)
zephyr_library_sources(drivers/source/cy_systick.c)
zephyr_library_sources(drivers/source/cy_trigmux.c)
zephyr_library_sources(drivers/source/cy_wdt.c)
