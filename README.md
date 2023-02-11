# AutonomousCar-Arduino

## An autonomous car Using Arduino and ML

### An idea of implementing large scale project into small Prototype. It is an IOT based project.

Preview
[![Watch the video](https://i.imgur.com/vKb2F1B.png)](https://github.com/Abhishek00p/AutonomousCar-Arduino/blob/master/modelRunning.mp4?raw=false)

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
