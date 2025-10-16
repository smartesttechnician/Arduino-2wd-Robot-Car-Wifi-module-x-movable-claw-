# Arduino-2wd-Robot-Car-Wifi-module-x-movable-claw-
#define BLYNK_TEMPLATE_ID "TMPL6nkexvefV"
#define BLYNK_TEMPLATE_NAME "IED Bot"
#define BLYNK_AUTH_TOKEN "bXV9ZG1ex4LrX1U2p3bVJ2Go-fmFSfAF"

#define BLYNK_PRINT Serial
#include <ESP8266_Lib.h>
#include <BlynkSimpleShieldEsp8266.h>

char ssid[] = "";  // essentially your phone hotspot 
char pass[] = "";

#include <SoftwareSerial.h>
SoftwareSerial EspSerial(12, 13);

#define ESP8266_BAUD 9600

ESP8266 wifi(&EspSerial);
#define motor_IN1 3
#define motor_IN2 5
#define motor_IN3 6
#define motor_IN4 9

#define Hit_aPin 4
#define Hit_bPin 2

#include <Servo.h> 
Servo clawServo;      // servo 

                                 
BlynkTimer timer;               

void setup()
{
  Serial.begin(9600);
  EspSerial.begin(ESP8266_BAUD);
  delay(10);

  Blynk.begin(BLYNK_AUTH_TOKEN, wifi, ssid, pass, "blynk.cloud", 80);

  pinMode(6, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(5, OUTPUT);
 
 clawServo.attach(A1);
 clawServo.write(70);  // claw open when start 
}

void loop() {
  Blynk.run();
  timer.run();
  targetsensor();
}

//Drive Functions
BLYNK_WRITE(V0) {
  int drive0 = param.asInt();
  Serial.print("V0 (Forward): ");  // used to check status of the car 
  Serial.println(drive0);
  if (drive0 == 1) {
    forward();
  } else {
    stop();
  }
}

BLYNK_WRITE(V1) {
  int drive1 = param.asInt();
  if (drive1 == 1) {
   backward();
  } else {
    stop();
  }
}

BLYNK_WRITE(V2) {
  int drive2 = param.asInt();
  if (drive2 == 1) {
    left();
  } else {
    stop();
  }
}

BLYNK_WRITE(V3) {
  int drive3 = param.asInt();
  if (drive3 == 1) {
    right();
  } else {
    stop();
  }
}

void targetsensor() {
  if (!digitalRead(2)) {        
    clawServo.write(70);           
  }
  if (!digitalRead(4)) {       
     clawServo.write(20);                               
  }
}


void forward() {
  analogWrite(6, 150);
  digitalWrite(9, LOW);
  digitalWrite(3, LOW);
  analogWrite(5, 150);
}

void backward() {
  digitalWrite(6, LOW);
  analogWrite(9, 150);
  analogWrite(3, 150);
  digitalWrite(5, LOW);
}

void left() {
  digitalWrite(6, LOW);
  digitalWrite(9, LOW);
  digitalWrite(3, LOW);
  analogWrite(5, 150);
}

void right() {
  analogWrite(6, 150);
  digitalWrite(9, LOW);
  digitalWrite(3, LOW);
  digitalWrite(5, LOW);
}

void stop() {
  digitalWrite(6, LOW);
  digitalWrite(9, LOW);
  digitalWrite(3, LOW);
  digitalWrite(5,LOW);
} */

