# Board test tool

A desktop test runner for Mo62A boards. It connects to the board over SSH,
runs the selected hardware checks and writes an HTML report with captured
images. The GUI is built with PySide6; there is no headless or command-line
mode yet, and the only report format is HTML.

Origin: migrated from the Mo62A repository, directory `tools/mo62a-auto-test`
(Apache-2.0). Application version string: `2.0.0`.

## Requirements

Host: Python 3.10 or newer and the packages in `requirements.txt`
(PySide6, paramiko, pyserial, Jinja2, Pillow, opencv-python). For the
Ethernet throughput test the host also needs `iperf3`; see
[`bin/README.md`](bin/README.md) for Windows.

Board: a Mo62A running Mo OS with SSH enabled. The connection dialog asks for
IP address, user and password; the defaults are the public factory defaults
(`debian`, port 22). Change the factory password before use on a network you
do not control.

```bash
python3 -m pip install -r requirements.txt
python3 main.py
```

## Covered checks

36 test classes in nine groups, registered in `interface/registry.py`:

| Group | Tests |
| --- | --- |
| system | firmware version, kernel version, CPU cores, CPU temperature, uptime |
| rtc | PCF85363 device, read, tick, write |
| storage | SD card capacity/read/write, DDR capacity/bandwidth |
| network | Ethernet speed/IP/iperf, Wi-Fi scan/signal, Bluetooth scan/signal |
| display | red/green LED, HDMI status/screen, IMX219 detect/capture |
| power | power button, battery hold, fan control |
| usb | hub, ports, read |
| audio | HDMI audio output, headphone loopback |
| expansion | 40-pin GPIO loopback (requires the loopback fixture) |

Several tests need fixtures or an operator: an HDMI display, an IMX219 camera
module, a headphone loopback cable, the GPIO loopback board and a reachable
`iperf3` server. Tests report `skip` with a reason when the fixture is absent.

Not covered yet: EEPROM, the S1 key, C7x inference, and headless/JSON output
for production lines.

## Layout

| Path | Content |
| --- | --- |
| `main.py` | Entry point |
| `gui/` | Welcome, connect, select and run pages |
| `connection/` | SSH session (`SSHBoard`), board discovery, connection history |
| `interface/` | One package per test group; `base.py` defines `TestCase` |
| `reporter/` | HTML report generation |
| `config/` | Settings and UI strings (English and Chinese) |
| `assets/` | IMX219 DCC binaries used by the camera capture test |
| `picture/` | Product image shown on the welcome page |
| `bin/` | Optional Windows `iperf3.exe` location (not committed) |
| `reports/` | Created at run time for reports and captured audio (ignored) |
