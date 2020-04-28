---
layout: post
author: kenji
category: pi
---
# Set up camera of Raspberry pi zero w
Followed tutorial here.

https://tutorial.cytron.io/2017/08/16/raspberry-pi-zero-w-pi-camera-application/

```
sudo apt update
sudo apt upgrade
```

While running `sudo apt upgrade`, this warning message was shown:
```
Get:27 http://archive.raspberrypi.org/debian buster/main armhf rpi-update all 20200409 [7488 B]     
Fetched 37.7 MB in 13s (2903 kB/s)                                                                  
apt-listchanges: Can't set locale; make sure $LC_* and $LANG are correct!
Reading changelogs... Done
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_TIME = "nl_NL.UTF-8",
	LC_MONETARY = "nl_NL.UTF-8",
	LC_ADDRESS = "nl_NL.UTF-8",
	LC_TELEPHONE = "nl_NL.UTF-8",
	LC_NAME = "nl_NL.UTF-8",
	LC_MEASUREMENT = "nl_NL.UTF-8",
	LC_IDENTIFICATION = "nl_NL.UTF-8",
	LC_NUMERIC = "nl_NL.UTF-8",
	LC_PAPER = "nl_NL.UTF-8",
	LANG = "en_GB.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to a fallback locale ("en_GB.UTF-8").
```

To fix this, run the following:
```
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
locale-gen en_US.UTF-8
dpkg-reconfigure locales
```

It seems you need to run as `root`.
```
pi@pizero1:~ $ export LANGUAGE=en_US.UTF-8
pi@pizero1:~ $ export LANG=en_US.UTF-8
pi@pizero1:~ $ export LC_ALL=en_US.UTF-8
-bash: warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)
pi@pizero1:~ $ locale-gen en_US.UTF-8
rm: cannot remove '/usr/lib/locale/locale-archive': Permission denied
Generating locales (this might take a while)...
  en_GB.UTF-8...cannot open locale archive "/usr/lib/locale/locale-archive": Permission denied
 done
Generation complete.
pi@pizero1:~ $ dpkg-reconfigure locales
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = "en_US.UTF-8",
	LC_ALL = "en_US.UTF-8",
	LC_ADDRESS = "nl_NL.UTF-8",
	LC_NAME = "nl_NL.UTF-8",
	LC_MONETARY = "nl_NL.UTF-8",
	LC_PAPER = "nl_NL.UTF-8",
	LC_IDENTIFICATION = "nl_NL.UTF-8",
	LC_TELEPHONE = "nl_NL.UTF-8",
	LC_MEASUREMENT = "nl_NL.UTF-8",
	LC_TIME = "nl_NL.UTF-8",
	LC_NUMERIC = "nl_NL.UTF-8",
	LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_MESSAGES to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
/usr/sbin/dpkg-reconfigure must be run as root
pi@pizero1:~ $ 
```

Rerun as `root`
```
pi@pizero1:~ $ sudo locale-gen en_US.UTF-8
Generating locales (this might take a while)...
  en_GB.UTF-8... done
Generation complete.
pi@pizero1:~ $ sudo dpkg-reconfigure locales
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = "en_US.UTF-8",
	LC_ALL = "en_US.UTF-8",
	LC_ADDRESS = "nl_NL.UTF-8",
	LC_NAME = "nl_NL.UTF-8",
	LC_MONETARY = "nl_NL.UTF-8",
	LC_PAPER = "nl_NL.UTF-8",
	LC_IDENTIFICATION = "nl_NL.UTF-8",
	LC_TELEPHONE = "nl_NL.UTF-8",
	LC_MEASUREMENT = "nl_NL.UTF-8",
	LC_TIME = "nl_NL.UTF-8",
	LC_NUMERIC = "nl_NL.UTF-8",
	LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_MESSAGES to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
/usr/bin/locale: Cannot set LC_CTYPE to default locale: No such file or directory
/usr/bin/locale: Cannot set LC_MESSAGES to default locale: No such file or directory
/usr/bin/locale: Cannot set LC_ALL to default locale: No such file or directory
Generating locales (this might take a while)...
  en_GB.UTF-8... done
  en_US.UTF-8... done
Generation complete.
pi@pizero1:~ $ 
```

Hmm, it's a bit weird that `en_GB.UTF-8` locale was generated after specifying `en_US.UTF-8`. Also `No such file or directory` warning. However, it's just locale so now I just ignore.

# raspi-config
```
sudo raspi-config 
```
Enable Camera interface by following the instruction and then `reboot`.

To test the camera, take an image
```
raspistill -o image
```
Copy the image to the local machine.
```
scp pi@pizero1:/home/pi/image .
```
Or use `vcgencmd get_camera` command.
```
pi@pizero1:~ $ vcgencmd get_camera
supported=1 detected=1
```

# UV4L
https://gist.github.com/accuware/370c3fdd758b5cb4b41c6aa2acfe9ce6
Install UV4L and the WebRTC plugin for UV4L.

Register repo.
```
curl http://www.linux-projects.org/listing/uv4l_repo/lpkey.asc | sudo apt-key add -
echo "deb http://www.linux-projects.org/listing/uv4l_repo/raspbian/stretch stretch main" | sudo tee -a /etc/apt/sources.list
sudo apt-get update
```

Install packages. This is only for pi zero!
```
sudo apt-get install -y uv4l uv4l-raspicam uv4l-raspicam-extras uv4l-webrtc-armv6 uv4l-raspidisp uv4l-raspidisp-extras
```

# Reference
https://daker.me/2014/10/how-to-fix-perl-warning-setting-locale-failed-in-raspbian.html

https://medium.com/home-wireless/headless-streaming-video-with-the-raspberry-pi-zero-w-and-raspberry-pi-camera-38bef1968e1

https://gist.github.com/accuware/370c3fdd758b5cb4b41c6aa2acfe9ce6