# Kverneland Bale Wrapper Counter 7593
![7593](images/Kverneland_7593.jpg?raw=true)

This is counter module that is used with a bale wrapper and it was produced by Kverneland, so this is part of an agricultural machine.
I got this unit from a co-worker with the request to have a look, it belongs to a neighbor of his and they already tried to have it repaired by a company that is specialized to do these kinds of repairs.
But they were told that the controller in this unit is dead and that it can not be replaced.

This is what the PCB looked liked when I got it, as beeing part of an agricultural machine it was no surprise that the PCB was rather filthy, so the first thing I had to do was to clean it.
![top_original](images/top_original.jpg?raw=true)
![top_original](images/top_original2.jpg?raw=true)

## Power Up
The first issue I had was powering the unit.
There is a 78L05 next to the fuse holder and a 74HC14N, so identifying GND was not an issue. Then the other contact on the external connector had to be positive and agricultural machines usually have a 12V battery, so they run with 14V like cars.

## First Repair
But supplying the unit with 13V did nothing, it was completely dead and there were no 5V.
I removed the fuse holder in order to trace the connections on the PCB and to find out how the battery supply is connected to the linear regulator.
To my surprise I found the first fault, the very small trace leading to the fuse holder rotted away directly at the fuse holder via.
Unfortunately I did not take a foto of the PCB with the fuse holder removed.
![top_original](images/bot_first_repair.jpg?raw=true)
![top_original](images/bot_first_repair2.jpg?raw=true)

So if your unit is completely dead, check for continuity between the points the short red cable is bridging.

## Reverse Enginering
Now that the 5V supply was working, the board started to actually do something, the LEDs blinked and about a third of the segments of the LCD got switched on.
At this point it looked like the LCD is defective.
So I started to reverse engineer a schematic from the PCB and one of the first things I found out was that the LEDs are controlled directly by the PIC16C57 on the board.

I traced the connections and took a whole lot more fotos.
![top_2](images/top_2.jpg?raw=true)
![top_detail](images/top_detail.jpg?raw=true)
![bot_2](images/bot_2.jpg?raw=true)

At some point I shifted the light guard under the display far enough to identify one of the chips under the LCD, 74HC164N, this is a 8-bit serial-in parallel-out shift register.
With this I had a pinout and under the assumption that all six chips under the LCD are the same I worked out more of the schematic.
So the LCD is a six digit seven-segment static type with 50 pins and pin 1 is the common pin.
I found and ordered what looked like a good replacement part: VI-602-DP-RC-S - unfortunately it is not a direct match.
At this point I connected a logic-analyzer to the first shift register and tried to measure the signales - but the measurements where all over the place but definately not clearly defined digital.

![top_lcd_removed](images/top_lcd_removed.jpg?raw=true)
![top_chips_removed](images/top_chips_removed.jpg?raw=true)
![bot_chips_removed](images/bot_chips_removed.jpg?raw=true)

My first instinct was to just cut out the LCD and the chips as I usually do with repairs but I decided to try to remove the LCD without damaing it as there was no way to cut the pins without breaking the glas.
I also removed the shift registers like this as to be able to examine these later.

## Second Repair
At this point I got impatient though and just soldered in the replacement chips I got since these did only cost around 60 cents each anyways.

![top_chips_replaced](images/top_chips_replaced.jpg?raw=true)

Then I tried to put in the VI-602-DP-RC-S that I got as replacment and found out that the pins on this one are not long enough.
Now I was indeed glad that I did not destroy the original LCD.

I put in the original LCD without soldering and to my surprise it worked, the unit cycled thru a couple of things displayed, the LEDs just where lit continously and using the buttons changed what was displayed - success.

So for some reason the shift registers went bad.

The other component that I replaced was on the 8x4k7 resistor networks. Not because it was defective, but because I needed to remove it from the top side in order to move the light guard under the LCD. This is why it goes from top to bottom and back in the images - after some abuse from desoldering I finally used a new part though.

## Up and running again
And here it is up and running again:
![top_repairedl](images/top_repaired.jpg?raw=true)

Before assembly I sprayed the PCB with protective coating to give the unit a better chance to witstand the harsh conditions in the agricultural environment for at least another ten years.

## Conclusion
This was a fun thing to do.
I even checked the possibilty to replace the controller but this would have meant to write a new software and I am still not 100% certain that I understood what it is supposed to do in detail.

At some point I even thought about replacing the PCB entirely, the design can be definately made more robust and using more modern components this should be not really a challenge.
But well, I am not into selling electronics and there probably is no market for these things anyways.

I have more images and in higher resolution as well, if anyone is interested.
