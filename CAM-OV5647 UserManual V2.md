# **CAM-OV5647** **UserManual**



![](https://github.com/INNO-MAKER/CAM-OV5647/raw/main/picture/background.jpg)

## 1. **General**

CAM-OV5647 is a low-cost wider field view camera module, designed for whole series Raspberry(P4/Pi3 B+/PI3 A+/PI3/PI ZERO/PI ZERO 2W/CM4/CM3+). The CAM-OV5647 has a 5 M Pixel sensor, and connects via a ribbon cable to the CSI connector on the Raspberry Pi. The video and still image quality is better than a USB webcam of similar price.

CAM-OV5647 is a Plug and Play device, driver-free. Support  libcamera and  Raspicam.

## 2. **Features** 

1. The   CAM-OV5647 Module is a low-cost wider field view camera module that designed for all Raspberry Pi. Comes with Pi4 and Pi Zero dedicated cable.

2. Connects to the CSI connector of Raspberry Pi directly. High bandwidth communication from the camera module to the Raspberry pi.

3. On-board OmniVision OV5647[6] Color CMOS QSXGA (5-megapixel); Video: 1080p at 30 fps with codec H.264 (AVC).

4. Len Feature: 2.8 Focal Length. F/NO: 2.2. Field Of view: D=90° H=72°. Element: 4G+IR. CRA: 10°. Relative Illumination: 52%. Focal distance is adjustable.

5. Plug and Play device, driver-free for all raspberry pi board，please download from our website product page or wiki（you can find link from color page）

## 3. **Hardware** **Description**               

### 3.1 Overview                              

|                                       |                                       |
| :-----------------------------------: | :-----------------------------------: |
|              Sensor type              |  OmniVision OV5647 Color CMOS QSXGA   |
|              Sensor size              |       3.67 x 2.74 mm (1/4 inch)       |
|              Resolution               |           5 million pixels            |
|             Field of view             |       Fov(D) = 90° Fov(H) = 72°       |
| Pixel Count(Still Picture Resolution) |              2592 x 1944              |
|             Focal Length              |                2.8 mm                 |
|            Focal Distance             |              Adjustable               |
|            F(N) /Aperture             |                  2.2                  |
|              Pixel Size               |             1.4 x 1.4 um              |
|                 Video                 |    1080p at 30 fps 720p at 60 fps     |
|              Board Size               | 39 x 39 mm (not including flex cable) |
|             TV DISTORTION             |                 <-17%                 |
|                  CRA                  |                  10°                  |
|         Relative Illumination         |                  52%                  |
|    Minimum Object Distance(M.O.D)     |               0.1 meter               |
|                Element                |                 4G+IR                 |
|             Lens Diameter             |                  M12                  |
|           Lens Seat Spacing           |                 22 mm                 |
|            Mounting Holes             |             4x D=2.20 mm              |

### 3.2 Len Size 

![](https://github.com/INNO-MAKER/CAM-OV5647/raw/main/picture/Len%20size.png)

### 3.3 Connect



![](https://github.com/INNO-MAKER/CAM-OV5647/raw/main/picture/connection.png)







## 4. **Libcamera** **Description**                

Raspberry Pi is transitioning from a legacy camera software stack based on proprietary Broadcom GPU code to an open-source stack based on `libcamera`. Raspberry Pi OS images from *Bullseye* onwards will contain **only** the `libcamera`-based stack. Raspberry Pi OS images up to and including *Buster* will contain the legacy *Raspicam* stack, though the `libcamera` stack and applications can be installed [using *apt*](https://www.raspberrypi.com/documentation/accessories/camera.html#libcamera-and-libcamera-apps-packages), or built by following the [normal build instructions](https://www.raspberrypi.com/documentation/accessories/camera.html#building-libcamera-and-libcamera-apps).

libcamera is an open source Linux community project. More information is available at the [libcamera website](https://libcamera.org/):

The libcamera source code can be found and checked out from the [official libcamera repository](https://git.linuxtv.org/libcamera.git/).

When running a Raspberry Pi OS based on Bullseye, the 5 basic libcamera-apps are already installed. In this case, official Raspberry Pi cameras will also be detected and enabled automatically. Below we only take ‘libcamera-hello’ for example. For more information, please refer to below link： 

https://www.raspberrypi.com/documentation/accessories/camera.html#binary-packages



### 4.1Libcamera-hello

libcamera-hello is the equivalent of a "hello world" application for the camera. It starts the camera, displays a preview window.

#### 4.1.1 Preview

Use below command to start the preview.

```
libcamera-hello -t 0
```

#### 4.1.2 Set the Framerate

Use below command to set the camera frame rate, the maximum of OV5647 sensor is 30 fpts.

```
libcamera-hello --framerate 30
```

------



### 4.2 Test the Framerate

Use below tools can test the current frame rate of camera module.

```
v4l2-ctl --stream-mmap --stream-count=-1 -d /dev/video0 --stream-to=/dev/null
```

------



## 5. **Raspicam** **Description** 

Please not that this functionality is deprecated and will not be supported for future development.

### 5.1 Enable Camera On Legacy

#### 5.1.1 raspi-config

 Open the raspi-config tool when you first set up your Raspberry Pi on Legacy

```
sudo raspi-config
```

#### 5.1.2 Camera Interface Enable

Select ‘Interfacing Options’ → ‘Camera’ →'Yes'→'Finish'

------



### 5.2 Enable Camera On Bullseyes

#### 5.2.1 raspi-config

 Open the raspi-config tool when you first set up your Raspberry Pi on Bullseyes

```
sudo raspi-config
```

#### 5.2.2 Camera Interface Enable

Select ‘Interfacing Options’ → 

‘I1 Legacy Camera Enable/disable legacy camera support’ →'Yes'→'Finish'



------



### 5.3 Take a Photo

raspistill is the command line tool for capturing still photographs with a Raspberry Pi camera module.

#### 5.3.1 Take a picture name ‘test’.

```
raspistill -o test.jpg
```

#### 5.3.2 Take a picture name ‘test’ with resolution 640*480

```
raspistill -o test.jpg -w 640 -h 480
```

 

#### 5.3.3 Take a picture name ‘test’ after 10 seconds(10000ms).

```
raspistill -t 10000 -o test.jpg
```

#### 5.3.4 Take a picture name ‘test’ with PNG format(raw date) . If will take more time to save.

```
raspistill -o test.png -e png
```

------



### 5.4 Take a Video

raspivid is the command line tool for capturing video with a Raspberry Pi camera module.

#### 5.4.1 Take a 10s(10000ms) video name ‘test’.

```
raspivid -o test.h264 -t 10000
```

####  5.4.2 Take a 10s(10000ms) video name ‘test’ with resolution 1280*720’.

```
raspivid -o test.h264 -t 10000 -w 1280 -h 720
```

------

