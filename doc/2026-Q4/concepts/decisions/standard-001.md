# standard-001: Byte count of Mixed Data Set chunks

- Status: proposed
- Date: 2026-10-06
- Canonical source: M2-104-UM v1.1.1 section 7.9
- Open work: confirm against another implementation or the MIDI
  Association

M2-104-UM says the field "number of valid bytes in this message chunk"
contains the size of the chunk "including the header". `aud_midi_standard`
reads that literally: the 16 header bytes, plus the 2 leading bytes of
each payload packet, plus the data, without padding. Other libraries (e.g.
ktmidi/cmidi2) count payload bytes only, so Mixed Data Sets between them
and aud_midi may disagree until this is settled.
