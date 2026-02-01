The Arduino code controls a two-motor line-following robot using two IR sensors. The sensors detect the line by reading digital signals: LOW means the sensor is over the black line, and HIGH means it is over the white surface.
The program continuously reads the sensor inputs in the loop() function and decides how to move the motors:
Go straight if both sensors detect the line (LOW).
Turn left if only the front sensor detects white (HIGH) and the left sensor detects the line (LOW).
Turn right if only the left sensor detects white (HIGH) and the front sensor detects the line (LOW).
If both sensors detect white (HIGH), the robot turns in the last direction it turned (left or right) to try and find the line again. If no previous turn is recorded, the robot stops.
Motor control is handled using digital outputs to set motor direction and PWM signals to control speed. The goStraight(), turnLeft(), turnRight(), and stopMotors() functions encapsulate these motor commands for clarity and reusability.
The lastTurn variable stores the most recent turn direction, enabling the robot to make intelligent decisions when it temporarily loses track of the line.
