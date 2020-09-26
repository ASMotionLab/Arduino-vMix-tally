# Arduino vMix tally

This project contains the firmware for a tally system based on an Arduino esp8266 and the vMix TCP API. 
Pictures of the tally can be found in the Pictures folder.

This fork adapts the existing project by Thomas Mout to work with a single WS2812B (Neopixel) led shield instead of the original LED matrix shield. Multiple WS2812B leds will also work.

There are modifications to change LED brightness from the setup web page, and a factory reset button to load defaults.

The enclosure has also been redesigned to fit the dev board + shield, to retain it, to allow mounting to a 1/4 tripod screw via a 3/8 adaptor boss.

## Installation

### Hardware

This fork uses a WeMos/Lolin D1 Mini clone
https://www.banggood.com/Geekcreit-D1-mini-V2_2_0-WIFI-Internet-Development-Board-Based-ESP8266-4MB-FLASH-ESP-12S-Chip-p-1143874.html
and a WS2812B (Neopixel) shield.
https://www.amazon.co.uk/ILS-WS2812B-RGB-Shield-Mini/dp/B079128452

The 2 are soldered together, leaving clearance the thickness of a stanley blade between the D1 mini and the shield.

The 3d printable enclosure is designed to retain this board sandwich with a tight tolerance.

The 'lens' used to diffuse the led is a 2cm diameter frosted acrylic circle (3mm thickness). It should press into the case if your printer is accurately calibrated.

#### Solder instructions

Make sure to match the board orientation when soldering the D1 and shield - make sure 3v3 goes to 3v3, 5v to 5v, etc etc.

### Software

#### 1. Install Arduino IDE

Download the Arduino IDE from the [Arduino website](https://www.arduino.cc/en/main/software) and install it.  
After the installation is complete go to File > Preferences and add http://arduino.esp8266.com/stable/package_esp8266com_index.json to the additional Board Manager URL.
Go to Tools > Board > Board Manager, search for *esp8266* and install the latest version.
After the installation go to Tools > Board and select *Wemos D1 R2* as your default board.  

#### 2. Copy libraries

All libraries included in the Libaries folder are required for this project. Please copy them to your own Arduino libraries folder (default path: *user/documents/Arduino/libraries*).
If some components are missing, you can easily find what's missing by googling the error.

#### 3. Uploading static files

Connect the Arduino to the computer with a USB cable.  
The static files in the Arduino-vMix-Tally/data folder must be uploaded using the Tools > ESP8266 Sketch Data Upload in the Arduino IDE.  

#### 4. Uploading firmware

Upload the Arduino-vMix-Tally/Arduino-vMix-Tally.ino from this repository to the D1 mini

#### 5. Connecting to your wireless network

To start with, the tally will try to connect to a non existent wifi network and will fail. After it fails, it becomes a wifi access point.
You can connect directly to it. It'll be called "vMix_Tally_X" where X is a number. The WiFi password is the same name, with "_access" added to the end._
So If the Access Point name is vMix_Tally_255, the password will be vMix_Tally_255_access.

Once you connect to it, navigate to address 192.168.4.1 in the browser and enter the details of your wifi network, the ip address of the vMix machine, which tally number it is and the LED brightness you want.

Hit Save. Tally restarts.

#### 5. Connecting to vMix

If all the details are right and vMix is running, it should light up blue and after 5-30s either turn off, go green or red.
vMix API runs on port 8099, so this port needs to be reachable by the tally - make sure firewall isn't blocking it.

#### 6. Colours

BLUE light indicates the tally is trying to connect to a network, or it's an Access Point of it's own.

OFF means the camera is not being previewed and it's not live (but vMix connection is working).

GREEN means the camera is being previewed (vMix connection is working).

RED means the camera is LIVE (vMix connection is working).

## Things to keep in mind

1. Make sure to use a power cable that does not support data when using a USB port on a camera. This can cause connecting issues in the camera.  
2. The D1 mini is completely dependent on a good WiFi signal.  
3. The tally must be connected to the same network as the vMix instance.
4. If you're having trouble setting up the tally, open a serial monitor with baud 9600 on the tally's COM port it will give you information about what it's doing.

## Footnote

Please note all images are for illustration purpose. Actual results may vary.  
Feel free open issues on this repository for bugs or feature requests.  
If you want to create your own version of this repository then a reference is appreciated.  
