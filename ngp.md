# AP-A02 Neo Geo Pocket Adapter

## Power

The following pins are connected to +3.3V or ground:

| NGP Pin | NGP Use |
| --- | --- |
| 1   | Gnd |
| 19  | +3.3V |

## Control

The Game Boy’s control pins are connected as follows:

| GB Pin | GB Use | NGP Pin | NGP Use |
| --- | --- | --- | --- |
| 5   | /CS | 33  | /CE |
| 4   | /RD | 32  | /OE |
| 3   | /WR | 18  | /WE |
| 2   | CLK |     | Latch |
| 30  | /RST | 34 | ?   |
| 31  | AUD |     | nc  |

The clock pin is used to [latch](#latched) address pins in order to access higher memory addresses.

## Address

The Game Boy’s 16 address pins are connected to the corresponding NGP pins in order, and 5 additional address pins are [latched](#latched) from a flip-flop.

| GB Pin | GB Use | NGP Pin | NGP Use |
| --- | --- | --- | --- |
| 6   | A0  | 35  | A0  |
| 7   | A1  | 27  | A1  |
| 8   | A2  | 26  | A2  |
| 9   | A3  | 25  | A3  |
| 10  | A4  | 24  | A4  |
| 11  | A5  | 23  | A5  |
| 12  | A6  | 22  | A6  |
| 13  | A7  | 21  | A7  |
| 14  | A8  | 17  | A8  |
| 15  | A9  | 16  | A9  |
| 16  | A10 | 5   | A10 |
| 17  | A11 | 15  | A11 |
| 18  | A12 | 14  | A12 |
| 19  | A13 | 13  | A13 |
| 20  | A14 | 12  | A14 |
| 21  | A15 | 11  | A15 |
|     |     | 10  | A16 |
|     |     | 2   | A17 |
|     |     | 20  | A18 |
|     |     | 4   | A19 |
|     |     | 3   | A20 |

## Data

The Game Boy’s 8 data pins are connected to the corresponding NGP pins in order:

| GB Pin | GB Use | NGP Pin | NGP Use |
| --- | --- | --- | --- |
| 22  | D0  | 31  | D0  |
| 23  | D1  | 30  | D1  |
| 24  | D2  | 29  | D2  |
| 25  | D3  | 28  | D3  |
| 26  | D4  | 9   | D4  |
| 27  | D5  | 8   | D5  |
| 28  | D6  | 7   | D6  |
| 29  | D7  | 6   | D7  |

## Latched

Because the Game Boy has fewer address pins (16) than the Neo Geo Pocket (21), the adapter includes an LC374A octal flip-flop. The flip-flop latches address pins A1:5 on a positive CLK edge and provdes them as A16:20. Three outputs are unused and their inputs pulled high:

| FF Pin | FF Use | NGP Pin | NGP Use |
| --- | --- | --- | --- |
| 1   | /OE | 1   | Gnd |
| 2   | 1Q  | 20  | A18 |
| 3   | 1D  | 25  | A3  |
| 4   | 2D  | 27  | A1  |
| 5   | 2Q  | 10  | A16 |
| 6   | 3Q  | 4   | A19 |
| 7   | 3D  | 24  | A4  |
| 8   | 4D  | 23  | A5  |
| 9   | 4Q  | 3   | A20 |
| 10  | Gnd | 1   | Gnd |
| 11  | CLK | *   | CLK |
| 12  | 5Q  | 2   | A17 |
| 13  | 5D  | 26  | A2  |
| 14  | 6D  | 19  | +5V |
| 15  | 6Q  |     | nc  |
| 16  | 7Q  |     | nc  |
| 17  | 7D  | 19  | +5V |
| 18  | 8D  | 19  | +5V |
| 19  | 8Q  |     | nc  |
| 20  | VCC | 19  | +5V |

## Unused

One pin on the NGP cartridge is unused:

| NGP Pin | NGP Use |
| --- | --- |
| 36  | nc  |
