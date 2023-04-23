# AutonomousCar-Arduino

## An autonomous car Using Arduino and ML

### An idea of implementing large scale project into small Prototype. It is an IOT based project.

Preview

https://user-images.githubusercontent.com/90974451/218242815-5cc34cc8-9641-4a9d-8746-cfafbf3770ac.mp4


```
Requirements

Hardware-
1. Arduino Uno
2. Arduino motor shield
3. HC-05 bluetooth module
4. car chasis ( motor ,wheels,car body)
5. li-ion rechargable batteries





software

IP-webcam ( available on playstore)
Note: I used IP-webcam as camera, You can purchase camera for arduino from the market
python
jupyter notebook
tensorflow for model training [ I used Teachable Machine platform for training ]

python Liabraries used - 

import cv2
import numpy as np
import serial
import time
from keras.models import load_model
import os
import socket 
import urllib
import sys
import serial

```


## Installation
##### Clone my git Repo into your desired location
##### open jupyter notebook 
##### go to cloned repo folder and open try01 file
##### open IP-WEBCAM software in mobile and click start Server
##### change ip address in "cv2.videocapture("newIPAddress/shot.jpg")line in try01 file
##### Run file in jupyter notebook

### you may need to change Model, Images are present in Imagesforcar folder for reference to train in model. 
### in label.txt classes for model are present (you can change )







