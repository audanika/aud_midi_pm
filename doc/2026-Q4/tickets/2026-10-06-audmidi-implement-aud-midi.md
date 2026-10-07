# audmidi: Implement aud_midi

## Goal

Implement the package family planned in
[aud_midi_01](2026-10-06-aud_midi_01-initial-midi-implementation.md): a
Dart MIDI package for iOS, macOS, Android, Windows, Linux and the web with
USB, Bluetooth LE, virtual and network MIDI, MIDI 1.0 and MIDI 2.0 (UMP),
FFI instead of platform channels and all I/O in its own isolate. The
ticket covers steps 0 to 12 of that plan in one go; step 13 (BLE
peripheral, Web Bluetooth, routing, MIDI-CI) stays later work.

## Affected repos

| Repo | Change |
| --- | --- |
| `aud_midi_pm` | decisions, architecture, references, this ticket |
| `aud_midi_standard` | messages, `MidiBytes`/`Ump`, codecs, translation, BLE-MIDI, constants (gg_midi_vars migrated), models |
| `aud_midi_core` | contracts, clock, `MidiEngine`, scheduler with lookahead, registry, diagnostics, composite and BLE backends, fake backend |
| `aud_midi_rtp` | RFC 6295 payload and complete recovery journal, session configuration, lossy channel |
| `aud_midi_network` | AppleMIDI and Network MIDI 2.0 sessions, mDNS browsing, session backend, lossy UDP proxy |
| `aud_midi_apple` | CoreMIDI (UMP), virtual endpoints, `MIDINetworkSession`, CoreBluetooth, Bonjour |
| `aud_midi_android` | Java shim plugin, jnigen bindings, AMidi, BLE, NSD, static virtual devices |
| `aud_midi_windows` | C++/WinRT shim, Windows MIDI Services (optional), pairing, DNS-SD |
| `aud_midi_linux` | ALSA sequencer via FFI incl. UMP, reader isolate, BlueZ, Avahi |
| `aud_midi_web` | Web MIDI backend |
| `aud_midi` | `Midi.open()`, MIDI isolate, proxies, backend selection, examples |

## Steps

1. Standard: message model, raw forms, codec signatures (coordinator);
   codecs, models and constants in parallel — done, verified on VM,
   dart2js and Wasm.
2. Core: contracts first, then engine, scheduler, registry, fakes — done.
3. RTP and network — done; property tests under loss converge.
4. Backends in parallel — done; Apple verified on macOS and the iOS
   simulator, Android on the emulator, Web in Chrome; Linux and Windows
   only as Dart logic and portable native parts.
5. Umbrella — MIDI isolate, proxies, backend composition, examples.
6. Every repo passes `gg one can commit` (100 % coverage per file).

Deviations from the plan are recorded as decisions: packaging-001,
translation-001, apple-001, isolate-001, naming-001, scheduling-001,
network-001, standard-001, web-001.

## Open questions

- Linux and Windows: first real build and run (ALSA, BlueZ, Avahi;
  C++/WinRT, Windows MIDI Services, MSVC hook build). A Windows header
  check from macOS would need the Windows SDK, whose license must be
  accepted by a person.
- Hardware tests: USB and BLE-MIDI devices on all platforms, Android API
  levels below 33, driver-owned CoreMIDI destinations (scheduling-001).
- Interop: Apple's network driver with the pure-Dart AppleMIDI session
  (needs the macOS network session enabled manually), Windows MIDI
  Services with Network MIDI 2.0, IPv6.
- Mixed Data Set byte count (standard-001).
- gg_midi_vars: discontinue, or publish a last version that re-exports
  from `aud_midi_standard`? Deprecate the misleading legacy names
  (`nonRegisteredParameterCoarse` = CC 98 is really the NRPN LSB,
  `controller64` … `controller70` hold 84 … 90)?
- UMP endpoint and function block info on Apple: `MIDIUMPEndpointManager`
  is main-thread only and listed no foreign endpoints in a command-line
  process.
- RTP: no tests against packet captures of Apple's driver yet.
