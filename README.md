The Sentry family of cameras provides a very easy-to-use development web interface that can be very quickly integrated into your existing development.

## 1. Interface Overview

Sentry provides the following four major interfaces:
- Distribution network interface
- Device Discovery Interface
- Interface for grabbing an image
- Interface to get the video stream
- Interface to control image quality

Next we will describe the use of these interfaces in detail


## 2. Detailed description of the interface

### 2.1 Distribution network interface

Sentry uses a serial port to config wifi. The format of the serial port send is as follows:

```
&&SSID:test-wifiname
&&PASS:test-password
&&NAME:test-sentryname
```

Note that each line above needs to be followed by a newline at the end to send to Sentry, and the order of sending is the same as the order listed above. If the serial port return is "SAVE", the setup is successful. (Please refer to this document for the detailed [Sentry wifi config](https://docs.google.com/presentation/d/1kwmyUJnEdvoTmH9pVKA9GpsY37tbT-Z7G08sZ-Bsne4/edit?usp=sharing))


### 2.2 Device Discovery Interface

In the local network, traverse 1~255 addresses in the same segment and send the following http request, Sentry will return certain format data after receiving it.

Send request: http://xxx.xxx.xx.xx:88/find
Sentry return: Sentry:camera-sentryname:sentry-ip-address

The Sentry inverts its own device name and IP address. After receiving these two pieces of information, the Sentry can be controlled in the next step
> Note that the port number here is 88


### 2.3 Sentry shooting interface

Type in your browser: http://xxx.xxx.xx.xx/capture to return the captured image
> Note that the port number of this interface is the default port number

### 2.4 Sentry video streaming interface

Type in your browser: http://xxx.xxx.xx.xx:81/stream
return video stream
> Note that the port number of this interface is 81


### 2.5 Sentry Image Control Interface

By typing Sentry's IP address directly into your browser: http://xxx.xxx.xx.xx

> The following settings will be overwritten after Sentry is restarted, and  you need to resend the request to make a setting

**1. Set camera resolution**

Parameter value:
7-->480x320
8-->640x480
9-->800x600
10-->1024x768
11-->1280x720

url request: 
```http://192.168.8.4/control?var=framesize&val=11```

val=11 indicates that the resolution of the camera is set to 1280x720

**2. Set whether the image is flipped**

Parameter value:
1-->enable     flip vertically
0-->disable    not flip vertically

```http://192.168.8.4/control?var=vflip&val=1```

val=1 indicates that the image will flip vertically


**3. Set image quality**

Parameter value:
10~64
A lower number means a higher quality


```http://192.168.8.117/control?var=quality&val=33```

val=33 indicates that set the picture quality to 33





