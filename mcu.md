# MCU Unidentified Microcontroller

All adapters have an IC on a SOT-23-6 footprint, likely a PIC10 (PIC10F20X) or possibly an AVR (ATTINY) microcontroller. It is connected to a LED on the back of the adapter which can be seen by a sensor in the Pocket. This likely serves as a side-channel to identify which adapter is inserted.

## Edge connector

The microcontroller is connected to a 6-pin edge connector on the back of the adapter. The connector is inaccessible while the adapter PCB is inside its enclosure. With an enclosure that allowed the board to be flipped, the connector would align with pins 14-19 (A8:13) of a Game Boy cartridge connector.

| Pin | Use | PICKit  |
| --- | --- | ------- |
| 1   | nc  | VPP     |
| 2   | VCC | VCC     |
| 3   | X0  | Gnd     |
| 4   | X1  | ICSPDAT |
| 5   | X2  | ICSPCLK |
| 6   | X3  | LVP     |

## Microcontroller

| Pin | Use | PIC         | AVR |
| --- | --- | ----------- | --- |
| 1   | X1  | GP0/ICSPDAT | PB0 |
| 2   | X0  | Gnd         | Gnd |
| 3   | X2  | GP1/ICSPCLK | PB1 |
| 4   | LED | GP2         | PB2 |
| 5   | VCC | VCC         | VCC |
| 6   | X3  | GP3         | PB3 |

## Protocol

The microcontroller outputs data as on pin 4 pulses at 14 kHz. Pulses are either short (~70us high, then ~70us low) or long (~140us high, then ~140us low). Data seems to be sent in packets of 48 pulses: first 16 short pulses, then 8 pulses alternating between long and short, then 24 varying outputs. Assuming short pulses are 0 and and long pulses are 1, I observed the following sequence from the Game Gear adapter:
```
$0000AA05A028
$0000AA07409C
$0000AA0680F7
```
