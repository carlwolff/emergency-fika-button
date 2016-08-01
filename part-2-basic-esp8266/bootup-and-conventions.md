# Bootup and Code Conventions

## Connect to module

Start the application Atom (which contains PlatformIO IDE).

We want to use PlatformIO to bring up the terminal of the ESP8266\. Ensure that the module is connected and then click the Power Connector-button in the toolbar.

![PlatformIO-home](/uploads/9072279df7ce88effa0547e79321dd8d/PlatformIO-home.png)

Set baud rate to 115200 and then select port. The port will differ on every operating system but on Mac it contains the text "CP2102 at /dev/cu.SLAB_USBtoUART". On Windows it might be something such as "COM3" and Linux will most probably be "/dev/ttyUSB0".

![PlatformIO-serialconfig](/uploads/bb5501fd51d488d3a3afd346c3da3d1a/PlatformIO-serialconfig.png)

When done, click `Start`.

## Verify that module is running NodeMCU

Press the `RST` button the module itself. It will reboot and text should be printed in the terminal.

```
> rl␀l��|␀�l�|␂␌␌␌�␌l�␌b|��␂�␒�r�b�␌b��nn�lnn���␌b␜p�lrlrlp�n�␐␂␌␌�␌l␌␌␌␌␌␌b␌n�|␂�␌␌쌎b��nn�␀l��l`␂�␒␒nn␌�␎l␎␂nr���n␌␌⒒`␂p�n�␐␂␌␌r�����␌␌␌␌b␌n�|␂���␌�
b��nn�␀␌�l`␂�␒␒nnl�l`␂␎␂nr���n␌␌�␒�`␂`�n␌␌␌��b�nl�␌��nn�␀␌�␎lp�n�␐␂␌␌r�����␌�␂␌b␌n�|␂␌␌b��nn�␀l�␌l`␂�␒␒nn␌l`␂␎␂nr���n␌␌���`␂␎r��n␌␌���`␂don't use rtc
mem data
rl���

NodeMCU custom build by frightanic.com
        branch: dev
        commit: 244c6e9db1b6643dc5ac1a96c758cec00d1178d8
        SSL: true
        modules: bit,cjson,dht,enduser_setup,file,gpio,http,mqtt,net,node,ow,spi,tmr,uart,wifi
 build  built on: 2016-06-12 21:14
 powered by Lua 5.1.4 on SDK 1.5.1(e67da894)
lua: cannot open init.lua
```

The first part is garbage that comes from the fact that the module changes baud rate during reboot but also from the interupted connection.

## The Lua terminal

When lua, the "operating system" of your newly flashed module, is waiting for its next command it will display `>`.

While typing in the lua command line you might end up with `>>`. This means that lua expects you to continue on whatever you wrote the line before. You can get out this by failing the command intentionally

```
> hello
>> ..
stdin:2: '=' expected near '..'
>
```

## Code Examples Conventions in This Book

When you see a code example beginning as

```lua
>
```

this means that the command should be written at the lua-prompt of a ESP8266 running NodeMCU (this entire chapter).

When you see a code example beginning with the dollar symbol

```bash
$
```

then it means that the command should be written at the command line prompt of your mac/linux/unix computer. If your running Windows, you _might_ be out of luck or on your own but I will do my best to cover this scenario as well.

--------------------------------------------------------------------------------

## Gotchas

- Copy-n-paste to lua terminal over serial might break from time to time. Retry a couple of times if needed. When retrying, first get rid of double `>>`.
- When you paste a multi-line snippet the NodeMCU might not always get all the characters and will complain. Get back to a single `>` and try again (a few times if needed).
