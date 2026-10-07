# apple-001: No legacy CoreMIDI packet-list path

- Status: accepted
- Date: 2026-10-06
- Canonical source: Flutter 3.47 app templates (iOS 15.0, macOS 12.0)
- Open work: none

`aud_midi_apple` uses only the UMP event-list API of CoreMIDI
(`MIDIInputPortCreateWithProtocol`, `MIDISendEventList`, virtual endpoints
with protocol), available since macOS 11 and iOS 14. Flutter's minimum
deployment targets are above that floor, so the deprecated packet-list
path of step 2 of the plan is not implemented.
