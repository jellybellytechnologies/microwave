
#****************************************************************#
# Software Author: Julian Sanchez
# Hardware Developed By: Lyle Frey and Julian Sanchez
# Version: 1.1beta1
# Inteded OS Version: Raspbian Jesse
# Designed For: Raspberry Pi 1 B+
# Python Version: 2.7
# Description: This software was designed for a Sharp Microwave 
# and enables you to use a UPC Wand to set the food time in the
# microwave
#
##  TBI (Planned Features):
# WiFi Booster 
# Bluetooth Music
# Web Interface
# Touch Screen
# PPPP Popcorn Pop Perfection Program) -- Detcts Poping Noise Stops and turns off Microwave
# 
#
#
#
#
#****************************************************************#


#Allows JSON to be fetched externally
import urllib
# Allows JSON to be read
import json
# GPIO Control Import
import RPi.GPIO as GPIO
from time import sleep

###Microwave Code###

#API Key to authorize access to the Microwave DB
apikey = "sS9d8yhJVEylqXJLStDkgGeGi63xEWlK"

#Sets GPIO Pin Numbering
GPIO.setmode(GPIO.BCM)

#Hides warnings that we already know about
GPIO.setwarnings(False)

#Sets Relay Pins as Output
GPIO.setup(23, GPIO.OUT)

#Sets Door Button as Input
GPIO.setup(18,GPIO.IN,pull_up_down=GPIO.PUD_UP)

#Resets Microwave Realy State to Off
GPIO.output(23, GPIO.HIGH)

while True:
        upc = raw_input('waiting for keyboard input ...\n')
	# URL to get datafrom
        geturl = "https://api.mlab.com/api/1/databases/microwavecookinginstructionsdb/collections/Foods?f={'time':1,'_id':0}&q={'upc':'"+upc+"'}&apiKey=" + apikey
        response = urllib.urlopen(geturl)
        data = json.loads(response.read())
	#Sets cooktime
        cooktime = data[0]['time']
                #counts down if time isnt zero
        while cooktime >= 0 and GPIO.input(18):
                                        sleep(1)
                                        cooktime-= 1
                                        GPIO.output(23,GPIO.LOW)
                                        print(cooktime)
	GPIO.output(23,GPIO.HIGH)
