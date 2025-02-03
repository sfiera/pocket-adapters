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
| 5   | /CS | *   | SYSCTL1 |
| 4   | /RD | 10  | /CS0? /OE? |
| 3   | /WR | 27  | /CS1? /WE? |
| 2   | CLK | *   | IODAT, Q1 via R4 |
| 30  | /RST | *  | MCU via R3 |
| 31  | AUD | 32  | AUDIN |

A Lynx will strobe pin 10 (/CS0) and increment A0:10 on each read or write to $FCB2 (RCART0). It will strobe pin 27 (/CS1) and increment A0:10 on each read or write to $FCB3 (RCART1).

The AUDIN pin (auxiliary data in) is a general-purpose IO pin, unrelated to audio. Some carts use it for bank-switching.

## Address

The Game Boy’s address pins A0:A10 are connected to the corresponding Lynx pins in order. The Lynx’s A12:19 are connected to a [shift register](#shifted). The Game Boy’s A11:15 are unused and the Lynx’s A11 is absent.

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

The original Lynx uses a HC164 shift register to specify address pins A12:19, and the adapter likewise includes a HC164 on the adapter as U2 (instead of replicating the logic in FPGA):

| SR Pin | SR Use | Lynx Pin | Lynx Use | GB Pin | GB Use |
| --- | --- | --- | ------- | --- | --- |
| 1   | A   | 1   | Gnd     | 32  | Gnd |
| 2   | B   | *   | IODAT   | 2   | CLK |
| 3   | QA  | 26  | A12     |     |     |
| 4   | QB  | 25  | A13     |     |     |
| 5   | QC  | 24  | A14     |     |     |
| 6   | QD  | 23  | A15     |     |     |
| 7   | Gnd | 1   | Gnd     | 32  | Gnd |
| 8   | CLK | *   | SYSCTL1 | 5   | /CS |
| 9   | /CLR | 33 | +5V     | 1   | +5V |
| 10  | QE  | 19  | A16     |     |     |
| 11  | QF  | 20  | A17     |     |     |
| 12  | QG  | 21  | A18     |     |     |
| 13  | QH  | 22  | A19     |     |     |
| 14  | VCC | 33  | +5V     | 1   | +5V |

## Unregulated

On a Lynx, pin 34 has an unregulated voltage sourced from the battery. On the Pocket adapter, it is connected to a PNP transistor controlled by CLK. Perhaps the Pocket sets a voltage with C3 and a duty cycle?

| Q1 Pin | Q1 Use | Lynx Pin | Lynx Use |
| --- | --------- | --- | ---------- |
| 1   | Base      | 34  | SWVCC, C3  |
| 2   | Emitter   |     | +5V        |
| 3   | Collector |     | CLK via R4 |
