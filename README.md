# Adaptive Smart Navigation Robot (STM32F407VG)

This is a smart obstacle-avoiding robot built using the STM32F407VG microcontroller. It uses three ultrasonic sensors to measure distance and avoid obstacles by deciding whether to move forward, reverse, or turn. The robot also gives audio and visual alerts when objects are too close.

---

## Features

- Real-time obstacle detection (front, rear-left, and rear-right)
- Adaptive movement: forward, backward, left, right, stop
- PWM motor control using TIM4 (smooth speed adjustment)
- Buzzer and onboard LEDs for obstacle alerts
- Accurate ultrasonic distance measurement using DWT-based microsecond delay
- Modular, clean code (easy to expand or modify)

---

## Hardware Used

- STM32F407VGT6 Development Board  
- L298N Motor Driver  
- 2x DC Motors  
- 3x HC-SR04 Ultrasonic Sensors  
- Buzzer (for audio alerts)  
- LEDs (for visual indication)  
- External battery (7–12V)  
- (Optional) HC-05 Bluetooth Module  

---

## Pin Mapping (STM32)

| Function         | STM32 Pin         |
|------------------|-------------------|
| ENA (Motor A)     | PB7 (TIM4_CH2)    |
| ENB (Motor B)     | PB6 (TIM4_CH1)    |
| IN1 / IN2         | PB1 / PA3         |
| IN3 / IN4         | PB0 / PC4         |
| Front Sensor TRIG | PE11              |
| Front Sensor ECHO | PE9               |
| Left Sensor TRIG  | PD1               |
| Left Sensor ECHO  | PD2               |
| Right Sensor TRIG | PD8               |
| Right Sensor ECHO | PD9               |
| Buzzer            | PC8               |
| LEDs              | PD12–PD15         |

---

## How It Works

1. On power-up, the robot moves forward briefly to initialize the motors.
2. In the main loop:
   - The three ultrasonic sensors measure distances in front and behind.
   - If an obstacle is detected:
     - LEDs and buzzer are activated.
     - The robot decides the best direction to move:
       - If front is blocked: check rear-left and rear-right to decide turn direction.
       - If all sides blocked: reverse.
       - Otherwise: move forward.
   - Motor speed is reduced if an obstacle is nearby, increased if the path is clear.
