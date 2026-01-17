# Low Power Fitness Tracker
### A Solar-Powered, Ultra-Low-Power Fitness Tracker

## Introduction

The **Low Power Rangers Fitness Tracker** is a wearable embedded systems project focused on pushing the limits of **energy-efficient design**. The goal was simple but ambitious: build a fitness tracker that minimizes reliance on USB charging by intelligently managing power and harvesting energy from a solar source.

Built around the **EFR32BG13** SoC, the system integrates motion tracking, heart-rate monitoring, BLE communication, and display control—while aggressively leveraging low-power modes. Every design decision, from hardware selection to firmware architecture, was guided by power budgeting, current profiling, and real-world measurements.

This project demonstrates a full **hardware–firmware co-design workflow**, emphasizing sustainable embedded systems and real-world validation rather than theoretical estimates.

---

## System Architecture & Power-Aware State Flow

At the core of the tracker is a **power-aware firmware architecture**, where system behavior adapts dynamically based on activity, connectivity, and energy availability. Rather than remaining fully active, the system transitions between operating modes to conserve energy whenever possible.

### High-Level State Flow
BOOT → IDLE / SLEEP →
SENSOR_ACQUIRE →
BLE_EVENT →
DATA_UPDATE →
LOW_POWER_MODE → IDLE


### State Breakdown

- **BOOT**  
  The system initializes hardware peripherals, sensors, power rails, and BLE stack while measuring boot-time current consumption.

- **IDLE / SLEEP**  
  The default low-power state. The MCU enters deep sleep while waiting for interrupts from sensors, BLE events, or scheduled wake-ups.

- **SENSOR_ACQUIRE**  
  Motion data from the IMU and heart-rate data are sampled using interrupt-driven, low-duty-cycle sensing to minimize active time.

- **BLE_EVENT**  
  Handles BLE advertising, connection, disconnection, and data transmission events. Current spikes during RF activity are carefully profiled and optimized.

- **DATA_UPDATE**  
  Processed sensor data is prepared for display or transmission while keeping CPU active time as short as possible.

- **LOW_POWER_MODE**  
  After completing active tasks, the system aggressively returns to low-power operation, disabling unused peripherals and clocks.

This structured flow ensures that **high-current events are brief, controlled, and measurable**, enabling long battery life even with frequent BLE activity and sensor updates.

---

## Key Design Focus

- Ultra-low-power operation using MCU sleep modes  
- Real-world current profiling across BLE states  
- Interrupt-driven sensor acquisition  
- Power-aware firmware architecture  
- Solar-assisted battery charging and management  




