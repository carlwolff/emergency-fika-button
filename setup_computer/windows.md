# Install USB-driver

The ESP8266 v1 uses a USB-chip called CP2102 by SiLabs. It's straight forward to install. The driver is required to allow the ESP8266-module to communicate using [emulated serial port](https://en.wikipedia.org/wiki/Serial_port) protocol.

1. Unplug ESP8266
2. Download [driver](https://www.silabs.com/Support%20Documents/Software/CP210x_Windows_Drivers.zip) from SiLabs
3. Unzip file and open directory
4. Run either `CP210xVCPInstaller_x64.exe` (most common today) or `CP210xVCPInstaller_x86.exe` installer script depending on your CPU-architecture.
5. Plugin EPS8266

To verify installation, open `Device Manager` and unfold `Ports`.  If there's a notion of CP210x, then your driver is installed.

# Install terminal for command input

The NodeMCU firmware will provide us with a prompt (similar to DOS/Powershell) on the serial interface we just enabled. What we now need is a tool to display that prompt. To unify the experience in Windows/Mac/Linux we use [PlatformIO IDE](http://platformio.org/platformio-ide).

1. Download [PlatformIO IDE](http://platformio.org/platformio-ide). 
2. Open up `platformio-atom-windows.exe` that you just downloaded.
3. Start Atom and wait for it to settle the installation before continuing. 