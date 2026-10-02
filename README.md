# Basic Actuator Control
## Circuit Diagram
<img width="810" height="601" alt="image" src="https://github.com/user-attachments/assets/4bdcfbf6-4c20-42aa-9e25-450335961090" />


```text
                 ┌──────────────────────┐
                 │        ESP32         │
                 │                      │
                 │ GPIO 21 ─────────────┼─────────► IN1
                 │ GPIO 22 ─────────────┼─────────► IN2
                 │ GPIO 23 ◄────────────┼────────── Button
                 │ GND ─────────────────┼─────┐
                 └──────────────────────┘     │
                                              │
                                              ▼
                              ┌────────────────────────┐
                              │     L298N DRIVER       │
                              │                        │
                    5V  ─────►│ 5V                     │
                    GND ─────►│ GND                    │
                              │                        │
               GPIO 21 ──────►│ IN1                    │
               GPIO 22 ──────►│ IN2                    │
                              │                        │
                    +V  ─────►│ 12V / VS               │
                              │                        │
                              │ OUT1 ──────────┐       │
                              │ OUT2 ──────────┤       │
                              └────────────────┼───────┘
                                               │
                                               ▼
                                      ┌────────────────┐
                                      │    DC MOTOR    │
                                      │                │
                                      │ OUT1 ◄─────────┤
                                      │ OUT2 ◄─────────┤
                                      └────────────────┘


                    ┌──────────────────┐
                    │    PUSH BUTTON   │
                    │                  │
              GND ──┤                  ├── GPIO 23
                    └──────────────────┘
                         Active LOW
                    INPUT_PULLUP enabled

```
## Demo 




https://github.com/user-attachments/assets/af2f071d-1197-4d56-805f-9442403ed36f





The DC motor was controlled using an L298N motor driver connected to the ESP32. GPIO 21 and GPIO 22 were used as the motor control inputs, while GPIO 23 was used for the push button with the ESP32's internal pull-up resistor.

When the button is pressed, GPIO 23 reads LOW, causing GPIO 21 to become HIGH while GPIO 22 remains LOW. This makes the motor rotate in one direction. When the button is released, both motor control signals are LOW and the motor stops.

The point where the motor starts rotating was determined through actual hardware testing. Therefore, the motor's rotation onset is considered a measured experimental result rather than a value taken from the datasheet. The motor supply voltage and the observed behavior were recorded during testing.

## References
L298N (HW-095): https://www.handsontec.com/dataspecs/L298N%20Motor%20Driver.pdf

Miniature 3V DC Motor: https://quartzcomponents.com/products/miniature-dc-motor
