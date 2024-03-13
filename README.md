# HTPA32x32d Capture Image

## Purpose of the Project
To capture images from HTPA32x32d with Raspberry pi.


## Requirements


### Raspberry pi Configuration


Raspberry-pi 4 Pinout


<img src="Markdown/images/raspberry-pi-4.png">


First, we configure the I2C settings.


#### [Configuring I2C](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)


After opening the console, type `sudo raspi-config`.


Then follow the steps below.

<img src="Markdown/images/learn_raspberry_pi_interfacing.png">
<img src="Markdown/images/learn_raspberry_pi_advancedopt.png">
<img src="Markdown/images/learn_raspberry_pi_i2c.png">
<img src="Markdown/images/learn_raspberry_pi_wouldyoukindly.png">
<img src="Markdown/images/learn_raspberry_pi_i2ckernel.png">
                
                
To check if the device is connected or not, 
download the 
```
sudo apt-get install -y i2c-tools
```

library and type into the console
sudo i2cdetect -y 1
if you are not using the first channel, you can also check other channels like 0-2-3.

<img src="Markdown/images/learn_raspberry_pi_i2c-detect.png">
Then you need to set your I2c speed. In a dialogue with HTPA technical engineers, we were told that setting it to 1Mhz would be healthy, hence we make these settings.


sudo nano /boot/config.txt
After adding the line "dtparam=i2c_arm=on,i2c_arm_baudrate=1000000", save and exit the file.


sudo reboot
you can restart the device.

Code Content
eeprom-test.py
htpa-test.py
htpa.py
capture_display.py
Fully Working Project
--> htpa.py is written as a library.

Libraries required for the library:


 pip install python-periphery
 sudo apt-get install python-opencv
 pip install opencv-python
Note: Due to some requirements, our code works in python2, it will not work if you try to run it in python3.

Although the i2cdetect command recognizes the device on the raspberry pi, sometimes the sensors can cause problems. I think it means your device is burnt out, so before running the main code, we need to test if we can communicate with the EEPROM and the device.


python eeprom-test.py
python htpa-test.py
--> after you are sure that the device is working perfectly, the only thing you need to do is to run


python capture_display.py
Outputs
Additional Information
One of the sources I got the most help from was the datasheet while the other was about image capture, EEPROM settings

<span style="color:red">The datasheet states that the framerate is 60 Hz, never fall for it; the maximum speed you can achieve is around 8Hz </span>.

```
Make sure to double-check the translation for accuracy and context, especially technical terms and device-specific jargon, to ensure they align with the correct specifications and usage in your domain.
```
