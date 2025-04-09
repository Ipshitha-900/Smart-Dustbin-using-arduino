# Smart-Dustbin-using-arduino
Project based on arduino
#include <Servo.h>

const int trigPin=7; //trigger pin for ultrasonic sensor
const int echoPin=6; //echo pin for ultrasonic sensor
const int servoPin=5; //servo pin 
Servo myservo;

void setup() {
  Serial.begin(9600); //initialise serial communication
  myservo.attach(servoPin); //attach the servo to its pin
  pinMode(trigPin,OUTPUT);
  pinMode(echoPin,INPUT);
  

}

void loop() {
  digitalWrite(trigPin,LOW); //clear 
  delayMicroseconds (2);
  digitalWrite(trigPin,HIGH);
  delayMicroseconds (10);
  digitalWrite(trigPin,LOW);

  long duration =pulseIn(echoPin,HIGH); //measure the time taken for the echo 
  int distance = duration /29/2; 
  Serial.print("duration: ");
  Serial.print(duration);
  Serial.print(" microseconds| distance:  ");
  Serial.print(distance);

  if (distance<20){
    myservo.write(180); //rotate the servo 180 degrees if distance is less than 20cm
    Serial.println(" Rotating servo to 180 degrees");
  }
  else{
    myservo.write(0); //rotate the servo to 0 degrees if distance is greater than 20cm
    Serial.println("Rotating servo to 0 degrees");
  }
  delay(500); //delay to readability to avoid rapid servo movements
  }
