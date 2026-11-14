# sksequencer
Kondo RF Sequencer

## Function
This board is a TX/RX sequencer for an amateur-radio station. An ATmega328P monitors the PTT line from the radio. When PTT is keyed (pulled to ground), the firmware switches the station in a set order: it removes power from the mast-mounted LNA, switches the coax relays and then enables the power amplifier. When PTT is released, it runs the same steps in reverse. This keeps RF out of the LNA and keeps the relays from switching while RF is present (no hot-switching). The sequence timing is set by the firmware.

## Inputs / Outputs

| Pad | Name | Type | Description |
|-----|------|------|-------------|
| TP13 | 5V PAD | Power in | +5 V logic supply. Protected by F1 (0.5 A polyfuse), Q7 (reverse-polarity P-FET) and D6 (6.8 V TVS) |
| TP15 | V1 | Power in | +15 V LNA supply, switched to the LNA output |
| TP16 | V2 | Power in | +28 V coax-relay supply, switched to the RELAY output |
| TP12 | PTT | Input | PTT from the radio, active low. 10k pull-up to +5 V, 1k series resistor and 100 nF filter cap, to PD2 |
| TP8 | LNA | Output | High-side switched +15 V (Q5 BS250P driven by Q1), with flyback diode |
| TP9 | RELAY | Output | High-side switched +28 V (Q6 BS250P driven by Q2), with flyback diode |
| TP10 | AMP | Output | Low-side open-drain output (Q3 BS170) for amplifier keying, clamped by a 36 V TVS |
| TP11 | OUT#4 | Output | Low-side open-drain output (Q4 BS170), spare, clamped by a 36 V TVS |
| TP14, TP17–TP21 | GND | Ground | Ground pads |

### Headers
| Ref | Description |
|-----|-------------|
| J1 | 1x4, output drive signals PD5, PD6, PD7, PB0 (MCU side of the gate resistors) |
| J2 | 1x6, RESET, PD0/RXD, PD1/TXD, PD2 (PTT), PD3, PD4 |
| J3 | 1x14, PC0–PC5, GND, AREF, +5 V, PB5–PB1 (spare I/O) |
| J4 | 2x3 AVR ISP programming header |
| SW1 | Reset pushbutton |

The MCU runs from a 16 MHz crystal (Y1). D1 is a +5 V power indicator LED.

## Project Files

| File | Description |
|------|-------------|
| `sequencer.kicad_pro` | KiCad project file |
| `sequencer.kicad_sch` | Schematic |
| `sequencer.kicad_pcb` | PCB layout |
| `sequencer.kicad_sym` | Project symbol library (BS250P and others) |
| `ECS-160-18-4X-CKM.kicad_sym` | Symbol for the 16 MHz crystal Y1 |
| `sym-lib-table` | Project symbol library table |
| `fp-lib-table` | Project footprint library table |
| `.gitignore` | Leaves KiCad backups, history, `.kicad_prl` user settings and generated output out of git |

**Note:** `fp-lib-table` references `sequencer footprint library.pretty` (footprints for Y1, Q5 and Q6), which is not yet in the repository.

Created with KiCad 10.
