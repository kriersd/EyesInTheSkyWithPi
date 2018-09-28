

![](images/cover.jpg)

**Session Objective:**  This is a simple little project to demonstrate docker on a RasperyPi and provide you with an introduction to the simplicity and power of containers. 

---

## Overview

**Here are the links to other blogs and github pages for reference**
https://blog.alexellis.io/track-flights-with-rpi/
https://github.com/alexellis/eyes-in-the-sky/blob/master/flightaware/Dockerfile
https://github.com/LoungeFlyZ/eyes-in-the-sky


**What You Need**

Here is what you need:
- RasperyPi Device
- MicroSD card
- NooElec ADSB Reciever
- A desire to learn
- A little bit of Linux skill (Just a little)

# Setup & Configuration of the Raspberry Pi


##Download and install OS on SSD Card
- Download the OS ZIP for Rasparian Stretch with Desktop (I use desktop). I won't go into details here because it's fairly simple. I use a macbook pro, so I have a SD Slot on my machine. I simply download the Raspbian image and use Etcher to load the image on my SD card. Once that's done all you need to do is boot the Pi up and finsih the inital setup. 
    - https://www.raspberrypi.org/downloads/raspbian/
- Download Etcher to burn the image to the SSD Card. 
    - https://etcher.io/
- Boot your Raspberry Pi and configure the OS
	- Setup WIFI
    - enalbe SSH
    - **CHANGE THE PASSWORD FOR USER pi**

##Setup Dynamic DNS

I use duckdns.org to setup my dynamic IP address on the Pi. I do this because I am often using my phone's hotspot for internet connectivity and the ip address changes every time my Pi boots. You will need to know the IP address of your pi to ssh into the pi from a terminal window. 

**note**: _I have found that must also have my laptop connected to my phone's hotspot in order to ssh into my pi. That may not be the case for for everyone. Just to be safe, I would connect your laptop to the same hotspot as your pi when you want to ssh into the pi_

Go to this site for the instructions to setup and configuration dynamic dns on your pi. 
https://www.duckdns.org/
- sign in to the site. 
    - You can use Twitter, Facebook, Google, or Reddit to sign in. (Quick and easy!!)
- create a dynamic domain name
- Configure your Pi to send the IP address to the server, so the domain name gets updated with the IP address at boot. 
	- Follow these instructions here: 
        - http://www.duckdns.org/install.jsp

**Note**: _I had to make one minor change to the duck.sh script because it wasn't picking up the right ip address. You will need to add your own token and your domain name of course_

```
    ip=($( ifconfig | grep "inet " | grep -v 127.0.0.1 | cut -c 14-25))

    echo ${ip}

    echo url="https://www.duckdns.org/update?domains=<your domain>&token=<your token>&ip="${ip} | curl -k -o ~/d
uckdns/duck.log -K -
```

##Setup SSH on the Pi** 

Follow these instructions to enable ssh on the pi. You then do not need to have a monitor hooked up to connect. 
https://www.raspberrypi.org/documentation/remote-access/ssh

**Reboot your Pi**
Now you should be able to ssh into your pi using your terminal window on your laptop. 

```
ssh pi@<yourdomainname>.duckdns.org
```

---
