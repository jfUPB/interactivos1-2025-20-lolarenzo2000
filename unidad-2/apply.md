# Unidad 2


## 🛠 Fase: Apply


``` py
from microbit import *
import utime
import music

Init = 0
Config = 1
Armed = 2
Exploded = 3

state = Init

fuse = 0
startT = 0

once = True

while True:
    if state == Init:
        once = True
        uart.write('Init|')
        fuse = 20000
        state = Config
        uart.write(str(int(fuse/1000))+"|")
    elif state == Config:
        display.show(Image.TRIANGLE)
        if button_a.was_pressed():
            if not(fuse + 1000 > 60000):
                fuse += 1000
            uart.write(str(int(fuse/1000))+"|")
        elif button_b.was_pressed():
            if not(fuse - 1000 < 10000):
                fuse -= 1000
            uart.write(str(int(fuse/1000))+"|")
        elif accelerometer.was_gesture('shake'):
            state = Armed
    elif state == Armed:
        uart.write('Armed|')
        while fuse > 0:
            display.show(Image.DIAMOND)
            if utime.ticks_diff(utime.ticks_ms(),startT) > 1000:
                startT = utime.ticks_ms()
                fuse -= 1000
                uart.write(str(int(fuse/1000))+'|')
        state = Exploded
    elif state == Exploded:
        if once:
            once = False
            uart.write('Kaboom|')
            display.show(Image.invert(Image.DIAMOND))
            music.play(music.WAWAWAWAA)
        if pin_logo.is_touched():
            state = Init
    else:
        display.show(Image.DUCK)
```

