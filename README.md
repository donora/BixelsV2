# Bixels Installation Instructions

_This guide will take you through the process of installing the Bixels software on a Raspberry Pi_

_You will need:_
- _A Raspberry Pi_
- _A screen and keyboard interface with your Raspberry Pi_
- _An SSH connection (optional)_

### 1. Prepare your Raspi
- Flash a microSD card with Raspberry Pi OS (32bit)
- Using the raspi config on an integrated screen, enable camera use:<br>
`sudo raspi-config`<br>
Go to Interfacing Options, and enable camera.

### 2. Set up Github access and clone Bixels files
- SSH into your raspi (if using SSH)
- Update your Raspberry Pi<br>
`sudo apt update`<br>
`sudo apt upgrade`<br>

- Then install git and configure with your Github details:
```
sudo apt install git
git config --global user.name "Your Name"
git config --global user.email "your.name@email.com "
git config --global core.editor nano
git init
```

- On the Bixels Github page (github.com/donora/Bixels), find the Fork button and click it.
You will now have a copy of the repo. You should see a Clone or download button. Clicking this will reveal the uniform resource identifier (URI) of the repo. Copy this, and add it to the ‘git clone’ command as follows (example link):<br>
`git clone https:github.com/donora/Bixels.git`<br>

- Now navigate to your Bixels folder:<br>
`cd Bixels`<br>
...and run the following command:<br>
`sudo chmod +x *`<br>
(You will need to do this any time you re-clone the Github repository. It allows read/write permissions used by the various python scripts.)

### 3. Install libraries
- Run the following commands:
```
sudo pip3 install Adafruit_Python_DHT
sudo apt-get install python3-flask
sudo pip3 install adafruit-blinka
sudo pip3 install rpi_ws281x adafruit-circuitpython-neopixel
sudo python3 -m pip install --force-reinstall adafruit-blinka
sudo pip install matplotlib
sudo apt install matchbox-keyboard
```

### 4. Set up crontab
- Edit the crontab by typing in:<br>
`crontab –e`<br>
and add the following line at the bottom of the file:<br>
`* * * * * sudo /home/pi/Bixels/runbixeldo.sh`<br>
 (save & exit)

- Best to reboot before starting:<br>
`sudo reboot`<br>

### 5. Set up your touchscreen
- After reboot, use the integrated screen rather than SSH (if you were using SSH). There should now be an on-screen keyboard installed (see above) – find it in ‘Accessories’ in the main dropdown menu.
- If your screen is upside down edit the following file:<br>
 `sudo nano /boot/config.txt`<br>
…and add this line at the top:<br>
`lcd_rotate=2`<br>

### 6. Initiate the webserver
- On your Raspi screen, go to the command line and run the following commands:
```
cd Bixels
sudo python3 bixelsettings.py
```
- Then open web browser and navigate to the Raspi's IP address (e.g. 192.168.0.218). This IP will work for any device on the same wifi – the Raspi's screen, a phone, a laptop, etc.

You can now control the Bixels device using the web server. As long as the server is running on the Raspberry Pi, you can access the page from any local device and set up, monitor and end experiments.
