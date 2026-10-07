# network-001: Session backends, one protocol each

- Status: accepted
- Date: 2026-10-06
- Canonical source: aud_midi_network
- Open work: IPv6; interop with Apple's driver and Windows MIDI Services

`MidiNetworkSessionBackend` runs either AppleMIDI (RTP-MIDI, byte ports)
or Network MIDI 2.0 (UDP, UMP ports) per instance; offering both needs two
instances with distinct names, because the name is the port-id prefix the
composite backend routes by. Network MIDI 2.0 authentication needs
SHA-256, so the package depends on `crypto` in addition to the plan's
list. `MIDINetworkSession` is inactive on macOS (it works on iOS), so macOS
uses the pure-Dart AppleMIDI session with a Bonjour advertiser from
`aud_midi_apple`. Sessions bind IPv4 only for now.
