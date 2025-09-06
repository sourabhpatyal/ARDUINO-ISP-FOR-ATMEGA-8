# Arduino Code Flashing on ATmega8A

This repository explains how to **flash Arduino sketches onto an ATmega8A microcontroller**, either with or without a bootloader.

---

## 🔧 Hardware Requirements
- ATmega8A microcontroller (DIP-28 or TQFP)
- USBasp programmer **or** Arduino UNO as ISP
- Optional: USB-to-TTL adapter (for uploading code after bootloader)
- 16 MHz crystal + 22pF capacitors (if using external crystal)
- Jumper wires, breadboard, power supply (5V)

---

## 📌 Pin Connections (ISP Programming)

| ATmega8A Pin | Function | Programmer Pin |
|--------------|----------|----------------|
| Pin 7, 20    | VCC      | +5V            |
| Pin 8, 22    | GND      | GND            |
| Pin 1        | RESET    | RESET          |
| Pin 17       | MOSI     | MOSI           |
| Pin 18       | MISO     | MISO           |
| Pin 19       | SCK      | SCK            |

👉 If using external clock: connect **Pin 9 & 10** to 16MHz crystal + capacitors.

---

## 🚀 Flashing Bootloader (Arduino IDE)
1. Install [MiniCore](https://github.com/MCUdude/MiniCore) in Arduino IDE Boards Manager.
2. Select:
   - **Board**: ATmega8
   - **Clock**: Internal 8 MHz (or 16 MHz if using external crystal)
   - **Programmer**: USBasp (or Arduino as ISP)
3. Click **Tools → Burn Bootloader**.

---

## 💻 Uploading Arduino Sketch
- After bootloader is installed, connect via USB-to-TTL adapter:

| USB-to-TTL | ATmega8A Pin |
|------------|--------------|
| TXD        | Pin 2 (RXD)  |
| RXD        | Pin 3 (TXD)  |
| GND        | GND          |
| VCC        | +5V          |
| DTR        | RESET (via 100nF capacitor) |

Then upload sketches directly from Arduino IDE.

---

## 🖥️ Uploading Without Bootloader (Direct HEX Flash)
You can also upload compiled code without bootloader using **avrdude**:

```bash
avrdude -c usbasp -p atmega8 -U flash:w:sketch.hex
