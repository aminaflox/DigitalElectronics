# DigitalElectronics
## This is description of intelligent waste container for small-scale  cases. Project is based on an Arduino Mega board and an ultrasonic sensor to monitor movement of the hand to open trash bin lid. The system is plugged to socket via cable. System perfomance was found satisfactory to the obtained test results during one week.
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
___ 


https://user-images.githubusercontent.com/98947733/171790715-71a9ae35-bcbe-4ef0-9265-d797bb71fc92.mp4
___


https://user-images.githubusercontent.com/98947733/171791704-2354009d-aecd-469b-bdfb-6832f223ab7a.mp4

___
![photo5247208528626694238](https://user-images.githubusercontent.com/98947733/171791837-b397047d-eb93-4171-a4f7-ba1efef69f12.jpg)
___
![photo5244523246353759488](https://user-images.githubusercontent.com/98947733/171792169-e93356ad-9d4f-4ffa-a7db-ac70b7033636.jpg)

