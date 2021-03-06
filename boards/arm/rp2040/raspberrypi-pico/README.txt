README
======

This directory contains the port of NuttX to the Raspberry Pi Pico.
See https://www.raspberrypi.org/products/raspberry-pi-pico/ for information
about Raspberry Pi Pico.

Currently only the following devices are suppored.

  Supported:
  - UART  (console port)
    - GPIO 0 (UART0 TX) and GPIO 1 (UART0 RX) are used for the console.
  - Flash ROM Boot
  - SRAM Boot
    - If Pico SDK is available, nuttx.uf2 file which can be used in
      BOOTSEL mode will be created.

  Not supported:
  - All other devices

Installation
============

1. Download Raspberry Pi Pico SDK

  $ git clone -b master https://github.com/raspberrypi/pico-sdk.git

2. Set PICO_SDK_PATH environment variable

  $ export PICO_SDK_PATH=<absolute_path_to_pico-sdk_directory>

3. Configure and build NuttX

  $ git clone https://github.com/apache/incubator-nuttx.git nuttx
  $ git clone https://github.com/apache/incubator-nuttx-apps.git apps
  $ cd nuttx
  $ make distclean
  $ ./tools/configure.sh raspberrypi-pico:nsh
  $ make V=1

4. Connect Raspberry Pi Pico board to USB port while pressing BOOTSEL.
   The board will be detected as USB Mass Storage Device.
   Then copy "nuttx.uf2" into the device.
   (Same manner as the standard Pico SDK applications installation.)

5. To access the console, GPIO 0 and 1 pins must be connected to the
   device such as USB-serial converter.

License exceptions
==================

The following files are originated from the files in Pico SDK.
So, the files are licensed under 3-Clause BSD same as Pico SDK.

- arch/arm/src/rp2040/rp2040_clock.c
- arch/arm/src/rp2040/rp2040_pll.c
- arch/arm/src/rp2040/rp2040_xosc.c
  - These are created by referring the Pico SDK clock initialization.

- arch/arm/src/rp2040/hardware/*.h
  - These are generated from rp2040.svd originally provided in Pico SDK.
