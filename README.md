# PiClock
![image](https://github.com/dandydanny/PiClock/blob/master/PiClock_readme_image.jpg)

### What?
Code that drives the Pimoroni Micro Dot pHAT with a current time display

### Why?
1. Retro 5x7 LED dot matrix display is cool
1. Clocks should have cool displays
1. Raspberry Pi should display useful information

### Where?
In my Raspberry Pi.

### Setup
#### Library Installation
```curl https://get.pimoroni.com/microdotphat | bash```

#### Clock Source Code

Put clock source code in:
/home/volumio/clock.py

```
import time
import datetime
from microdotphat import write_string, set_decimal, clear, show

while True:
    clear()
    t = datetime.datetime.now()
    if t.second % 2 == 0:
        set_decimal(2, 1)
        set_decimal(4, 1)
    else:
        set_decimal(2, 0)
        set_decimal(4, 0)
    write_string(t.strftime('%H%M%S'), kerning=False)
    show()
    time.sleep(0.05)
```

#### Make Clock Automatically Run on Boot

In /etc/systemd/system
Make clock.service file.

Put in following:

```
[Unit]
Description=Get clock service running at boot
After=mosquitto.service mysql.service

[Service]
ExecStart=/usr/bin/python3 /home/volumio/clock.py
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=clock
User=volumio
Group=volumio

[Install]
WantedBy=multi-user.target
```


Enable service: 

`sudo systemctl enable clock.service`

Start clock for current boot only:

`sudo systemctl start clock.service`

Check if it's running:

`systemctl status clock.service`

To select differnt time zone:

`tzselect`


### About
Daniel is a web developer seeking opportunities, beverage socials, and late-night taco runs. [dandydanny.github.io](https://git.io/vxurG)
