# Mo62A peripheral diagnostics

GPIO, UART5 and PWM loopback scripts belong here because they diagnose board
interfaces and can be reused by a future Studio workflow. They are not complete
applications. Preserve the documented wiring, 3.3 V limits, selected boot entry
and the script dependencies (`gpiod` / `pyserial` as applicable).

Follow https://developer.inhand.online/docs/mo-62a/application-development/gpio-and-peripherals/
for wiring, invocation and recorded results. The scripts were moved unchanged;
this migration did not repeat electrical tests. Local LICENSE and MIGRATION.md
retain their original terms and provenance.
