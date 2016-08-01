# Hello World

This example includes the result of your command (`print...`) as well as the "waiting for next input" (`>`) that will show up after almost every command. If you don't see it, press enter and it should show up.

```lua
> print("Hello".." ".."World")
Hello World
>
```

What we did was:

1. Ask lua to concatenate the three strings `Hello`, `<space>` and `World`.
2. Tell lua that we want the result of the concatenated strings printed to screen

---

## Gotchas

- Copy-n-paste to lua terminal over serial might break from time to time. Retry a couple of times if needed. When retrying, first get rid of double `>>`.
