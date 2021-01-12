# Skippy the shiny beer can

## Project Goal

Built a voice assistant that can integrate with Home-Assistant without need for cloud based service.
Target : replacement of Alexxa or google voice assistant to remove cloud dependency and latency

## hardware components

### Server node

- intel based pc (NUC/...)
- 
### Satellite node

- Raspberry Zero (w) : https://www.raspberrypi.org/products/raspberry-pi-zero-w/ 
- Respeaker 2 mic hat : https://respeaker.io/2_mic_array/
- 8 ohm - 3 watts speaker jst-ph2.0 interface : https://www.amazon.fr/gp/product/B0738NLFTG/ref=ppx_yo_dt_b_asin_title_o02_s01?ie=UTF8&th=1  

## software components
- ubuntu server 20.04 LTS on pc : https://ubuntu.com/download/server
- raspbian buster lite on raspberry zero : https://www.raspberrypi.org/software/operating-systems/
- rhasspy : https://rhasspy.readthedocs.io/en/latest/tutorials/

## installation steps

(see : https://rhasspy.readthedocs.io/en/latest/tutorials/#from-scratch-on-a-raspberry-pi)
- flash sd-card
- enable ssh & wifi
- install re-speaker drivers
    
```
$ sudo apt-get update
$ sudo apt-get install --yes git
$ git clone https://github.com/respeaker/seeed-voicecard
$ cd seeed-voicecard
$ sudo ./install.sh
$ sudo reboot
```

