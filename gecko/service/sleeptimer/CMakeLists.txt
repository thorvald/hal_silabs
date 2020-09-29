# Makefile - Gecko SDK
#
# Copyright (c) 2020, Thorvald Natvig
#
# SPDX-License-Identifier: Apache-2.0
#

# Translate the SoC name and part number into the gecko device and cpu name
# respectively.
zephyr_include_directories(inc config)
zephyr_library()
zephyr_library_sources(src/sl_sleeptimer.c)
if(CONFIG_GECKO_SLEEPTIMER_RTC)
  zephyr_library_compile_definitions(SL_SLEEPTIMER_PERIPHERAL=SL_SLEEPTIMER_PERIPHERAL_RTC)
  zephyr_library_sources(src/sl_sleeptimer_hal_rtc.c)
endif()
if(CONFIG_GECKO_SLEEPTIMER_RTCC)
  zephyr_library_compile_definitions(SL_SLEEPTIMER_PERIPHERAL=SL_SLEEPTIMER_PERIPHERAL_RTCC)
  zephyr_library_sources(src/sl_sleeptimer_hal_rtcc.c)
endif()
