# HTPA32x32d Capture Image

## 项目目标
用树莓派通过I2c读取HTPA32x32d的图像，带温度数据。

## 要求
树莓派+HTPA32x32d模块

### 树莓派配置
树莓派4的管脚图

<img src="Markdown/images/raspberry-pi-4.png">

1.通过raspi-config配置I2c

#### [Configuring I2C](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c)

打开终端, 输入 `sudo raspi-config`.

步骤如下

<img src="Markdown/images/learn_raspberry_pi_interfacing.png">
<img src="Markdown/images/learn_raspberry_pi_advancedopt.png">
<img src="Markdown/images/learn_raspberry_pi_i2c.png">
<img src="Markdown/images/learn_raspberry_pi_wouldyoukindly.png">
<img src="Markdown/images/learn_raspberry_pi_i2ckernel.png">
                
                
2.安装i2c-tools检查器件是否正常连接
```
sudo apt-get install -y i2c-tools
sudo i2cdetect -y 1
```
如果你没有使用第一个通道，你也可以检查其他通道，比如0-2-3

<img src="Markdown/images/learn_raspberry_pi_i2c-detect.png">

3.设置I2C速度。在与HTPA技术工程师的对话中，我们被告知将其设置为1Mhz会比较好，因此我们进行了这些设置。
```
sudo nano /boot/config.txt
```
在文件末尾添加 "dtparam=i2c_arm=on,i2c_arm_baudrate=1000000",保存文件然后重启设备

```
sudo reboot
```
### 文件列表

eeprom-test.py

htpa-test.py

htpa.py（pa.py is written as a library.）

capture_display.py

### 依赖的python库(python3):
```
 pip3 install python-periphery
 sudo apt-get install python-opencv
 pip3 install opencv-python
```

虽然i2cdetect命令可以在树莓派上识别设备，但有时传感器会引起问题。我认为这意味着你的设备已经烧毁，所以在运行主代码之前，我们需要测试是否可以与EEPROM和设备进行通信。

```
python eeprom-test.py
python htpa-test.py
```
--> 在你确定设备运行完美之后，你唯一需要做的就是运行如下命令。

```
python capture_display.py
```
![微信截图_20240313232549](https://github.com/zhaochengwei/HTPA32x32d_Raspberry_pi/assets/13081827/455b83c7-d131-4e3e-a960-77ddb73ab519)

### Additional Information

我得到最多帮助的一个来源是数据手册，而另一个则是关于图像捕捉、EEPROM设置的。

<span style="color:red">The datasheet states that the framerate is 60 Hz, never fall for it; the maximum speed you can achieve is around 8Hz </span>.


请确保仔细检查翻译的准确性和上下文，特别是技术术语和设备特定的行话，以确保它们与您领域中的正确规格和使用相符。



