# wifi-shell

- name: Wi-Fi shell
- relevant-api: net_stats

Test Wi-Fi functionality using the Wi-Fi shell module.

## Overview

This sample allows testing Wi-Fi drivers for various boards by
enabling the Wi-Fi shell module that provides a set of commands:
scan, connect, and disconnect.  It also enables the net_shell module
to verify net_if settings.

## Building and Running

Verify the board and chip you are targeting provide Wi-Fi support.

For instance you can use Espressif's ESP32-C5 DevKitC by selecting the esp32c5_devkitc/esp32c5/hpcore board or the Xiao's C5 with xiao_esp32c5/esp32c5/hpcore.

```
.. zephyr-app-commands::
   :zephyr-app: shell
   :board: esp32c5_devkitc, xiao_esp32c5
   :goals: build
   :compact:
```

Building commands
===

DevKitC on Zephyr is an old version, it has the v1.1 with 8MB Flash and 4 MB PSRAM. Actual version v1.2 has 8MB Flash and 8 MB PSRAM.

```bash
west build -p -b esp32c5_devkitc/esp32c5/hpcore --sysbuild
west build -p -b xiao_esp32c5/esp32c5/hpcore --sysbuild

west build -b esp32c5_devkitc/esp32c5/hpcore
west build -b xiao_esp32c5/esp32c5/hpcore
```

- Using the Snippets to add configurations:

```bash
west build -p -b esp32c5_devkitc/esp32c5/hpcore --sysbuild -S espressif-psram-8M -S espressif-psram-wifi
west build -p -b xiao_esp32c5/esp32c5/hpcore --sysbuild -S espressif-psram-8M -S espressif-psram-wifi
```

- Flashing the board:

```bash
west flash --esp-device COM20
west espressif monitor -p COM20
```

## Sample console interaction

```bash
shell> wifi scan
Scan requested
shell>
Num  | SSID                             (len) | Chan | RSSI | Sec
1    | kapoueh!                         8     | 1    | -93  | WPA/WPA2
2    | mooooooh                         8     | 6    | -89  | WPA/WPA2
3    | Ap-foo blob..                    13    | 11   | -73  | WPA/WPA2
4    | gksu                             4     | 1    | -26  | WPA/WPA2
----------
Scan request done

shell> wifi connect "gksu" 4 SecretStuff
Connection requested
shell>
Connected
shell>
```