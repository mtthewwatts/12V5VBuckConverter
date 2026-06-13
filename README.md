# 12V to 5V Buck Converter

KiCad project for a 12V → 5V step-down (buck) DC/DC converter.

## Key ICs / Components

| Reference | Part | Description |
|-----------|------|-------------|
| IC1 | LM2679SD-5.0/NOPB | 8V–40V, 5A Step-Down Switching Regulator (Texas Instruments) |
| D1 | VS-6TQ045S-M3 | 45V, 6A Schottky Diode — D2PAK (Vishay) |

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
