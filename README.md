# sensor-ditection-
sensor ditection with esp32 and light 
#include <Wire.h>

#define echoPin 2
#define trigPin 4

long duration, distance;

void setup() {
  Serial.begin(9600);  // Fixed capitalization of Serial
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(5, OUTPUT);
}

void loop() {
  // Trigger the ultrasonic sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the echo time
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate distance in centimeters
  distance = duration / 58.2;
  
  // Display the distance
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  // Delay before next measurement
  delay(100);
  
  // Control an output based on distance
  if (distance <= 50) {
    digitalWrite(5, HIGH);
    delay(100);
  } else {
    digitalWrite(5, LOW);
  }
}

