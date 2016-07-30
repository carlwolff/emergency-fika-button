# Connect to WiFi

Prerequisites:

- WiFi-access point with WPA2-personal (most common configuration)
- SSID and password for WiFi

## Connect to wifi and get an IP-address

Show current IP-address on screen

```lua
> print(wifi.sta.getip())
nil
>
```

It seems like we don't have an IP-address yet. That's good! We haven't told our chip about our wifi configuration. So, let's do it!

The chip can behave as access point (in most scenarios, a part of your router at home) or client. The latter is what we want it to be, a simple device connected to pre-existing infrastructure. We already have an access point available (your router).

Tell the chip to go into wifi client (station!) mode by

```lua
> wifi.setmode(wifi.STATION)
>
```

Nothing will be returned as noted by a new `>`.

Even if we already know the network we want to connect to, we can display nearby networks for verbosity. Of course, it could also help if you're unsure of the range of your wifi.

```lua
> function listap(t)
    for k,v in pairs(t) do
        print(k.." : "..v)
    end
end
>
```

Lua is asyncronous, similar to javascript, and will return when it has assembled a result. When running `wifi.sta.getap(1, listap)` you will the result within a few seconds. Be patient.

```lua
> wifi.sta.getap(1, listap)
> bc:ee:7b:55:5f:d2 : T-800,-73,3,3
80:37:73:df:df:c1 : ComHemDFDFBD,-84,3,1
ae:22:0b:e9:a1:dc : iotmalmo,-68,3,11
cc:b2:55:d4:a9:29 : Lorgonet,-94,3,6
28:10:7b:8e:42:a6 : YaStNetwork,-81,4,5
34:08:04:dc:26:dc : SOFIAS,-91,4,10
```

To connect, we now need to configure the chip with our SSID (wifi network name) and password.

```lua
> wifi.sta.config("iotmalmo","iotmalmo123")
>
```

As you might know, sometimes a connection takes a little bit longer than you would expect, so even if you print the IP-address again it might still be `nil`.

```lua
> print(wifi.sta.getip())
nil
> print(wifi.sta.getip())
10.0.1.86       255.255.255.0   10.0.1.1
>
```

We got IP, subnet mask and router ip – **wohoo, we're online!!**

# References

- [NodeMCU wifi-documentation](http://nodemcu.readthedocs.io/en/master/en/modules/wifi/)