```

/*

  Arduino Bluetooth Controlled Car
  Install Adafruit Motor Shield Library before uploading this code.
  AFMotor Library https://learn.adafruit.com/adafruit-motor-shield/library-install

  -> If you need helping guide on how to install library for the motor shield or how to use motor shield then
     watch this: https://youtu.be/vooJEyco1J4

     Caution: Remove the jumper or switch off the battery switch before connecting the Arduino board to computer.

     For more support contact me on Telegram: @UtGoTech


*/


#include <AFMotor.h>
#include <SoftwareSerial.h>
//#include "NewPing.h"

SoftwareSerial bluetoothSerial(0, 1); // RX, TX
#define echopin A2
#define trigopin A3

//initial motors pin
AF_DCMotor motor1(1, MOTOR12_1KHZ);
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);

char command;

void setup()
{
  bluetoothSerial.begin(9600);  //Set the baud rate to your Bluetooth module.
  Serial.println("Connected to BT");
  //  Serial.begin(91000);
  //  Serial.println("connected");
    pinMode (trigopin,OUTPUT);
    pinMode(echopin,INPUT);

  motor1.setSpeed(100);

  motor2.setSpeed(100);

  motor3.setSpeed(100);

  motor4.setSpeed(100);
}

void loop() {
    long  dis = data();
  //  delay(5000);

if (int(dis)<=9){
  Stop();
}else{

  if (bluetoothSerial.available() > 0) {
    command = bluetoothSerial.read();
    Serial.println(command);
    Stop(); //initialize with motors stoped
    //     if( int(dis) <=9){
    //    Stop();
    //     delay(0.5);
    //    back();
    //   delay(1);
    //    left();
    //    delay(0.5);
    //    Stop();
    //
    //  }

    switch (command) {
      case 'F':
        forward();
        break;
      case 'B':
        back();
        break;
      case 'L':
        left();
        break;
      case 'R':
        right();
        break;
      case 'G':
        forwardLeft();
        break;
      case 'I':
        forwardRight();
        break;
      case 'H':
        backLeft();
        break;
      case 'J':
        backRight();
        break;
      default :
        Stop();
        break;
    }
  }
}

}

long data(){

  digitalWrite(trigopin,LOW);
  delayMicroseconds(2);
  digitalWrite(trigopin,HIGH);
  delayMicroseconds(10);
  int distance = pulseIn(echopin,HIGH);

  return distance*0.034/2;
}

void forward()
{
  motor1.setSpeed(170); //Define maximum velocity
  motor1.run(FORWARD);  //rotate the motor clockwise
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(FORWARD);  //rotate the motor clockwise
  motor3.setSpeed(130); //Define maximum velocity
  motor3.run(FORWARD);  //rotate the motor clockwise
  motor4.setSpeed(170); //Define maximum velocity
  motor4.run(FORWARD);  //rotate the motor clockwise
  //delay(400);
  //  Stop();
}

void back()
{
  motor1.setSpeed(140); //Define maximum velocity
  motor1.run(BACKWARD); //rotate the motor anti-clockwise
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(BACKWARD); //rotate the motor anti-clockwise
  motor3.setSpeed(130); //Define maximum velocity
  motor3.run(BACKWARD); //rotate the motor anti-clockwise
  motor4.setSpeed(140); //Define maximum velocity
  motor4.run(BACKWARD); //rotate the motor anti-clockwise
  //delay(400);
  //  Stop();
}

void right()
{
  motor1.setSpeed(210); //Define maximum velocity
  motor1.run(FORWARD); //rotate the motor anti-clockwise
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(BACKWARD); //rotate the motor anti-clockwise
  motor3.setSpeed(130); //Define maximum velocity
  motor3.run(FORWARD);  //rotate the motor clockwise
  motor4.setSpeed(150); //Define maximum velocity
  motor4.run(FORWARD);  //rotate the motor clockwise
  //delay(400);
}

void left()
{
  motor1.setSpeed(150); //Define maximum velocity
  motor1.run(FORWARD);  //rotate the motor clockwise
  motor2.setSpeed(255); //Define maximum velocity
  motor2.run(FORWARD);  //rotate the motor clockwise
  motor3.setSpeed(120); //Define maximum velocity
  motor3.run(BACKWARD); //rotate the motor anti-clockwise
  motor4.setSpeed(210); //Define maximum velocity
  motor4.run(FORWARD); //rotate the motor anti-clockwise
  //delay(400);

}

void forwardLeft()
{
  //
  motor1.setSpeed(120);
  motor1.run(FORWARD);  //rotate the motor clockwise

  motor2.run(FORWARD);  //rotate the motor clockwise
  motor3.setSpeed(130);
  motor3.run(FORWARD);
  //rotate the motor anti-clockwise


  motor4.setSpeed(190);
  motor4.run(FORWARD); //rotate the motor anti-clockwise
  //    delay(400);
}
void forwardRight() {
  //
  motor1.setSpeed(190);
  motor1.run(FORWARD);


  motor3.setSpeed(160);
  motor3.run(FORWARD); //rotate the motor anti-clockwise
  motor4.setSpeed(120);
  motor4.run(FORWARD); //rotate the motor anti-clockwise
  //    delay(400);
}
//
void backRight() {
  //
  motor1.setSpeed(130);
  motor1.run(BACKWARD);
  //  motor3.setSpeed(180);
  //  motor3.run(BACKWARD); //rotate the motor anti-clockwise
  motor4.setSpeed(110);
  motor4.run(BACKWARD); //rotate the motor anti-clockwise
  //    delay(400);
}
//
void backLeft() {
  //
  motor1.setSpeed(110);
  motor1.run(BACKWARD);
  //  motor3.setSpeed(120);
  //  motor3.run(BACKWARD); //rotate the motor anti-clockwise
  motor4.setSpeed(130);
  motor4.run(BACKWARD); //rotate the motor anti-clockwise
  //    delay(400);
}
void Stop()
{
  motor1.setSpeed(0);  //Define minimum velocity
  motor1.run(RELEASE); //stop the motor when release the button
  motor2.setSpeed(0);  //Define minimum velocity
  motor2.run(RELEASE); //rotate the motor clockwise
  motor3.setSpeed(0); //Define minimum velocity
  motor3.run(RELEASE); //stop the motor when release the button
  motor4.setSpeed(0); //Define minimum velocity
  motor4.run(RELEASE); //stop the motor when release the button

}

```
