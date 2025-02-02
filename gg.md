# AP-A01 Game Gear Adapter

## Power

The following pins are connected to ground:

| GG Pin | GG Use |
| --- | --- |
| 16  | Gnd |
| 17  | Gnd |
| 18  | Gnd |
| 41  | Gnd |

The following pins are connected to +5V, either to provide power or where features are not supported by the Pocket:

| GG Pin | GG Use |
| --- | --- |
| 2   | +5V |
| 35  | +5V |
| 36  | /M1 |
| 38  | /Refresh |
| 40  | CLK |

## Control

The Game Boy’s control pins are connected as follows:

| GB Pin | GB Use | GG Pin | GG Use |
| --- | --- | --- | --- |
| 5   | /CS | 24  | /CE |
| 4   | /RD | 26  | /RD |
| 3   | /WR | 3   | /WR |
| 2   | CLK | 37  | /IOReq |
| 30  | /RST | 39 | /RST |
| 31  | AUD | 42  | /GG |

When /GG (AUD) is pulled low, the cartridge plays in Game Gear mode; when high, it plays in Master System mode.

## Address

The address pins are connected in the physical order that they appear on the cartridge, rather than the logical order. Game Boy address pins are in ascending order, left-to-right, but Game Gear pins are shuffled:

| GB Pin | GB Use | GG Pin | GG Use |
| --- | --- | --- | --- |
| 6   | A0  | 4   | A12 |
| 7   | A1  | 5   | A7  |
| 8   | A2  | 6   | A6  |
| 9   | A3  | 7   | A5  |
| 10  | A4  | 8   | A4  |
| 11  | A5  | 9   | A3  |
| 12  | A6  | 10  | A2  |
| 13  | A7  | 11  | A1  |
| 14  | A8  | 12  | A0  |
| 15  | A9  | 25  | A10 |
| 16  | A10 | 28  | A15 |
| 17  | A11 | 29  | A11 |
| 18  | A12 | 30  | A9  |
| 19  | A13 | 31  | A8  |
| 20  | A14 | 32  | A13 |
| 21  | A15 | 33  | A14 |

## Data

Unlike the address pins, the data pins are lined up in matching order on Game Boy and Game Gear cartridges, and are connected accordingly:

| GB Pin | GB Use | GG Pin | GG Use |
| --- | --- | --- | --- |
| 22  | D0  | 13  | D0  |
| 23  | D1  | 14  | D1  |
| 24  | D2  | 15  | D2  |
| 25  | D3  | 19  | D3  |
| 26  | D4  | 20  | D4  |
| 27  | D5  | 21  | D5  |
| 28  | D6  | 22  | D6  |
| 29  | D7  | 23  | D7  |

## Generated

In order to provide the /M0-7 (pin 27) and /M8-B (pin 34) signals to the cartridge, the adapter uses a HC139, a dual 2:4 demux. These signals are purely for the convenience of the cartridge, and can be generated from other signals on the Game Gear cartridge connector:

| Demux Pin | Demux Use | GG Pin | GG Use |
| --- | --- | --- | --- |
| 1   | 1/G | 24  | /CS |
| 2   | 1A  | 33  | A14 |
| 3   | 1B  | 28  | A15 |
| 4   | 1Y0 |     | nc  |
| 5   | 1Y1 |     | nc  |
| 6   | 1Y2 | 34  | /M8-13 |
| 7   | 1Y3 |     | nc  |
| 8   | Gnd |     | Gnd |
| 9   | 2/G |     | nc  |
| 10  | 2A  |     | nc  |
| 11  | 2B  |     | nc  |
| 12  | 2Y0 | 27  | /M0-7 |
| 13  | 2Y1 |     | Gnd |
| 14  | 2Y2 | 28  | A15 |
| 15  | 2Y3 | 24  | /CS |
| 16  | VCC |     | +5V |

## TV

The Game Gear TV pins are unconnected:

| GG Pin | GG Use |
| --- | --- |
| 1   | +34V |
| 43  | /TV |
| 44  | TV Right Audio |
| 45  | TV Left Audio |
