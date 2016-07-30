# Hello World

Start the application Atom (which contains PlatformIO IDE).

We want to use PlatformIO to bring up the terminal of the ESP8266\. Ensure that the module is connected and then click the Power Connector-button in the toolbar.

![PlatformIO-home](/uploads/9072279df7ce88effa0547e79321dd8d/PlatformIO-home.png)

Set baud rate to 115200 and then select port. The port will differ on every operating system but on Mac it contains the text "CP2102 at /dev/cu.SLAB_USBtoUART". On Windows it might be something such as "COM3" and Linux will most probably be "/dev/ttyUSB0".

![PlatformIO-serialconfig](/uploads/bb5501fd51d488d3a3afd346c3da3d1a/PlatformIO-serialconfig.png)

When done, click `Start`.

## Verify that module is running NodeMCU

Press the `RST` button the module itself. It will reboot and text will be printed in the terminal.

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

The first part is obviously junk that comes from the fact that the module changes baud rate during reboot but also from the interupted connected.

When lua is waiting for its next command it will display `>`. While typing in the lua command line you might end up with `>>`. This means that lua expects you to continue on whatever you wrote the line before. You can cancel this by failing the command.

```
> hej
>> ..
stdin:2: '=' expected near '..'
>
```

## Hello World

Write (but omit the initial `>`)

```lua
> print("Hello".." ".."World")
```

I will include the result in this snippet as well as the "waiting for new input" (`>`)

```lua
> print("Hello".." ".."World")
Hello World
>
```

What we did was:

1. Ask lua to concatenate the strings `Hello`, `<space>` and `World`.
2. Tell lua that we want the result of the concatenated strings printed to screen

# Gotchas

- Copy-n-paste to lua terminal over serial might break from time to time. Retry a couple of times if needed. When retrying, first get rid of double `>>`.
