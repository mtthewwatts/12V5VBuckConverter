# 12V → 5V Buck Converter

A custom KiCad-designed buck (step-down) converter PCB that regulates an 11.4V–12V LiPo battery input down to a stable 5V/5A output. Designed to power a Raspberry Pi 5 and control electronics on an autonomous line-following search-and-rescue robot, consolidating the robot's entire power system into a single battery source.

Built for **MTE 380: Mechatronics Engineering Design Workshop** at the University of Waterloo (Group 12).

## Overview

The robot this board was built for is powered by a single 3S 11.4V LiPo battery. Rather than using a separate USB power bank to run the Raspberry Pi and control electronics, this PCB steps the battery voltage down to a regulated 5V/5A rail, cutting weight and wiring complexity. Raw battery voltage still feeds the drive motors directly through a separate motor shield.

- **Input:** 8V–40V (11.4V nominal, 3S LiPo)
- **Output:** 5V regulated, up to 5A continuous
- **Topology:** Synchronous-adjacent buck converter, datasheet reference design
- **Fabrication:** 1 oz copper, ~2mm power traces sized for 25W max output, continuous ground plane

## Key ICs / Components

| Reference | Part | Description |
|-----------|------|--------------|
| IC1 | LM2679SD-5.0/NOPB | 8V–40V, 5A Step-Down Switching Regulator (Texas Instruments) |
| D1 | VS-6TQ045S-M3 | 45V, 6A Schottky Diode — D2PAK (Vishay) |

Full bill of materials is documented in [`docs/Buck_Converter_Reference.docx`](docs/Buck_Converter_Reference.docx).

## Design Notes

This design follows Texas Instruments' [SNVA054C SIMPLE SWITCHER PCB Layout Guidelines](https://www.ti.com/lit/an/snva054c/snva054c.pdf) and the [LM2679 datasheet](https://www.ti.com/lit/ds/symlink/lm2679.pdf) reference application circuit. Key layout decisions:

- **Component placement** minimizes the high-current switching loop — regulator IC, inductor, diode, and capacitors are placed tightly together to reduce parasitic inductance.
- **Routing** keeps battery input and 5V output traces short and direct to limit voltage drop, with the switching node kept compact and isolated from signal traces to reduce noise coupling.
- **Ground plane** provides a low-impedance return path for both electrical stability and thermal performance.
- **Trace widths** (~2mm on high-current paths) were sized using IPC-2221 guidelines for a 5V/5A (25W) maximum load.

See [`docs/Buck_Converter_Reference.docx`](docs/Buck_Converter_Reference.docx) for the full design rationale, and Section 2.2.3 of [`docs/Milestone8_FinalReport.docx`](docs/Milestone8_FinalReport.docx) for how this board fits into the robot's overall electrical architecture.

## Project Files

| File | Purpose |
|------|---------|
| `12V5VBuckConverter.kicad_sch` | Schematic |
| `12V5VBuckConverter.kicad_pcb` | PCB layout |
| `12V5VBuckConverter.kicad_pro` | Project settings |
| `12V5VBuckConverter.step` | 3D STEP model |
| `ProjectLibrary.kicad_sym` | Project symbol library (LM2679) |
| `VS-6TQ045S-M3.kicad_sym` | Diode symbol |
| `VS6TQ045SM3.kicad_mod` | Diode footprint |
| `sym-lib-table` | Symbol library table |
| `fp-lib-table` | Footprint library table |

## Opening the Project

Open `12V5VBuckConverter.kicad_pro` in **KiCad 9.0** or later.

All custom libraries are stored in the project folder and referenced via `${KIPRJMOD}`, so no path changes are needed after cloning.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
# then open 12V5VBuckConverter.kicad_pro in KiCad
```

## Status / Known Limitations

- Validated on the bench and used successfully on Game Day, but battery voltage sag under load was not fully characterized — output behavior at low state-of-charge is a known open item.
- No onboard reverse-polarity or overcurrent protection beyond the regulator IC's internal limiting.
- Designed for a single fixed 5V/5A rail; not currently configurable for other output voltages.

## Background

This board was the electrical subsystem of a larger capstone project: a fully autonomous line-following robot built to navigate a maze, retrieve a target, and return it to a safe zone under a $300 budget and strict size/weight constraints. Full project report and results are in [`docs/Milestone8_FinalReport.docx`](docs/Milestone8_FinalReport.docx).

## License

MIT — see [LICENSE](LICENSE).
