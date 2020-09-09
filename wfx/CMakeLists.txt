# Makefile - wfx-fullMAC-driver
#
# Copyright (c) 2017, Thorvald Natvig
#
# SPDX-License-Identifier: Apache-2.0
#

zephyr_include_directories(
  wfx_fmac_driver
  wfx_fmac_driver/bus
  wfx_fmac_driver/firmware
)

zephyr_include_directories_ifdef(CONFIG_WIFI_WFX_SECURE_LINK
  wfx_fmac_driver/secure_link
)

zephyr_include_directories_ifdef(CONFIG_WIFI_WFX_BUS_SDIO
  sdio
)

zephyr_library()

zephyr_library_sources(
  wfx_fmac_driver/sl_wfx.c
  wfx_fmac_driver/bus/sl_wfx_bus.c
)

if(CONFIG_WIFI_WFX_SECURE_LINK)
  zephyr_compile_definitions(SL_WFX_USE_SECURE_LINK)
  if(CONFIG_WIFI_WFX_SECURE_LINK_PFS)
    zephyr_compile_definitions(SL_WFX_SLK_CURVE25519)
  endif()
  zephyr_library_sources(
    wfx_fmac_driver/secure_link/sl_wfx_secure_link.c
  )
endif()

if(CONFIG_WIFI_WFX_BUS_SDIO)
  zephyr_compile_definitions(SL_WFX_SDIO_BLOCK_SIZE=64)
  zephyr_library_sources(
    wfx_fmac_driver/bus/sl_wfx_bus_sdio.c
    sdio/sdio.c
    sdio/sdiodrv.c
  )
endif()

if(CONFIG_WIFI_WFX_BUS_SPI)
  zephy_library_sources(
    wfx_fmac_driver/bus/sl_wfx_bus_spi.c
  )
endif()
