# translation-001: Default MIDI 1.0 ↔ 2.0 translation rules

- Status: accepted
- Date: 2026-10-06
- Canonical source: M2-104-UM v1.0 Appendix D, v1.1.1 Appendix D
- Open work: none

The translators follow the Default Translation Mode of M2-104-UM. A MIDI
1.0 Note On with velocity 0 becomes a MIDI 2.0 Note Off with velocity
0x0000 (D.3.1; AM_MIDI2.0Lib uses 0x8000, the Linux kernel 0x0000). Bank
Select values wait for the next Program Change; RPN/NRPN selections and
Data Entry MSB wait for Data Entry LSB (CC 38); single CC 6, 38, 98–101
do not translate; Data Increment/Decrement stay control changes. An
optional alternate mode (`flushDataEntryMsb`) also sends an MSB-only data
entry when a new selection arrives, for senders without CC 38. MIDI 2.0
Note On velocities that scale down to 0 become 1. Messages without a MIDI
1.0 equivalent are dropped with an `untranslatable` diagnostic.
