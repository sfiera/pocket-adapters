# AP-A03 Atari Lynx Adapter

Lynx pins are numbered in the opposite orientation from the Game Boy pins. Game Boy pin 1 is near Lynx pin 34, and Lynx pin 1 is near Game Boy pin 32.

As the adapter lacks part references, this document uses the following:

| Ref | Location    | Part                              |
| --- | ----------- | --------------------------------- |
| U1  | Mid right   | Unknown [MCU](mcu.md)             |
| U2  | Mid left    | HC164 [shift register](#shifted)  |
| Q1  | Bottom left | Transistor                        |
| R1  | Below C1    | Resistor (220Ω)                   |
| R2  | Above U1    | Resistor (10kΩ)                   |
| R3  | Above R2    | Resistor (10kΩ)                   |
| R4  | Above U2    | Resistor                          |
| C1  | Below U1    | Capacitor                         |
| C2  | Above Q1    | Capacitor                         |
| C3  | Left of C2  | Capacitor                         |
| D1  | Underside   | LED                               |

## Power

The following pins are connected to +3.3V or ground:

| Lynx Pin | Lynx Use |
| --- | --- |
| 1   | Gnd |
| 33  | +3.3V |

## Control

The Game Boy’s control pins are connected as follows:

| GB Pin | GB Use | Lynx Pin | Lynx Use |
| --- | --- | --- | --- |
| 5   | /CS | *   | U2 |
| 4   | /RD | 10  | /OE |
| 3   | /WR | 27  | /WE |
| 2   | CLK | *   | U2, Q1 via R4 |
| 30  | /RST | *  | MCU via R3 |
| 31  | AUD | 32  | AUD |

The clock pin is used to [latch](#latched) address pins in order to access higher memory addresses.

## Address

The Game Boy’s address pins A0 through A10 are connected to the corresponding Lynx pins in order. The Lynx’s A12 through A19 are connected through a [shift register](#shifted). The Game Boy’s A11 through A15 are unused and the Lynx’s A11 is absent.

| GB Pin | GB Use | Lynx Pin | Lynx Use |
| --- | --- | --- | --- |
| 6   | A0  | 17  | A0  |
| 7   | A1  | 11  | A1  |
| 8   | A2  | 12  | A2  |
| 9   | A3  | 13  | A3  |
| 10  | A4  | 15  | A4  |
| 11  | A5  | 16  | A5  |
| 12  | A6  | 14  | A6  |
| 13  | A7  | 18  | A7  |
| 14  | A8  | 28  | A8  |
| 15  | A9  | 29  | A9  |
| 16  | A10 | 30  | A10 |
| 17  | A11 |     | nc  |
| 18  | A12 |     | nc  |
| 19  | A13 |     | nc  |
| 20  | A14 |     | nc  |
| 21  | A15 |     | nc  |
|     |     | 26  | A12 |
|     |     | 25  | A13 |
|     |     | 24  | A14 |
|     |     | 23  | A15 |
|     |     | 19  | A16 |
|     |     | 20  | A17 |
|     |     | 21  | A18 |
|     |     | 22  | A19 |

## Data

The Game Boy’s 8 data pins are connected to the corresponding Lynx pins in order:

| GB Pin | GB Use | Lynx Pin | Lynx Use |
| --- | --- | --- | --- |
| 22  | D0  | 7   | D0  |
| 23  | D1  | 5   | D1  |
| 24  | D2  | 3   | D2  |
| 25  | D3  | 2   | D3  |
| 26  | D4  | 4   | D4  |
| 27  | D5  | 6   | D5  |
| 28  | D6  | 8   | D6  |
| 29  | D7  | 9   | D7  |

## Shifted

Because the Game Boy has fewer address pins (16) than the Lynx (19), the adapter includes a HC164 shift register. The shifts CLK into the register on /CS and provides them as A12:19.

| SR Pin | SR Use | Lynx Pin | Lynx Use |
| --- | --- | --- | --- |
| 1   | A   | 1   | Gnd |
| 2   | B   | *   | CLK |
| 3   | QA  | 26  | A12 |
| 4   | QB  | 25  | A13 |
| 5   | QC  | 24  | A14 |
| 6   | QD  | 23  | A15 |
| 7   | Gnd | 1   | Gnd |
| 8   | CLK | *   | /CS |
| 9   | /CLR | 33 | +5V |
| 10  | QE  | 19  | A16 |
| 11  | QF  | 20  | A17 |
| 12  | QG  | 21  | A18 |
| 13  | QH  | 22  | A19 |
| 14  | VCC | 33  | +5V |

## Unregulated

On a Lynx, pin 34 has an unregulated voltage sourced from the battery. On the Pocket adapter, it is connected to a PNP transistor controlled by CLK. Perhaps the Pocket sets a voltage with C3 and a duty cycle?

| Q1 Pin | Q1 Use | Lynx Pin | Lynx Use |
| --- | --------- | --- | ---------- |
| 1   | Base      | 34  | SWVCC, C3  |
| 2   | Emitter   |     | +5V        |
| 3   | Collector |     | CLK via R4 |
