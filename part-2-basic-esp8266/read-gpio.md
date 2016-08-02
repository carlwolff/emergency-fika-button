# Read GPIO state

GPIOs are awesome! It's a low-level connection all the way to the machine (SoC) which enables us to connect simple, slow, things like a switch or a LED.

## Longer Intro to GPIO

GPIO is a abbreviation for "General Purpose input/input" ([wiki](https://en.wikipedia.org/wiki/General-purpose_input/output)). Eh...what? The greyish chip is a system-on-chip (SoC); a bunch of components that's needed to build a computer as well as some additional stuff such as wifi.

![](/assets/esp8266-pinout1.png)

So, how does the microcontroller understand that something is hooked up to a pin and can be controlled/read? It needs to have a common reference with whatever is connected. That is: subatomic particles (electrons) needs to be able to exit at one pin and re-enter at another.

The common reference is either a 3.3V output (red) or ground/GND. In the case of GND, you can make a shared ground between two different ESP8266 of if you like for some reason.

## Short Intro to GPIO on ESP8266

The following image shows the all the pins of the ESP8266. Note that some pins have a notion of "GPIO" but may as well have an extra box specifying pre-defined configuration (green) or alternative configuration (blue).

![esp8266v1](http://cdn.frightanic.com/blog/wp-content/uploads/2015/09/esp8266-nodemcu-dev-kit-v1-pins.png)

## Reading pin state by polling

We will configure D1 (GPIO5) for our use. Run the following two commands to tell the ESP8266 that you want to use `D1` as input and that you want to read the value

```lua
> gpio.mode(1, gpio.INPUT, gpio.PULLUP)
> print(gpio.read(1))
1
>
```

The output, `1`, is the result of reading from GPIO pin 1 (`D1/GPIO5`) given current situation. If we connect a wire between GPIO5 and GND, and rerun the command above, we should get another result

```lua
> print(gpio.read(1))
0
>
```

Result

- `0 = short circuit`: Wire connected from GPIO5 and GND gives as something called a [short-circuit](https://en.wikipedia.org/wiki/Short_circuit). This is the same thing that happens when you lit up you light at home, you allow electrons to flow.
- `1 = open circuit`: No connection from GPIO5 and GND gives something called an [open circuit](https://en.wikipedia.org/wiki/Open-circuit_voltage). When you turn the lights off at home, you break the flow of electrons.

Are we done? It depends. Reading the state like this becomes tedious over time. Imagine that you create a function that will run `read` over and over (multiple times per second). That's a lot of power going to waste. It is called _polling_ and it definitely has its use-case, but should be avoided if possible due to the ineffiency.

## Reading pin state (by triggering)

Processors have for a long time had something called an _interupt_. That is an alerting system to tell it to stop with whatever it is currently doing (sleeping?) and go to a predefined place to execute code before returning to whatever it was doing. You could either run code to find out what was triggering the interupt and then poll for the actual value, or if you have support for multiple interupts, just run arbitary code.

All the GPIOs of ESP8266 has built in interrupts. You know exactly which GPIO-pin that triggered an event. We will now tell the ESP8266 that we want to listen for changes on D1/GPIO5 and, in case of trigger, run an (anonymous) function that prints the new state.

```lua
> gpio.mode(1, gpio.INT, gpio.PULLUP)
> gpio.trig(1, 'both', function(t)
  print('GPIO5/D1 state is: '..t)
end)
```

Try dis-/connecting the wire a couple of times. See?

```lua
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 1
```

Awesome! We're done here. (hint: press `<enter>` to get prepare for the input of next command.

---

## Gotchas

- D0 has no support for interupt.
- De-bouncing is the art of removing duplicate output for the same value. Right now we do not care about it though.
- `0` vs `1` does not necessarily respond to the state of the emergency fika button. If your button is a "normally closed" one, that means that ESP8266 will output `1` when you press the button and `0` otherwise. There's usually a small notion of `NC` or `NO` which specifies its default state.
