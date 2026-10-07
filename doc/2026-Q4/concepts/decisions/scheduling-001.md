# scheduling-001: Cancellable OS scheduling with a lookahead

- Status: accepted
- Date: 2026-10-06
- Canonical source: aud_midi_apple loopback probes, aud_midi_web Chrome
  tests, `MidiEngineOptions.lookahead` in aud_midi_core
- Open work: verify driver-owned CoreMIDI destinations (no hardware here)

`MIDIFlushOutput` sends a System Reset (`0xFF`, MIDI 2.0: `0x10ff0000`)
to every virtual destination it flushes, even with nothing pending, and
Chrome 153 has no `MIDIOutput.clear()`. Such ports report `scheduledSend`
but not `cancelPending`, and `aud_midi_apple` never calls
`MIDIFlushOutput`. The engine keeps scheduled packets in its software
queue until `lookahead` before they are due and only then hands them to
the operating system with their original time: they stay cancellable and
still leave with OS precision. `aud_midi` uses 100 ms on native platforms
and no lookahead on the web, where background tabs throttle timers.
`cancelPending()` returns the number of packets the OS still holds.
