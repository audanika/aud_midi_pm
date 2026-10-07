# packaging-001: The umbrella depends on all backends, Flutter SDK accepted

- Status: accepted
- Date: 2026-10-06
- Canonical source: ticket audmidi, user decision during implementation
- Open work: none

`aud_midi` depends directly on every backend package, including
`aud_midi_android`. That package needs `jni`, whose pubspec requires the
Flutter SDK, so the family no longer installs with the Dart SDK alone.
The "no Flutter" proof of step 0 of the plan is dropped. The packages
`aud_midi_standard`, `aud_midi_core` and `aud_midi_rtp` stay pure Dart
without any Flutter dependency, and `jni` compiles and runs in plain
`dart test` on the VM with the Flutter toolchain's `dart`.
