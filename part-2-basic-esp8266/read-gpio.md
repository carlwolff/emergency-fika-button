# Read GPIO state

GPIO is a abbreviation for "General Purpose input/input" ([wiki](https://en.wikipedia.org/wiki/General-purpose_input/output)). Eh...say what?

The idea is that the microcontroller has pins which are available given that somebody makes sure to add this to the mainboard. GPIOs are awesome! It's a low-level connection all the way to the microcontroller which enables us to connect either a switch or a LED to a pin.

The following image shows the all the pins of the ESP8266\. Note that some pins have a notion of "GPIO" but may as well have an extra box specifying pre-defined configuration (green) or alternative configuration (blue).

![esp8266v1](http://cdn.frightanic.com/blog/wp-content/uploads/2015/09/esp8266-nodemcu-dev-kit-v1-pins.png)

So, how does the microcontroller understand that something is connected to a pin? It needs to have a common reference with whatever is connected. That is: subatomic particles (electrons) needs to be able to exit the microcontroller and enter somewhere else.

The common reference is either a 3.3V output (red) or ground/GND.

## Reading pin state (by polling)

We will configure GPIO5 (D1) for use with our switch. Run the following command to tell the ESP8266 how you want pin `1` to be configured.

```lua
> gpio.mode(1, gpio.INPUT, gpio.PULLUP)
>
```

continue by running

```lua
> print(gpio.read(1))
1
>
```

Ok?

`1` is the output, or the current result of the pin when reading its state. Let's connect a wire between GPIO5 and GND, and rerun the command above.

```lua
> print(gpio.read(1))
0
>
```

Result

- `0 = short circuit`: Wire connected from GPIO5 and GND gives as something called a [short-circuit](https://en.wikipedia.org/wiki/Short_circuit). This is the same thing that happens when you lit up you light at home, you allow electrons to flow.
- `1 = open circuit`: No connection from GPIO5 and GND gives something called an [open circuit](https://en.wikipedia.org/wiki/Open-circuit_voltage). When you turn the lights off at home, you break the flow of electrons.

Are we done? Kind of. Reading the state like this becomes tedious over time. Imagine that you create a function that will run over and over (80 MHz ~ 80 million times per second) only to read the state. That's a lot of power going to waste. We call this _polling_ and it definitely has its use-case, but avoid it if possible.

## Reading pin state (by triggering)

Microprocessors, as well as processors, have for a long time had something called an _interupt_. That is an alerting system to tell it to stop with whatever it is currently doing (sleeping?) and poll for an update. Multiple interupts would allow more granular alerting.

The GPIOs of ESP8266 has built in interupts. You know exactly which GPIO that triggered an event. Let's try it!

```lua
> gpio.mode(1, gpio.INT, gpio.PULLUP)
> gpio.trig(1, 'both', function(t)
  print('GPIO5/D1 state is: '..t)
end)
```

Try dis-/connecting the wire. See?

```lua
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 0
GPIO5/D1 state is: 1
```

Awesome! We're done here. (hint: press

<ente> to get back to <code>&gt;</code>)</ente>

# Gotchas

- D0 has no support for interupt.
- De-bouncing is the art of removing duplicate output for the same value. Right now we do not care about it though.
- `0` vs `1` does not necessarily respond to the state of the emergency fika button. If your button is a "normally closed" one, that means that ESP8266 will output `1` when you press the button and `0` otherwise. There's usually a small notion of `NC` or `NO` which specifies its default state.
