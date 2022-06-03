# DigitalElectronics
## This paper presents a cost-effective design of intelligent waste container for small-scale  cases. This project is based on an Arduino Mega board and an ultrasonic sensor to monitor movement of the hand to open trash bin lid. The system is plugged to socket via cable. System perfomance was found satisfactory to the obtained test results during one week.
___ 
```c++
int echo = 6;
int servoPin = 9;
long duration, distance, average;
long aver[3];

void setup() {
  Serial.begin(9600);
  servo.attach(servoPin);
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  servo.write(0); //CLOSES CAP ON STARTING
  delay(100);
  servo.detach();
}

void measure() {
  digitalWrite(trig, LOW);
  delayMicroseconds(5);
  digitalWrite(trig, HIGH);
  delayMicroseconds(15);
  digitalWrite(trig, LOW);
  pinMode(echo, INPUT);
  duration = pulseIn(echo, HIGH);
  distance = (duration / 2) / 29.1; //CALCULATES DISTANCE
}

void loop() {
  Serial.println(distance);     //CAN BE DISABLED
  for (int i = 0; i <= 2; i++) { //CALCULATES AVERAGE DISTANCE
    measure();
    aver[i] = distance;
    delay(10);
  }
  distance = (aver[0] + aver[1] + aver[2]) / 3;

  if ( distance <= 20 ) { //CHANGE AS PER AS NEED
    servo.attach(servoPin);
    delay(1);
    servo.write(0);
    delay(3500); //CHANGE AS PER AS NEED
    servo.write(180);
    delay(1500); //CHANGE AS PER AS NEED
    servo.detach();
  }
}
```
