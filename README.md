#  8051-Based 3-Digit Persistent Counter with I²C EEPROM & 7-Segment Multiplexed Display

This project showcases a **3-digit decimal counter (000–999)** built around the **8051 microcontroller** family, featuring **non-volatile storage** using an external **I²C EEPROM (24C02)** and real-time display on **multiplexed 7-segment displays**. A single **push-button input** increments the counter, which is stored and restored across power cycles.

This is a great demonstration of interfacing EEPROMs via bit-banged I²C, handling display multiplexing using timer interrupts, and creating reliable embedded applications on minimal hardware.

---

## ✨ Features

- 🔢 Counts from **000 to 999**
- 💾 EEPROM-backed **non-volatile storage** (24C02)
- 💡 Multiplexed **3-digit 7-segment display**
- ⏲️ **Timer0-based display refresh**
- 🔘 Push-button controlled counter increment
- 🔄 **Automatic wrap-around** from 999 → 000
- ⚡ **Retains last count** even after power-off

---

## 🧰 Hardware Requirements

| Component         | Description                               |
|------------------|-------------------------------------------|
| **Microcontroller**  | AT89C51 / AT89S52 (8051 core)         |
| **EEPROM**            | 24C02 – I²C compatible EEPROM          |
| **Display**           | 3-digit common cathode 7-segment       |
| **Push Button**       | Active-low digital input               |
| **Resistors**         | Pull-ups and segment current limiting  |
| **Power Supply**      | +5V DC regulated                       |

---

## 🖇️ Pin Mapping

| 8051 Pin | Function                      
|---------------|--------------------------|
| **P1.0–P1.7** | Segment lines (a–g, dp)  |
| **P2.0**      | Digit select – Units     |
| **P2.1**      | Digit select – Tens      |
| **P2.2**      | Digit select – Hundreds  |
| **P0.0**      | I²C SDA (EEPROM Data)    |
| **P0.1**      | I²C SCL (EEPROM Clock)   |
| **P0.7**      | Push Button (Active-Low) |

> 💡 **Note**: Bit-banged I²C is implemented in software using P0.0 and P0.1.

---

## ⚙️ Functional Overview

### 1. **Startup**
- Reads last saved count from EEPROM address `0x00`
- Defaults to `000` if uninitialized

### 2. **Display Refresh**
- **Timer0** interrupts refresh each digit in sequence (multiplexing)
- Smooth display output using persistence of vision

### 3. **Button Press Detection**
- On press, counter:
  - Increments by 1
  - Wraps from 999 → 000
  - Saves new value to EEPROM

### 4. **Power-Off Safety**
- Counter value persists through reboots using EEPROM

---

## ⏱️ Timer Configuration

- **Timer Used**: Timer0  
- **Mode**: Mode 1 (16-bit timer)  
- **Purpose**: Digit refresh/multiplexing via interrupts

---

## 📦 EEPROM Storage Format

| EEPROM Address | Data Description       |
|----------------|------------------------|
| `0x00`         | Counter value (0–255)  |

> Currently using a single byte; easily extendable to 2 bytes for full 000–999 range.

---

## 🧪 Example Behavior

1. Power on → loads last count from EEPROM
2. Button press → increments and updates EEPROM
3. Reaches 999 → wraps to 000
4. Power cycle → resumes from last saved count

---

## 💡 Use Cases

- 🧪 Embedded systems lab demonstration
- 🏭 Simple digital production counter
- 🎓 Educational example for EEPROM & timers
- 🛠️ DIY electronics scoreboard or tally system

---

## 👨‍💻 Author

**MANISHA S**  


📁 Project: *I²C EEPROM-Backed 8051 Counter with Multiplexed 7-Segment Display*  
🔗 *Feel free to fork, contribute, or report issues!*
