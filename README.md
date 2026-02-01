Overview:
This project is a simple line-following robot built using an Arduino Uno, two infrared (IR) sensors, and two DC motors controlled by an H-bridge motor driver. The robot detects a black line on a white surface and follows it autonomously by adjusting motor speeds and directions.

Components and Pin Connections:
Front IR Sensor (senseF)	Digital Pin 2	Input
Left IR Sensor (senseL)	Digital Pin 4	Input
Motor 1 PWM Control (pwmF)	PWM Pin 5	Output
Motor 2 PWM Control (pwmL)	PWM Pin 6	Output
Motor 2 Forward (mtrTwoF)	Digital Pin 8	Output
Motor 2 Backward (mtrTwoL)	Digital Pin 7	Output
Motor 1 Forward (mtrOneF)	Digital Pin 13	Output
Motor 1 Backward (mtrOneL)	Digital Pin 12	Output

How It Works:
The robot uses two IR sensors to detect the line.
Sensor reading LOW means the sensor is over the black line.
Sensor reading HIGH means the sensor is over the white surface (no line).
The Arduino reads the sensors continuously and decides how to move:
Go Straight: Both sensors detect the line (LOW).
Turn Left: Front sensor detects white (HIGH), left sensor detects line (LOW).
Turn Right: Left sensor detects white (HIGH), front sensor detects line (LOW).
Search for Line: Both sensors detect white (HIGH), the robot turns in the last known direction to relocate the line. If no last direction, it stops.
Motor directions and speeds are controlled by digital outputs and PWM signals.
The lastTurn variable tracks the last turning direction for better handling when the line is lost.

Code:
The Arduino code controls a two-motor line-following robot using two IR sensors. The sensors detect the line by reading digital signals: LOW means the sensor is over the black line, and HIGH means it is over the white surface.
The program continuously reads the sensor inputs in the loop() function and decides how to move the motors:
Go straight if both sensors detect the line (LOW).
Turn left if only the front sensor detects white (HIGH) and the left sensor detects the line (LOW).
Turn right if only the left sensor detects white (HIGH) and the front sensor detects the line (LOW).
If both sensors detect white (HIGH), the robot turns in the last direction it turned (left or right) to try to find the line again. If no previous turn is recorded, the robot stops.
Motor control is handled using digital outputs to set motor direction and PWM signals to control speed. The goStraight(), turnLeft(), turnRight(), and stopMotors() functions encapsulate these motor commands for clarity and reusability.
The lastTurn variable stores the most recent turn direction, enabling the robot to make intelligent decisions when it temporarily loses track of the line.
