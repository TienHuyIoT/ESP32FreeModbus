# Modbus Data Model: Coils, Inputs, and Registers

Modbus organizes device data into **four main parameter types**.  
Each type has its own address range and access rules.  

---

## 1. Coils (`0xxxx`)
- **Type**: Discrete **output** (1 bit)  
- **Access**: Read/Write  
- **Function Codes**:
  - `0x01` → Read Coils  
  - `0x05` → Write Single Coil  
  - `0x0F` → Write Multiple Coils  
- **Example**: Turn ON/OFF a motor, relay, or lamp  

---

## 2. Discrete Inputs (`1xxxx`)
- **Type**: Discrete **input** (1 bit)  
- **Access**: **Read-only**  
- **Function Codes**:
  - `0x02` → Read Discrete Inputs  
- **Example**: Read status of a switch, push button, or contact  

---

## 3. Input Registers (`3xxxx`)
- **Type**: 16-bit **input register** (word)  
- **Access**: **Read-only**  
- **Function Codes**:
  - `0x04` → Read Input Registers  
- **Example**: Sensor values (temperature, voltage, current)  

---

## 4. Holding Registers (`4xxxx`)
- **Type**: 16-bit **general-purpose register** (word)  
- **Access**: Read/Write  
- **Function Codes**:
  - `0x03` → Read Holding Registers  
  - `0x06` → Write Single Register  
  - `0x10` → Write Multiple Registers  
- **Example**: Store configuration parameters, setpoints, calibration data  

---

## 📌 Summary Table

| Type                | Address Range | Size   | Access   | Typical Use                     |
|---------------------|---------------|--------|----------|---------------------------------|
| **Coils**           | `0xxxx`       | 1 bit  | R/W      | Control outputs (relay, lamp)   |
| **Discrete Inputs** | `1xxxx`       | 1 bit  | Read     | Status of switch, button        |
| **Input Registers** | `3xxxx`       | 16-bit | Read     | Sensor values (temperature, V)  |
| **Holding Registers** | `4xxxx`     | 16-bit | R/W      | Config & data storage           |

---

## 🗂️ Memory Map Diagram (Table)

```
+---------------------+---------------+-----------+-----------------------------+
| Type                | Address Range | Size      | Access                      |
+---------------------+---------------+-----------+-----------------------------+
| Coils               | 00001 - 09999 | 1 bit     | Read / Write (Outputs)      |
| Discrete Inputs     | 10001 - 19999 | 1 bit     | Read Only (Inputs)          |
| Input Registers     | 30001 - 39999 | 16-bit    | Read Only (Analog Inputs)   |
| Holding Registers   | 40001 - 49999 | 16-bit    | Read / Write (Parameters)   |
+---------------------+---------------+-----------+-----------------------------+
```

---

## 🧩 Memory Layout (ASCII Block Diagram)

```
+-----------------------------+
| 0xxxx - Coils               |
| (Discrete Outputs, 1 bit)   |
| Access: Read / Write        |
+-----------------------------+
| 1xxxx - Discrete Inputs     |
| (Digital Inputs, 1 bit)     |
| Access: Read Only           |
+-----------------------------+
| 3xxxx - Input Registers     |
| (Analog Inputs, 16-bit)     |
| Access: Read Only           |
+-----------------------------+
| 4xxxx - Holding Registers   |
| (Config / Data, 16-bit)     |
| Access: Read / Write        |
+-----------------------------+
```

---

## 🔎 Note on Addressing
- In documentation, addresses often start at **1** (e.g., `40001`).  
- In Modbus protocol messages, addresses start at **0**.  
  - Example: `40001` (doc) → `0x0000` (message).  
  - Example: `40010` (doc) → `0x0009` (message).  

