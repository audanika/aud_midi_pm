# References

External specifications and reference implementations the aud_midi
family is built on, downloaded on 2026-10-06 during ticket audmidi. They
are kept here for offline reading and for AI agents, which read the text
extractions.

Rules:

- Read the code here to understand a protocol; never copy it into an
  aud_midi package. Every file keeps its own license, listed below; none
  of it falls under the MIT license of this repository.
- Files are unmodified copies; folders below `code/` mirror the path in
  the original repository.
- The MIDI Association documents are not in git, see
  [MIDI Association documents](#midi-association-documents).

## Specifications

| File | Document | Source | License |
| --- | --- | --- | --- |
| `midi-association/M2-104-UM_v1-1-1_UMP_and_MIDI_2-0_Protocol_Specification.pdf` | Universal MIDI Packet (UMP) Format and MIDI 2.0 Protocol, v1.1.1, 2023-07-19 | [AMEI mirror](https://amei.or.jp/midistandardcommittee/MIDI2.0/MIDI2.0-DOCS/M2-104-UM_v1-1-1_UMP_and_MIDI_2-0_Protocol_Specification.pdf) | © MMA and AMEI, all rights reserved |
| `midi-association/M2-104-UM_v1-1-1_…txt` | Text extraction of the PDF above (pypdf; figures and bit diagrams are lost, Appendix F/G tables survive) | generated | as the PDF |
| `midi-association/M2-104-UM_v1-0_UMP_and_MIDI_2-0_Protocol_Specification.pdf` | UMP Format and MIDI 2.0 Protocol, v1.0, 2020-02-20; still the source for the wording of Appendix D (translation) | [AMEI mirror](https://amei.or.jp/midistandardcommittee/MIDI2.0/MIDI2.0-DOCS/M2-104-UM_v1-0_UMP_and_MIDI_2-0_Protocol_Specification.pdf) | © MMA and AMEI, all rights reserved |
| `midi-association/M2-104-UM_v1-0_…txt` | Text extraction of the PDF above | generated | as the PDF |
| `ietf/rfc6295.txt` | RFC 6295, RTP Payload Format for MIDI | [rfc-editor.org](https://www.rfc-editor.org/rfc/rfc6295.txt) | IETF Trust, verbatim copies allowed |
| `ietf/rfc4696.txt` | RFC 4696, An Implementation Guide for RTP MIDI | [rfc-editor.org](https://www.rfc-editor.org/rfc/rfc4696.txt) | IETF Trust, verbatim copies allowed |
| `ietf/rfc3550.txt` | RFC 3550, RTP: A Transport Protocol for Real-Time Applications | [rfc-editor.org](https://www.rfc-editor.org/rfc/rfc3550.txt) | IETF Trust, verbatim copies allowed |

Not included, because they are only available behind a midi.org login:
the MIDI 1.0 Detailed Specification, the BLE-MIDI specification and
M2-124-UM Network MIDI 2.0 (UDP). For Network MIDI 2.0 the Zephyr and
Windows MIDI Services code below, including Microsoft's spec conformance
review, stands in.

## Reference implementations

| Folder | What | Source (branch as of 2026-10-06) | License | Used for |
| --- | --- | --- | --- | --- |
| `code/linux-kernel/` | `sound/core/ump_convert.c`, `include/sound/ump_convert.h`, `include/sound/ump_msg.h` | [torvalds/linux](https://github.com/torvalds/linux) `master` | GPL-2.0-or-later, see `GPL-2.0` | UMP bit layouts, MIDI 1.0 ↔ UMP conversion |
| `code/am-midi2-lib/` | AM_MIDI2.0Lib by Andrew Mee: byte stream ↔ UMP, UMP → MIDI 1.0/2.0 protocol, UMP processor | [midi2-dev/AM_MIDI2.0Lib](https://github.com/midi2-dev/AM_MIDI2.0Lib) `main` | MIT, see `LICENSE` | Translation rules, value scaling |
| `code/zephyr/` | `subsys/net/lib/midi2/netmidi2.c`, `include/zephyr/net/midi2.h` | [zephyrproject-rtos/zephyr](https://github.com/zephyrproject-rtos/zephyr) `main` | Apache-2.0, see `LICENSE` | Network MIDI 2.0 (UDP) host |
| `code/windows-midi-services/` | Network MIDI 2.0 transport of Windows MIDI Services and its `SPEC_REVIEW.md` | [microsoft/MIDI](https://github.com/microsoft/MIDI) `main` | MIT, see `LICENSE` | Network MIDI 2.0 (UDP) commands, authentication, FEC |
| `code/wireshark/` | `epan/dissectors/packet-applemidi.c` | [wireshark/wireshark](https://github.com/wireshark/wireshark) `master` | GPL-2.0-or-later, see `COPYING` | AppleMIDI session commands (IN, OK, NO, BY, CK, RS, RL) |
| `code/alsa-lib/` | Public headers `include/` of alsa-lib | [alsa-project/alsa-lib](https://github.com/alsa-project/alsa-lib) tag `v1.2.16.1` | LGPL-2.1-or-later, see `COPYING` | ALSA sequencer and UMP API for the Linux backend |

## MIDI Association documents

The MIDI Association specifications state: "No part of this document may
be reproduced or transmitted in any form or by any means … without
permission in writing from the MIDI Manufacturers Association." This
repository is public on GitHub, so `midi-association/` is listed in
`.gitignore`: the files stay on the machine that downloaded them and are
never pushed. To get them on another machine, download them from the
links above or from [midi.org](https://midi.org/specifications).
