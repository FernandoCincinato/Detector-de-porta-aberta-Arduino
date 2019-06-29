# Detector-de-porta-aberta-Arduino
Projeto de eletrônica para computação - SCC0180


Circuito do projeto:
https://www.tinkercad.com/things/8NF2KFNrF77

Video explicando o funcionamento:
https://youtu.be/EKtAz8PLLIk

Código utilizado:

#include <NewPing.h>

#define TRIGGER_PIN  12  // Arduino pin tied to trigger pin on the ultrasonic sensor.
#define ECHO_PIN     11  // Arduino pin tied to echo pin on the ultrasonic sensor.
#define MAX_DISTANCE 100 // Maximum distance we want to ping for (in centimeters).

NewPing sonar(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE); // NewPing setup of pins and maximum distance.

void setup() {
  Serial.begin(9600); // Open serial monitor at 9600 baud to see ping results.
  pinMode(9, OUTPUT);
}

void loop() {
  delay(100);                     
  Serial.print(sonar.ping_cm());       // Send ping, get distance in cm and print result (0 = outside set distance range)
  Serial.println("cm");
  if(sonar.ping_cm()>=10 || sonar.ping_cm()==0){     //anything far than 10 centimeters will trigger the LED
    digitalWrite(9, HIGH);
    delay(100);
    digitalWrite(9, LOW);
    }
}
