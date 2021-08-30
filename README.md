# Umbrel Status Screen

Updated `umbrel-details` script to display similar information like the RaspiBlitz on a 3.5 inch LCD display.

## Installation

1. Login via SSH on your Pi running Umbrel OS

	```
	ssh umbrel@umbrel.local
	```

2. Install Waveshare LCD screen drivers

	```
	git clone https://github.com/waveshare/LCD-show.git
	cd LCD-show/
	chmod +x LCD35-show
	sudo ./LCD35-show lite
	```

	- Use `sudo ./LCD35-show lite 180` instead to flip screen
	- see https://www.waveshare.com/wiki/3.5inch_RPi_LCD_(A) for further information
	- No worries, Pi will restart. Login again.
	
3. Replace content of `umbrel-details` file

	```
	nano ~/umbrel/scripts/umbrel-os/umbrel-details
	```

4. Update Connection details service

	```
	sudo nano /etc/systemd/system/umbrel-connection-details.service
	```
	Service section should look like this:
	```
	[Service]
	Type=simple
	Restart=always
	RestartSec=60s
	ExecStart=/home/umbrel/umbrel/scripts/umbrel-os/umbrel-details
	User=umbrel
	Group=umbrel
	StandardOutput=tty
	TTYPath=/dev/tty1
	```

5. Restart your Umbrel via Web interface and enjoy your new status screen