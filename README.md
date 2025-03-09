# Teardown of the LaPochée（ラポッシュ）digital camera module

The **Lapochée** is a digital camera module accompanying the THZ43 Chiaro mobile phone released in May 1999 by the Tu-Ka mobile phone company and operator (then merged in KDDI Corporation). Both phone and camera module were made by Mitsubishi. This was technically the **first case of mobile phone equipped with a digital camera** (and among the first low-end market digital cameras too).

Fun fact, "LaPochée" is probably a name designed to sound cute and French but it means nothing in French apart an approximate translation of "The pocket" ("La Poche"). And it sounds a bit off in French.

The LaPochée camera module acquired a certain celebrity in the Game Boy Camera nerds community as it shows a potential hardware filiation with the Game Boy Camera according to various Mitsibishi sources frome 1999-2000. It might or might not share the same analog light sensor from the M6428X series. I tried to find this camera module for years. By the time, addict to old electronic stuff I landed on some M64283FP sensors from factory (possibly used in the LaPochée) by pure luck and published [Arduino codes codes to drive them](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor). The M64283FP sensor is basically a Game Boy Camera M64282FP sensor with more functions, but pin compatible. You will see why I insist on this sensor later.

I finally got the Lapochée camera module in March 2025 thanks to a local contact in Japan (see aknowledgments). The device was advertised as electronic junk but in pristine state according to seller images. It was delivered in its factory plastic bag still with the protective film on front face ([click here for some ASMR](/Pictures/Lapochee_ASMR.mp4)). Sadly for me, the LCD display was burnt beyond repair (both the polarizer and the liquid crystal panel were completely dark). This is common with old Japanese electronic products and due to overheating. 

I do not own the user manual but I am in search for it (feel free to contact me if you have one).

But I guess you landed here for some good old vintage electronic porn and not to read a draw my life. Her we go.

# Pictures from the outside / inside and comments

![](/Pictures/Lapochee_2.jpg)
The device exudes the 2000s with its white round design anf the touch of blue plastic.

![](/Pictures/Lapochee_side.jpg)
The right side features the on/off button and a contrast thumbwheel for the display. The device has no LED or speaker / buzzer to indicate its state. It's completely mute. Mine shows no sign of life due to defective display.

![](/Pictures/Lapochee_bottom.jpg)
The bottom shows the communication port with the mobile phone. The port is a 8 pins something that I cannot identify. It's not a common plug.

![](/Pictures/Lapochee_rear_2.jpg)
The back side shows the battery compartment and a 3 positions stand. Not sure why the stand is longer than the device itself. Design I guess...

![](/Pictures/Lapochee_rear_open.jpg)
PDZ43 must be the Mitsubishi factory name of the LaPochée module. I guess it references to the user manual I do not own.

![](/Pictures/Lapochee_2xAAA_batteries.jpg)
The device is supposed to work with 2xAAA batteries which was a very fancy norm before the flooding of market with shitty lithium batteries. Because yes, we were yet able to use AAA rechargeable batteries (and reuse them elsewhere) in these old times.

![](/Pictures/Lapochee_main_board_with_LCD_mounted.jpg)
The device opens by removing four annoying 3-wings screw similar to any Nintendo products from that era. I guess this was a common trick in Japan to discourage user to sneak inside electronic products.

![](/Pictures/Lapochee_head_assembly_2.jpg)
The rotating head itself has two similar screws to remove in order to see the inside. Similarity with the Game Boy camera is immediately striking.

![](/Pictures/Lapochee_empty_head_2.jpg)
You can easily go further in the head assembly / disassembly if you are familiar with the Game Boy Camera. It feel better than a Game Boy Camera thanks to two prongs on the metal ring that safely position the head in normal or selfy position. The design is more refined, while very similar. The sensor ribbon socket is smaller than the Game Boy Camera (must be a JST connector with 1 mm pitch).

