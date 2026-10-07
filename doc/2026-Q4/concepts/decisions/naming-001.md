# naming-001: All public types carry the Midi prefix

- Status: accepted
- Date: 2026-10-06
- Canonical source: code guide, "Name things consistently"
- Open work: none

The code guide asks for the package prefix on every type. The plan's
short names such as `NoteOn2`, `ControlChange2` or `RegisteredController`
become `MidiNoteOn2`, `MidiControlChange2` and `MidiRegisteredController`.
UMP-specific types use `Ump` (`Ump`, `UmpMessageType`, `UmpEncoder`), and
`FakeMidiBackend` keeps the name the plan gave it.
