# Teardown of the LaPochée（ラポッシュ）digital camera module

The Lapochée is a digital camera module accompanying the THZ43 Chiaro mobile phone released in May 1999 by Tu-Ka mobile phone company and operator (then merged in KDDI Corporation). Both phone and camera module were made by Mitsubishi. This is technically the **first mobile phone equipped with a digital camera** (and among the first low-end market digital cameras too) so it kind of belong to history.

Fun fact, "LaPochée" is probably a name designed to sound cute and French but it means nothing in French apart an approximate translation of "The pocket" ("La Poche").

The LaPochée camera module acquired a certain celebrity in the niche Game Boy nerds community as it shows a potential hardware filiation with the Game Boy Camera according to various Mitsibishi sources frome 1999-2000. It might or might not share the same analog light sensor from the M6428X series. I tried to find this camera module for years. By the time, addict to old electronic stuff I landed on some M64283FP sensors from factory (possibly used in the LaPochée) by pure luck and published [Arduino codes codes to drive them](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor). The M64283FP sensor is basically a Game Boy Camera M64282FP sensor with more functions and the same shitty datasheet. You will see why I insist on this sensor later.

I finally got the Lapochée camera module in March 2025 thanks to a local contact in Japan (see aknowledgments). The device was advertised as electronic junk but in pristine state according to seller images. It was delivered in its factory plastic bag still with the protective film on front face. Sadly for me, the display was burnt beyond repair (both the polarizer and the liquid crytal part were completely dark). This is common with Japanese product and due to overheating. I do not own the user manual but I am in search for it.

But I guess you landed here for some good old vintage electronic porn and not to see a draw my life.

# Pictures from the outside / inside and comments

![](/Pictures/Lapochée_2.JPG)
The device exudes the 2000s with its white round design anf the touch of blue plastic.

![](/Pictures/Lapochée_side.JPG)
The right side features the on/off button and a contrast thumbwheel for the display. The device has no LED or speaker / buzzer to indicate its state. It's completely mute. Mine shows no sign of life due to defective display.

![](/Pictures/Lapochée_bottom.JPG)
The bottom shows the communication port with the mobile phone. The port is a 8 pins something that I cannot identify. It's not a common plug.

![](/Pictures/Lapochée_rear_2.JPG)
The back side shows the battery compartment and a 3 positions stand. Not sure why the stand is longer than the device itself. Design I guess...

![](/Pictures/Lapochée_rear_open.JPG)
![](/Pictures/Lapochée_2xAAA_batteries.JPG)
The device works with 2xAAA batteries which was a very fancy habit before the flooding of market with shitty lithium batteries. Because yes, we were yet able to use AAA rechargeable batteries (and reuse them elsewhere) in these old times. PDZ43 must be the Mitsubishi factory name of the LaPochée module.

![](/Pictures/Lapochée_main_board_with_LCD_mounted.JPG)
![](/Pictures/Lapochée_head_assembly_2.JPG)
The device opens by removing four annoying 3-wings screw similar to any Nintendo products from that era. The rotating head itself has two similar screws. I guess this was a common trick in Japan to discourage user to sneak inside electronic products.

![](/Pictures/Lapochée_empty_head_2.JPG)
You can easily go further in the head assembly / disassembly if you are familiar with the Game Boy Camera. It feel better than a Game Boy Camera thanks to two prongs on the metal ring that safely position the head in normal or selfy position. The design is more refined, while very similar. The sensor ribbon socket is smaller than the Game Boy Camera (must be a JST connector with 1 mm pitch).

![](/Pictures/Lapochée_PCB_front.JPG)
At this step removing the main PCB is very easy. The front side mainly features a Mitsubishi M64916FP chip. Although sharing the numbering of Mitsubishi chips (FP termination seems to be used for home appliance, M64 is a common prefix of several Mitsubishi chips), this chip is not documented anywhere. By tracing some connections I conclude that this is probably a custom driver chip for the LCD display and not a kind of MAC-GBD like chip driving the sensor.

![](/Pictures/Lapochée_serial_8_pins_connection.JPG)
Some details of the bottom serial connector. It's not a socket I know, maybe something custom.

![](/Pictures/Lapochée_main_board_with_LCD.JPG)
![](/Pictures/Lapochée_PCB_rear.JPG)
The rear side contains all the meat: LCD assembly, flash memory and main MCU. The flash memory is a 4MB / 3.3V only [M5M29KB800](/Datasheets/Renesas_M5M29KB.PDF) from Mitsubishi, commonly used in mobile phones from that era. The MCU is a 10 MHz 16-bit [M30610MCA](/Datasheets/Renesas_M5M29KB.PDF) microcontroller, also from Mitsubishi. The marking indicates that this is a 128 KB ROM, 10 KB RAM, mask ROM version 282. Pins are 5V tolerant. This MCU also has several 10 bits analog to digital converters so I guess the sensor is directly driven by this chip, nothing else is required. 

The last noticeable chip is a Sharp [IR3E05](/Datasheets/Sharp_IR3E05.pdf). The only information I can find is that the chip is a divided voltage generator for LCD drive, so the chip that send the high voltage signal to the display individual pixels to twist more or less the liquid crystals. This indicates that the LCD can display several gray levels.

![](/Pictures/Lapochée_LCD_front_with_bracket_and_damper.JPG)
![](/Pictures/Lapochée_LCD_rear.JPG)
The display assembly is very easy to dismount and neatly designed. The LCD is a 128x128 pixels Sharp M1128CP with a 22 pins ribbon connector. I do not find any reference for this display. Mine is defective and stay completely dark even with the polarizer removed. I have very thin hope to find a replacement or a compatible one due to the absence of datasheet for both the LCD and the M64916FP driver chip. They both can be totally custom for this device.

![](/Pictures/Lapochée_lens_front.JPG)
![](/Pictures/Lapochée_lens_rear.JPG)
The lens used is very similar to the Game Boy Camera one with a screw mount to adjust focus in factory.

![](/Pictures/Lapochée_sensor_PCB_ribbon.JPG)
The sensor uses a 9 wires connections. 

![](/Pictures/Lapochée_sensor_PCB_rear.JPG)
![](/Pictures/Lapochée_sensor_PCB_front.JPG)
The PCB comprises two caps and one inductance, similar to the Game Boy Camera. I guess this is exactly the same electrical circuit.

![](/Pictures/Lapochée_sensor_reference.png)
A quick look under a powerfull microscope shows that this is a 128x128 pixels [M64283FP](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor) sensor, successor of the M64282FP sensor used in the Game Boy Camera. A quick look at the front of the PCB shows that STRB and TADD pins which allows access to advanced functions, are just not connected. As the Lapochée module is advertised as taking [96x96 pixels images](https://pc.watch.impress.co.jp/docs/article/990413/tu_ka.htm) (1 bpp or 2 bpp), this implies that images are cropped by software and not by using the random access mode of the sensor.

Without any way of firing the device, I cannot investigate more.

# Credits
Please credit any image you publish / reuse from this repository like this: **Raphaël BOICHOT, 2025**. And give a link to this repository.

# Acknowledgements
- Author want to thank **Frédéric Mercier** for the finding of the Lapochée camera module on Mercari in Japan.
- Thanks also to Razole for providing me some factory sealed M64283FPs from under the counter.
