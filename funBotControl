import RPi.GPIO as GPIO
import enum
from time import sleep

class Direction(enum.Enum):
	CW = 1
	CC = 2

GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)

#====================
# Camera movement (servo motor)
#====================
servoRotatePin = 8
servoTiltPin = 7

GPIO.setup(servoRotatePin, GPIO.OUT)
GPIO.setup(servoTiltPin, GPIO.OUT)

servoRotate= GPIO.PWM(servoRotatePin, 50)
servoTilt = GPIO.PWM(servoTiltPin, 50)

servoRotate.start(0)
servoTilt.start(0)

#====================
# Car movement
# d1 = driver 1
# d2 = driver 2
#====================

# Driver 1
# Motor 1 pins
d1_PWMA = 21
d1_AIN2 = 20
d1_AIN1 = 16

# Motor 2 pins
d1_PWMB = 23
d1_BIN2 = 24
d1_BIN1 = 25

# Driver 2
# Motor 3 pins
d2_PWMA = 22
d2_AIN2 = 27
d2_AIN1 = 17
# Motor 4 pins
d2_PWMB = 5
d2_BIN2 = 26
d2_BIN1 = 6


# Setup
GPIO.setup(d1_PWMA, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d1_AIN2, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d1_AIN1, GPIO.OUT, initial=GPIO.LOW)

GPIO.setup(d1_PWMB, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d1_BIN2, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d1_BIN1, GPIO.OUT, initial=GPIO.LOW)

GPIO.setup(d2_PWMA, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d2_AIN2, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d2_AIN1, GPIO.OUT, initial=GPIO.LOW)

GPIO.setup(d2_PWMB, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d2_BIN2, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(d2_BIN1, GPIO.OUT, initial=GPIO.LOW)

# Motor direction enabled

# Motor A - Driver 1
def d1_motor_A_Enabled(dir : Direction):
	if(dir == Direction.CW):
		GPIO.output(d1_PWMA, GPIO.HIGH)
		GPIO.output(d1_AIN2, GPIO.HIGH)
		GPIO.output(d1_AIN1, GPIO.LOW)
	else:
		GPIO.output(d1_PWMA, GPIO.HIGH)
		GPIO.output(d1_AIN2, GPIO.LOW)
		GPIO.output(d1_AIN1, GPIO.HIGH)

def d1_motor_A_Disabled():
	GPIO.output(d1_PWMA, GPIO.LOW)
	GPIO.output(d1_AIN2, GPIO.LOW)
	GPIO.output(d1_AIN2, GPIO.LOW)

# Motor B - Driver 1
def d1_motor_B_Enabled(dir : Direction):
	if(dir == Direction.CW):
        	GPIO.output(d1_PWMB, GPIO.HIGH)
        	GPIO.output(d1_BIN2, GPIO.HIGH)
        	GPIO.output(d1_BIN1, GPIO.LOW)
	else:
		GPIO.output(d1_PWMB, GPIO.HIGH)
		GPIO.output(d1_BIN2, GPIO.LOW)
		GPIO.output(d1_BIN1, GPIO.HIGH)

def d1_motor_B_Disabled():
         GPIO.output(d1_PWMB, GPIO.LOW)
         GPIO.output(d1_BIN2, GPIO.LOW)
         GPIO.output(d1_BIN2, GPIO.LOW)


# Motor A - Driver 2
def d2_motor_A_Enabled(dir : Direction):
	if(dir == Direction.CW):
        	GPIO.output(d2_PWMA, GPIO.HIGH)
        	GPIO.output(d2_AIN2, GPIO.HIGH)
        	GPIO.output(d2_AIN1, GPIO.LOW)
	else:
		GPIO.output(d2_PWMA, GPIO.HIGH)
		GPIO.output(d2_AIN2, GPIO.LOW)
		GPIO.output(d2_AIN1, GPIO.HIGH)

def d2_motor_A_Disabled():
         GPIO.output(d2_PWMA, GPIO.LOW)
         GPIO.output(d2_AIN2, GPIO.LOW)
         GPIO.output(d2_AIN2, GPIO.LOW)

# Motor B - Driver 2
def d2_motor_B_Enabled(dir : Direction):
	if(dir == Direction.CW):
		GPIO.output(d2_PWMB, GPIO.HIGH)
		GPIO.output(d2_BIN2, GPIO.HIGH)
		GPIO.output(d2_BIN1, GPIO.LOW)
	else:
		GPIO.output(d2_PWMB, GPIO.HIGH)
		GPIO.output(d2_BIN2, GPIO.LOW)
		GPIO.output(d2_BIN1, GPIO.HIGH)

def d2_motor_B_Disabled():
         GPIO.output(d2_PWMB, GPIO.LOW)
         GPIO.output(d2_BIN2, GPIO.LOW)
         GPIO.output(d2_BIN2, GPIO.LOW)

# Directions

def back():
	d1_motor_A_Enabled(Direction.CC)
	d1_motor_B_Enabled(Direction.CC)
	d2_motor_A_Enabled(Direction.CC)
	d2_motor_B_Enabled(Direction.CC)

def forward():
	d1_motor_A_Enabled(Direction.CW)
	d1_motor_B_Enabled(Direction.CW)
	d2_motor_A_Enabled(Direction.CW)
	d2_motor_B_Enabled(Direction.CW)

def left():
	d1_motor_A_Enabled(Direction.CW)
	d1_motor_B_Enabled(Direction.CC)
	d2_motor_A_Enabled(Direction.CC)
	d2_motor_B_Enabled(Direction.CW)

def right():
	d1_motor_A_Enabled(Direction.CC)
	d1_motor_B_Enabled(Direction.CW)
	d2_motor_A_Enabled(Direction.CW)
	d2_motor_B_Enabled(Direction.CC)

def stop():
	d1_motor_A_Disabled()
	d1_motor_B_Disabled()
	d2_motor_A_Disabled()
	d2_motor_B_Disabled()



#
# Rotate Camera
#

def rotateCameraRight():
	startVal: Float = 2
	for x in range (10):
		servoRotate.ChangeDutyCycle(startVal + 0.5)
		sleep(0.5)
		servoRotate.start(0)

def rotateCameraLeft():
	for x in range (7, 12):
		servoRotate.ChangeDutyCycle(7.5)
		sleep(0.2)
		servoRotate.start(0)

def tiltCameraTop():
	servoTilt.ChangeDutyCycle(6)
	sleep(0.5)
	servoTilt.start(0)

def tiltCameraBottom():
	servoTilt.ChangeDutyCycle(8)
	sleep(0.5)
	servoTilt.start(0)

import tty
import sys
import termios

# GET CONTROL  KEY PRESS
def getch():
	fd = sys.stdin.fileno()
	old_settings = termios.tcgetattr(fd)
	tty.setraw(sys.stdin.fileno())
	ch = sys.stdin.read(1)
	termios.tcsetattr(fd, termios.TCSADRAIN, old_settings)
	return ch

# Control

var = ''
#todo w and s reverse
while var != 'q':
	var = getch()
	if var == 's':
		forward()
	if var == 'w':
		back()
	if var == 'a':
		left()
	if var == 'd':
		right()
	if var == 'o':
		stop()
	if var == 'n':
		rotateCameraRight()
	if var == 'm':
		rotateCameraLeft()
	if var == 'k':
		tiltCameraTop()
	if var == 'l':
		tiltCameraBottom()

	sleep(0.1)
	print (var)
