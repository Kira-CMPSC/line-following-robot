// Initial Code 
int senseL = 4;
int pwmF = 5;
int pwmL = 6;
int mtrTwoF = 8;
int mtrTwoL = 7;
int mtrOneF = 13;
int mtrOneL = 12;
int speed = 200;
void setup(){
	pinMode(senseF, INPUT);
	pinMode(senseL, INPUT);
	pinMode(pwmF, OUTPUT);
	pinMode(pwmL, OUTPUT);
	pinMode(mtrTwoF, OUTPUT);
	pinMode(mtrTwoL, OUTPUT);
	pinMode(mtrFirstF, OUTPUT);
	pinMode(mtrFirstL, OUTPUT);
}

void goStraight(){
		digitalWrite(mtrOneF, HIGH);
		digitalWrite(mtrTwoF, HIGH);
		digitalWrite(mtrOneL, LOW);
		digitalWrite(mtrTwoL, LOW);
		analogWrite(pwmF, speed);
		analogWrite(pwmL, speed);
}

void turnLeft(){
		digitalWrite(mtrOneF, HIGH);
		digitalWrite(mtrTwoF, LOW);
		digitalWrite(mtrOneL, LOW);
		digitalWrite(mtrTwoL, HIGH);
		analogWrite(pwmF, speed);
		analogWrite(pwmL, speed);
}

void turnRight(){
		digitalWrite(mtrOneF, LOW);
		digitalWrite(mtrTwoF, HIGH);
		digitalWrite(mtrOneL, HIGH);
		digitalWrite(mtrTwoL, LOW);
		analogWrite(pwmF, speed);
		analogWrite(pwmL, speed);
}

void stopMotors(){
		digitalWrite(mtrOneF, LOW);
		digitalWrite(mtrTwoF, LOW);
		digitalWrite(mtrOneL, LOW);
		digitalWrite(mtrTwoL, LOW);
		analogWrite(pwmF, speed);
		analogWrite(pwmL, speed);
}


void loop(){
	int senseFvalue = digitalRead(senseF);
	int senseLvalue = digitalRead(senseL);
	char lastTurn = 'S';
	if (senseLvalue == LOW && senseFvalue == LOW){
		goStraight();
		lastTurn = 'S';
	} else if (senseFvalue == HIGH && senseLvalue == LOW){
		turnLeft();
		lastTurn = 'L';
	} else if (senseFvalue == LOW && senseLvalue == HIGH){
		turnRight();
		lastTurn = 'R';
	} else if (senseFvalue == HIGH && senseLvalue == HIGH){
		if(lastTurn == 'L') turnLeft();
		else if(lastTurn == 'R') turnRight();
		else stopMotors();
	}
}
