# Part Counter with Analog Safety Override (RSLogix 500)

This project simulates a real-world control system where a motor starts only after detecting three distinct part arrivals, and only if analog pressure is below a safe threshold. The program uses a modular, structured ladder logic approach in RSLogix 500 with separate sections for digital I/O, analog scaling, and main control logic.

## 🧠 Core Concepts Demonstrated

- `CTU` (Count Up) with part detection trigger
- `ONS` (One-Shot) to prevent scan-based double-counts
- `SCP` (Scale with Parameters) to convert raw analog to engineering units (PSI)
- `LES` / `GRT` to monitor pressure thresholds
- Digital memory bits (`B3`) for interlocking, output control, and override flags
- Reset logic for system recovery
- Unsafe condition visual indicator
- Pressure override to prevent motor operation under unsafe analog conditions

---

## 🧾 System Description

###  Inputs
| Tag | Description |
|-----|-------------|
| `B3:0/0` | Simulated Part Sensor Pulse |
| `B3:0/4` | Analog Override (Unsafe Pressure Bit) |
| `F8:0` | Scaled Analog Pressure Value (PSI) |

###  Outputs
| Tag | Description |
|-----|-------------|
| `B3:0/2` | Motor Enable Output |
| `B3:0/6` | Motor Trigger (latched when 3 parts arrive) |
| `B3:0/7` | Unsafe Pressure Indicator |

### 📸 System States to Document
Resting State

Counter = 0, pressure is safe, motor is OFF, no unsafe light

Parts Detected (1 or 2)

Counter incrementing, motor not yet triggered

3rd Part Reached, Pressure Safe

C5:0/DN goes true → triggers motor latch → motor output ON

Pressure Unsafe

F8:0 > 4.5 → unsafe pressure bit ON → motor OFF or blocked

Reset / System Clear

Manual reset rung deactivates system and prepares for next batch

### 💡 Real-World Applications
Batch part handling or feeder logic

Interlocked conveyor systems

Pressure-controlled valve/motor activation

Industrial motor logic where analog safety is required

### 🛠 Tools Used
RSLogix Micro Starter Lite

RSLinx Classic

RSLogix Emulate 500
