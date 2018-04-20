# PiClock
Code that drives the Pimoroni Micro Dot pHAT with a current time display




In /etc/systemd/system

Make clock.service file.

Put in following

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

Put clock source code in:
/home/volumio/clock.py


Enable it with: sudo systemctl enable clock.service
Start it (this boot only) with: sudo systemctl start clock.service
Find if it's running with: systemctl status clock.service


To select differnt time zone:
tzselect
