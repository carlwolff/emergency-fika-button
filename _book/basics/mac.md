# Install USB-driver

The ESP8266 v1 uses a USB-chip called CP2102 by SiLabs. It's straight forward to install. The driver is required to allow the ESP8266-module to communicate using [emulated serial port](https://en.wikipedia.org/wiki/Serial_port) protocol.

1. Unplug ESP8266
2. Download [driver](https://www.silabs.com/Support%20Documents/Software/Mac_OSX_VCP_Driver.zip) from SiLabs
3. Mount disk image by double clicking the `SiLabsUSBDriverDisk.dmg`. A new windows will pop open.
4. Install driver by double clicking `Silicon Labs VCP Driver.pkg` and follow instructions. You will be asked for your login password during this process.
5. Plugin EPS8266

To verify installation, go to -menu, `About this Mac`, `System Report`, `USB`. You should see `CP2102 USB to UART Bridge Controller` in the list on the right side. If you are not running latest OS X, currently OS X El Capitan, then these steps differs somewhat.

# Install Terminal for Command Input

The NodeMCU firmware will provide us with a prompt (similar to Terminal) on the serial interface we just enabled. What we now need is a tool to display that prompt. To unify the experience in Mac/Windows/Linux we use [PlatformIO IDE](http://platformio.org/platformio-ide).

1. Download [PlatformIO IDE](http://platformio.org/platformio-ide). 
2. Open up `platformio-atom-mac.zip` that you just downloaded, it will result in a new application called Atom.
3. Install `Atom` by dragging the icon to `Applications` in Finder
3. Start Atom and wait for it to settle the installation before continuing.

![image](https://gitlab.com/iot-malmo/emergency-fika-button/uploads/383781f79d5ce590bafc36751dc73847/image.png)
