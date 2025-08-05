# Unidad 2


## 🛠 Fase: Apply


``` py
from microbit import *
import utime

Init = 0
Config = 1
Armed = 2
Exploded = 3

state = Init

fuse = 0
startT = 0

while True:
    if state == Init:
        
        fuse = 20000
        state = Config
    elif state == Config:
        if button_a.was_pressed():
            if not(fuse + 1000 > 60000):
                fuse += 1000
            uart.write(str(fuse)+"|")
        elif button_b.was_pressed():
            if not(fuse - 1000 < 10000):
                fuse -= 1000
            uart.write(str(fuse)+"|")
        elif accelerometer.was_gesture('shake'):
            state = Armed
    elif state == Armed:
        while fuse > 0:
            display.show(Image.DIAMOND)
            if utime.ticks_diff(utime.ticks_ms(),startT) > 1000:
                startT = utime.ticks_ms()
                fuse -= 1000
        state = Exploded
    elif state == Exploded:
        if pin_logo.is_touched():
            state = Init
    else:
        display.show(Image.DUCK)
```
