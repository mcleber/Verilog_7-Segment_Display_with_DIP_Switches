# Controlling a 7-Segment Display with DIP Switches in Verilog

This project is heavily inspired by the “cistern” example from the book Eletrônica Digital, Verilog e FPGA.

## 1. Description

This project implements a BCD (Binary-Coded Decimal) converter that reads DIP switch input and controls a 7-segment display, showing digits 0–8 or ‘E’ for invalid combinations. It offers a hands-on introduction to Verilog development and FPGA pin mapping using the Gowin IDE.

## 2. Repository Structure

- assets/ - Images, schematics and tables

- constraints/ - Pin constraint file

- src/ - Verilog source code

## 3. Bill of Materials

- Tang Primer 20K FPGA (GW2A-LV18PG256C8/I7) with Dock

- 1 Common cathode 7-segment display

- 1 DIP switch (8 positions)

- 7 Current-limiting resistors (~150Ω)

- 8 Pull-down resistors (10kΩ)

- Jumper wires

- 1 Breadboard

- USB-C cable

## 4. Schematic Diagram

Below is the schematic diagram of the circuit used to connect the DIP switches and the display to the FPGA.

![Schematics](https://github.com/mcleber/Verilog_7-Segment_Display_with_DIP_Switches/blob/main/assets/encoder_decoder_bcd_esquematico.png)

## 5. Truth Tables

The developed system operates based on two fundamental truth tables that define the entire behavior of the circuit. The first table establishes the relationship between the DIP switch key combinations and the corresponding decimal values, while the second table determines how these values should be displayed on the display.

![Table.1](https://github.com/mcleber/Verilog_7-Segment_Display_with_DIP_Switches/blob/main/assets/Table1.png)

Outputs from Table 1:

`D3 = HGFEDCBA`

`D2 = H’GFEDCBA + H’G’FEDCBA + H’G’F’EDCBA + H’G’F’E’DCBA`

`D1 = H’GFEDCBA + H’G’FEDCBA + H’G’F’E’D’CBA + H’G’F’E’D’C’BA`

`D0 = H’GFEDCBA + H’G’F’EDCBA + H’G’F’E’D’CBA + H’G’F’E’D’C’B’A`

![Table.2](https://github.com/mcleber/Verilog_7-Segment_Display_with_DIP_Switches/blob/main/assets/Table2.png)

These tables serve as essential references both for the Verilog code implementation and for the practical verification of the circuit.

## 6. Verilog Code and Constraints

 Available in the `src` and `constraints` directories.

## 7. Common Errors and Solutions

During development, I encountered some practical issues that may occur with any beginner:

`Incorrect use of reserved pins:` During signal mapping, an SPI-dedicated pin was incorrectly assigned to the display LEDs, triggering a ‘cannot be placed according to constraint’ synthesis error. The issue was resolved by reassigning the connection to an available GPIO pin, following the Dock’s pinout documentation.

`Reversed wiring on the display:` One of the segment wires was connected incorrectly, causing incorrect numbers to be displayed. After reviewing the segment order (a–g), I corrected the connections, and the display started working correctly.

## 8. Results

The GIF below demonstrates the circuit operation. As the DIP switches are progressively activated, the display shows the corresponding decimal value. When all switches are on, it displays ‘8’. Invalid combinations trigger ‘E’ to indicate an input error.

![circuit operation](https://github.com/mcleber/Verilog_7-Segment_Display_with_DIP_Switches/blob/main/assets/gif_display.gif)

## 9. Conclusion

This project is a great introduction to the interaction between programmable digital logic and external peripherals. It reinforces fundamental Verilog concepts such as input decoding, display control, and FPGA pin mapping.

## 10. Technologies Used

- FPGA: Sipeed Tang Primer 20K (GW2A-LV18PG256C8/I7) with Dock

- HDL: Verilog

- Development Tool: Gowin IDE

- Schematic Design: KiCAD
