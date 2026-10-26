# Windows iperf3 binary (not committed)

The Ethernet throughput test (`interface/network/ethernet.py`) runs `iperf3` on
the host. On Linux and macOS the `iperf3` found on `PATH` is used. On Windows
the tool first looks for `iperf3.exe` in this directory, then on `PATH`.

The Windows build of iperf3 and the `cygwin1.dll` it depends on are not part of
this repository. Obtain them yourself from the iperf project
(<https://iperf.fr/iperf-download.php>, Windows 64-bit archive), extract
`iperf3.exe` and `cygwin1.dll`, and place both files in this directory. The
`.gitignore` of `board-test/` excludes `*.exe` and `*.dll` so they are never
committed.
