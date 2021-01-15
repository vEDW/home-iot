# Skippy the shiny beer can

## Project Goal

Build a voice assistant that can integrate with Home-Assistant without need for cloud based services.
The goal is to replace the likes of Alexxa or google voice assistant to remove internet and cloud dependency.

Home-assistant is considered already deployed and running in your environment.

remark : 

    skippy is a character from the book series "Expeditionary Force" written by Craig Alanson (https://www.craigalanson.com/).
    It is an advanced AI with an "attitude" that can do all kind of neat things with technology.

    see also : https://expeditionary-force-by-craig-alanson.fandom.com/wiki/Skippy

## hardware components

### Server node

- intel based pc (NUC/...) 

### Satellite node

- Raspberry Zero (w) : https://www.raspberrypi.org/products/raspberry-pi-zero-w/ 
- Respeaker 2 mic hat : https://respeaker.io/2_mic_array/
- 8 ohm - 3 watts speaker jst-ph2.0 interface : https://www.amazon.fr/gp/product/B0738NLFTG/ref=ppx_yo_dt_b_asin_title_o02_s01?ie=UTF8&th=1  

## software components

- ubuntu server 20.04 LTS on pc : https://ubuntu.com/download/server
- raspbian buster lite on raspberry zero : https://www.raspberrypi.org/software/operating-systems/
- rhasspy : https://rhasspy.readthedocs.io/en/latest/tutorials/

## Base installation steps

docker is installed and running.



## Satellite installation steps

(see : https://rhasspy.readthedocs.io/en/latest/tutorials/#from-scratch-on-a-raspberry-pi)

- flash sd-card
- enable ssh & wifi

### Satelliite install respeaker drivers

- install re-speaker drivers
    
```
$ sudo apt-get update
$ sudo apt-get install --yes git
$ git clone https://github.com/respeaker/seeed-voicecard
$ cd seeed-voicecard
$ sudo ./install.sh
$ sudo reboot
```

This may take a long time to complete, and will reboot your Pi when finished. Once your Pi reboots, log in and check if your microphone is available:

```
$ arecord -L
```
if all goes well, you should see something like : 

```
null
    Discard all samples (playback) or generate zero samples (capture)
jack
    JACK Audio Connection Kit
pulse
    PulseAudio Sound Server
default
playback
capture
dmixed
array
sysdefault:CARD=seeed2micvoicec
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Default Audio Device
dmix:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Direct sample mixing device
dsnoop:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Direct sample snooping device
hw:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Direct hardware device without any conversions
plughw:CARD=seeed2micvoicec,DEV=0
    seeed-2mic-voicecard, bcm2835-i2s-wm8960-hifi wm8960-hifi-0
    Hardware device with all software conversions
usbstream:CARD=seeed2micvoicec
    seeed-2mic-voicecard
    USB Stream Output
```

### install docker

```
$ curl -sSL https://get.docker.com | sh
```

add user to docker group
```
$ sudo usermod -aG docker pi
$ sudo reboot
```

Raspberry Pi Zero

Docker on the Raspberry Pi Zero appears to be broken, and will pull the wrong Docker image by default. To fix this, you must enable "experimental" features in your Docker daemon and explicitly specify the platform.

First, edit your ```/etc/docker/daemon.json``` file (create it if it doesn't exist using ```sudo```) and add the following content:
```
{
  "experimental": true
}
```

Next, restart your Docker daemon by running:
```
$ sudo systemctl restart docker
```

Finally, pull the correct Docker image:
```
$ docker pull --platform linux/arm/v6 rhasspy/rhasspy
```

remark : the image is about 1.3 GB large - this will take some time to pull down.

## install docker-compose

installing docker-compose on Raspbian is done through python installer (for some obscure reason)



```
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip

sudo pip3 install docker-compose
```

## testing rhasppy on pi zero



```
docker run -it -p 12101:12101 \
      -v "$HOME/.config/rhasspy/profiles:/profiles" \
      -v "/etc/localtime:/etc/localtime:ro" \
      --device /dev/snd:/dev/snd \
      rhasspy/rhasspy \
      --user-profiles /profiles \
      --profile en
```

French version:

```
docker run -it -p 12101:12101 \
      -v "$HOME/.config/rhasspy/profiles:/profiles" \
      -v "/etc/localtime:/etc/localtime:ro" \
      --device /dev/snd:/dev/snd \
      rhasspy/rhasspy \
      --user-profiles /profiles \
      --profile fr
```


# configuration

## integration in Home-Assistant

TO DO

https://www.atomicha.com/home-assistant-how-to-generate-long-lived-access-token-part-1/



## 3D housing

To Do
