# STM32 LED Control Projects (LEDSequencer & CycleControl)

This repository contains two embedded systems projects developed using the **STM32F767ZI Nucleo board** and **STM32CubeIDE**.  
The project focuses on GPIO configuration, LED control, and user button interaction.

## Projects Overview

### 1. LEDSequencer
A basic LED sequencing project where the onboard LEDs (Green, Blue, Red) flash in a defined order.

**Key features:**
- Sequential LED flashing
- GPIO output configuration
- Timing control using `HAL_Delay()`

---

### 2. CycleControl
An interactive LED control project where the **USER button** cycles through LEDs.  
Each button press selects a different LED, and the selected LED blinks continuously.

**Key features:**
- Button-controlled LED cycling
- LED blinking behaviour
- Button debouncing using falling-edge detection
- Clear LED state management using `if-else` logic

---

## Hardware Used
- **Board:** STM32F767ZI Nucleo
- **IDE:** STM32CubeIDE
- **Button:** USER button (PC13, active-low)

### LED Pin Mapping
| LED Color | GPIO Pin |
|---------|----------|
| Green   | PB0      |
| Blue    | PB7      |
| Red     | PB14     |

---

## Button Behaviour
- The USER button is **active-low**
- Logic used:
  - `GPIO_PIN_RESET` → Button pressed
  - `GPIO_PIN_SET` → Button released
- Falling-edge detection ensures **one LED change per press**

---

## Challenges & Fixes

### Challenge 1: Button always reading HIGH
- Cause: The USER button on the Nucleo board uses an external pull-up.
- Fix: Treated the button as **active-low** and adjusted logic accordingly.

### Challenge 2: LEDs behaving incorrectly (all ON or wrong LED)
- Cause: Misunderstanding LED polarity (`SET = ON`, `RESET = OFF`)
- Fix: Explicitly reset all LEDs before enabling the selected LED.

### Challenge 3: Multiple LED changes on a single press
- Cause: Button bouncing / continuous polling
- Fix: Implemented **falling-edge detection** using previous button state tracking.

---

## How to Run the Projects

1. Open **STM32CubeIDE**
2. Import the desired project (`LEDSequencer` or `CycleControl`)
3. Build the project
4. Flash to the STM32F767ZI board
5. Press the USER button (CycleControl) to cycle LEDs

---

## Future Improvements
- Replace polling with **GPIO interrupts**
- Use **hardware timers** instead of `HAL_Delay()`
- Add UART output for debugging
- Extend to RGB LED control or FreeRTOS tasks

---

## Author
Developed as part of hands-on learning in **Embedded Systems and Microcontroller Programming**.
