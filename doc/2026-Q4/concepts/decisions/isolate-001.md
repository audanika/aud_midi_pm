# isolate-001: Other isolates attach through an explicit connector

- Status: accepted
- Date: 2026-10-06
- Canonical source: Dart 3.13 `dart:isolate` (no name server outside
  Flutter's `dart:ui`)
- Open work: none

Pure Dart has no process-wide registry for `SendPort`s. `Midi.open()`
spawns the MIDI isolate once per isolate that calls it first and returns
a shared proxy inside that isolate. Another isolate attaches to the same
MIDI isolate with `Midi.attach(connector)`, where the sendable connector
comes from the first proxy and is passed to the worker, e.g. as the
argument of `Isolate.spawn`.