![](/Pictures/Lapochee_PCB_front.jpg)
At this step removing the main PCB is very easy. The back side mainly features a Mitsubishi M64916FP chip and an oscillating crystal (6.898594 MHz probably). Although sharing the numbering of Mitsubishi chips (FP termination seems to be used for home appliance, M64 is a common prefix of several Mitsubishi chips), this chip is not documented anywhere. By tracing some connections I conclude that this is probably a custom driver chip for the LCD display and not a kind of MAC-GBD like chip driving the sensor.

![](/Pictures/Lapochee_serial_8_pins_connection.jpg)
Some details of the bottom serial connector with the plastic plug removed. It's not a common socket from that era. It features 8 pins.

![](/Pictures/Lapochee_main_board_with_LCD.jpg)
Front side of the PCB with the LCD mounted on brackets. A black rubber damper ensure a very tight fit within the shell in case of shock. The LCD assembly can be easily removed from the main PCB by just unclipping it. Nothing is glued. It is clearly meant to be repairable.

![](/Pictures/Lapochee_PCB_rear.jpg)
The front PCB side (below the LCD display) contains all the meat: LCD assembly, flash memory and main MCU. The flash memory is a 4MB / 3.3V only [M5M29KB800](/Datasheets/Renesas_M5M29KB.PDF) from Mitsubishi, commonly used in mobile phones from that era. The MCU is a 7 to 10 MHz 16-bit [M30610MCA](/Datasheets/Renesas_M5M29KB.PDF) microcontroller, also from Mitsubishi. The marking indicates that this is the 128 KB ROM, 10 KB RAM, mask ROM version 282. This MCU also has several 10 bits analog-to-digital converters (A/C) so I guess the sensor is directly driven by this chip, nothing else is required. 

The last noticeable chip is a Sharp [IR3E05](/Datasheets/Sharp_IR3E05.pdf). The only information I can find is that the chip is a divided voltage generator for LCD drive, so the chip that sends the high voltage signal to the display individual pixels to twist more or less the liquid crystals. This indicates that the LCD can display several gray levels.

![](/Pictures/Lapochee_LCD_rear.jpg)
The display assembly is very easy to dismount and neatly designed. The LCD is a 128x128 pixels Sharp M1128CP with a 22 pins ribbon connector, probably manufactured in March 1999. I do not find any datasheet for this display. Mine is defective and stay completely dark even with the polarizer removed. I have very thin hope to find a replacement or a compatible one due to the absence of datasheet for both the LCD and the M64916FP driver chip. They both can be totally custom for this device.

![](/Pictures/Lapochee_lens_front.jpg)
![](/Pictures/Lapochee_lens_rear.jpg)
The lens used is very similar to the Game Boy Camera one with a screw mount to adjust focus in factory.

![](/Pictures/Lapochee_sensor_PCB_ribbon.jpg)
The sensor uses a 9 wires connections. 

![](/Pictures/Lapochee_sensor_PCB_rear.jpg)
![](/Pictures/Lapochee_sensor_PCB_front_M64283FP.jpg)
The PCB comprises two caps and one inductance, similar to the Game Boy Camera. I guess this is exactly the same electrical circuit. The two round test pads are connected to STRB and TADD pin (see next). Strangely enough, the TADD pin has solder residues (maybe accidental).

![](/Pictures/Lapochee_sensor_reference.png)
A quick look under a powerfull microscope shows that this is a 128x128 pixels [M64283FP](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor) sensor, successor of the M64282FP sensor used in the Game Boy Camera. A quick look at the front of the PCB shows that STRB and TADD pins which allows access to advanced functions, are just not connected. As the Lapochée module is advertised as taking [96x96 pixels images](https://pc.watch.impress.co.jp/docs/article/990413/tu_ka.htm) (1 bpp or 2 bpp), this implies that images are cropped by software and not by using the random access mode of the sensor.

Without any way of firing the device, I cannot investigate more.

# Credits
Please credit any image you publish / reuse from this repository like this: **Raphaël BOICHOT, 2025**. And give a link to this repository.

# Acknowledgements
- Author want to thank **Frédéric Mercier** for the finding of the Lapochée camera module on Mercari in Japan.
- Thanks also to Razole for providing me some factory sealed M64283FPs from under the counter.
