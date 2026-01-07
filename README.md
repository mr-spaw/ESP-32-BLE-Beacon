
# ESP-32 BLE Beacon (Arduino Core 3.0.7 Compatible)

This project demonstrates how to configure an **ESP32** as a **Bluetooth Low Energy (BLE) Beacon** using the **ESP32 Arduino Core v3.0.7**.

Unlike many legacy BLE examples found online, this implementation is **fully compatible with newer ESP32 Arduino Core versions**, where several BLE demo codes fail due to API and type changes.

---

## 📡 What is a BLE Beacon?

A BLE beacon continuously broadcasts a small packet of data that nearby BLE-enabled devices (phones, scanners, gateways) can detect **without pairing**.

Common use cases:

* Indoor navigation
* Proximity marketing
* Asset tracking
* Attendance & access systems
* Smart automation triggers

---

## Problem Solved!!

Many popular ESP32 BLE beacon examples were written for **older Arduino cores (≤2.x)**.
With **Arduino Core 3.x**, these examples often fail to compile due to:

* Stricter C++ type checking
* Internal BLE API changes
* Mixing of `std::string` and Arduino `String`

This repository provides:

* A **working BLE Beacon example**
* Tested on **ESP32 Arduino Core 3.0.7**
* Clean, minimal, and future-proof code
* No deprecated or broken APIs

---

## Tested Environment

| Component    | Version                             |
| ------------ | ----------------------------------- |
| Board        | ESP32                               |
| Arduino Core | **3.0.7**                           |
| Compiler     | GCC 12.x                            |
| BLE Stack    | ESP32 BLE Arduino (core-integrated) |

---

## Common Compilation Error (Explained)

When compiling older BLE beacon code on Arduino Core **3.0.7**, you may encounter errors like:

```text
error: no match for 'operator+=' (operand types are 'std::string' and 'String')
error: cannot convert 'std::string' to 'String'
```

### Root Cause

* `BLEBeacon::getData()` now returns an **Arduino `String`**
* Many examples incorrectly use `std::string`
* Arduino Core 3.x **does NOT implicitly convert** between these types

This breaks code such as:

```cpp
std::string strServiceData;
strServiceData += oBeacon.getData();   // Compilation error
```

---

## Solution Used 

This implementation **uses Arduino `String` consistently**, which matches the BLE API expectations in Core 3.0.7:

```cpp
String serviceData;
serviceData += oBeacon.getData();
advertisementData.addData(serviceData);
```

✔ No implicit conversions
✔ No STL / Arduino string mixing
✔ Fully compatible with new toolchains

---

## Key Implementation Details

* Uses **BLE Beacon advertising mode**
* Manually constructs advertisement payload
* Avoids deprecated BLE APIs
* Safe memory handling
* Clean initialization and advertising start

---

## How to Use

1. Install **ESP32 Arduino Core v3.0.7**
2. Open the sketch in Arduino IDE
3. Select your ESP32 board
4. Compile and upload
5. Scan using:

   * nRF Connect
   * LightBlue
   * Any BLE scanner app

---

## Expected Output

* ESP32 appears as a **BLE Beacon**
* Advertisement packets visible without pairing
* Stable broadcasting interval
* No runtime crashes or watchdog resets

---

