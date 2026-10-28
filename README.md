# stm32-f103-can-node

CAN node on an STM32F103 (Blue Pill) that measures its internal temperature
and broadcasts it on a CAN bus once per second.

It is the transmitter side of the
[stm32-can-bus-sniffer](https://github.com/trangonameless/stm32-can-bus-sniffer) project,
where an STM32L476 receives the frames and forwards them over UART.

## Hardware
- STM32F103 board (Blue Pill), programmed with an ST-Link V2
- 3.3 V CAN transceiver SN65HVD230 
- 120 Ω termination resistors at both ends of the bus

| MCU pin | Transceiver |
|---------|-------------|
| PA12 (CAN_TX) | TXD |
| PA11 (CAN_RX) | RXD |
| 3V3 / GND     | VCC / GND (Rs/S pin to GND) |

CAN-H and CAN-L go to the other node. Grounds of all boards must be common.

## CAN frame

| CAN ID | DLC | Bytes 0-1                                   | Byte 2        |
|--------|-----|---------------------------------------------|---------------|
| 0x100  | 3   | Temperature in 0.1 °C, int16, little-endian | Frame counter |

Example: `2D 01 14` means 0x012D = 301 → 30.1 °C, frame number 20.

## License
MIT
