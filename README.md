# PLC-Controlled Automatic Car Wash System

## 1. Overview

This project outlines the design and logic for an automatic car wash system controlled by a Programmable Logic Controller (PLC). The system executes a predefined sequence of operations including water spraying, detergent dispensing, brushing, steam application, and drying. The control logic is based on sensor inputs and timed operations to ensure a complete car wash cycle.

This project was developed as part of the Industrial Automation Systems Lab I coursework at the Department of Control and Automation Engineering, Yıldız Technical University.

## 2. System Operation Sequence

The car wash process follows these sequential steps:

1.  **Car Entry & Initial Water Spray:**
    * `Sensor 1` detects a car entering the washing area.
    * After a 3-second delay, the water spray system (`Washing` output) activates.

2.  **Detergent Dispensing:**
    * 4 seconds after the water spray starts, the detergent dispensing system is activated.
    * The water spray system (`Washing` output) continues to operate alongside the detergent.

3.  **Brushing Cycle:**
    * The detergent system stops after 5 seconds of operation.
    * Simultaneously, the 3-way brushing system starts:
        * The brush motor moves forward (`Motor Forward` output).
    * When `Sensor 3` (end of car) is detected by a sensor moving with the brush system, the brush motor reverses (`Motor Backward` output).
    * The brushes return to their starting position, detected by `Sensor 4` (original location of scrubbing mechanism).

4.  **Hot Steam Application:**
    * Once brushes are back at the starting point (`Sensor 4` active), the water spray (`Washing` output) is turned off.
    * The hot steam sending output is activated.

5.  **Drying Cycle:**
    * After 5 seconds of steaming, the drying motor (`Drying` output) is activated.
    * The `Washing` output remains off, but the `Drying` output is now continuously active.

6.  **Cycle Completion & System Ready:**
    * The drying system operates for 8 seconds.
    * When the drying system deactivates, all systems reset.
    * The `Ready` output becomes true, indicating the system is ready for a new car (this is active when no car is detected in the area, likely meaning `Sensor 1` and `Sensor 2` are off).

## 3. Inputs and Outputs

### Inputs (Digital Inputs - DI):
* **DI 1: Sensor 1:** Detects car entering the wash area.
* **DI 2: Sensor 2:** Detects car exiting the wash area. (Used to determine if the area is clear for the `Ready` state).
* **DI 3: Sensor 3:** Detects the end of the car for the brushing mechanism.
* **DI 4: Sensor 4:** Detects the original/home position of the scrubbing/brushing mechanism.

### Outputs (Digital Outputs - DO):
* **DO 1: Washing:** Controls the water spray and detergent mix (active from initial spray until steaming starts).
* **DO 2: Drying:** Controls the drying fan (active from steaming until the end of the drying cycle).
* **DO 3: Ready:** Indicates the system is idle and ready for a new car.
* **DO 4: Motor Forward:** Drives the brushing system forward.
* **DO 5: Motor Backward:** Drives the brushing system backward.
* **DO 6: Detergent:** Dispensing detergent.

## 4. Software and Hardware

* **Software:** Developed using `Phoenix Contact PC Worx 6.30.3146`
* **Hardware:** Designed for a generic PLC system with the specified digital inputs and outputs.

## 5. Repository Contents

* **`Car Wash.pdf`**
* **`README.md`**

## 6. Author

* Halil Onur Tutar
