# Teardown of the LaPochée（ラポッシュ）digital camera module

The **PDZ43 Lapochée** is a digital camera module accompanying the **THZ43 Chiaro** mobile phone released in May 1999 by the Tu-Ka mobile phone company and operator (then merged in KDDI Corporation). Both phone and camera module were made by Mitsubishi. This was technically the **[first case of mobile phone equipped with a digital camera](/Amateurism%20is%20the%20mother%20of%20invention.pdf)** (and among the first low-end market digital cameras too).

The LaPochée camera module acquired a certain celebrity in the Game Boy Camera nerds community as it shows a potential hardware filiation with the Game Boy Camera according to various Mitsubishi sources frome 1999-2000. It might or might not share the same analog light sensor from the M6428X series. I tried to find this camera module for years. By the time, addict to old electronic stuff, I obtained some M64283FP sensors from factory (possibly used in the LaPochée) by pure luck and published [Arduino codes codes to drive them](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor). The M64283FP sensor is basically a Game Boy Camera M64282FP sensor with more functions, but pin compatible. You will see why I insist on this sensor later.

I finally got the Lapochée camera module in March 2025 thanks to a local contact in Japan (see acknowledgments). The device was advertised as electronic junk but in pristine state according to seller images. It was delivered in its factory plastic bag still with the protective film on front face ([click here for some ASMR](/Pictures/Lapochee_ASMR.mp4)). Sadly for me, the device required changing the two LCD polarizers (which was a [real pain in the arse](/Pictures/Lapochee_LCD_repair_1.jpg)) and even after that, did not boot and draws nothing even connected to a stabilized power supply. The PCB is a 4 layers board (tracing is a nightmare) and a basic checking reveals at least a shorted capacitor and lack of connection to ground for several other ones (so at least two different issues), which is critical enough to declare the device non fixable in absence of a schematic, without wasting an unreasonable amount of time. Of course reflowing all reachable surface components changed nothing, so the issue is probably within the inner PCB layers.

Fun fact, "LaPochée" is probably a name designed to sound cute and French. It is an approximate translation of "The pocket" ("La Poche"). It uses the same acute accent as in "Pokémon", just to annoy the English speakers.

I do not own the user manual but I am in search for it (feel free to contact me if you have one or a scan, I would be glad to credit you).

But I guess you landed here for some good old vintage electronic porn and not to read a draw my life. Let's dive into the beast !

# Pictures from the outside / inside and comments

![](/Pictures/Lapochee_2.jpg)
The device exudes the 2000s with its white round design and the touch of blue transparent plastic.

![](/Pictures/Lapochee_side.jpg)
The right side features the on/off button and a contrast thumbwheel for the display. The device has no LED or speaker / buzzer to indicate its state. It's completely mute.

![](/Pictures/Lapochee_bottom.jpg)
The bottom shows the communication port with the mobile phone. It's not a common plug, I have no idea what it is for the moment (see next for a closer picture without the cap).

![](/Pictures/Lapochee_rear_2.jpg)
The back side shows the battery compartment and a 3 positions stand. Not sure why the stand is longer than the device itself. Design I guess. The camera was probably thought to be conspicuously shown hanging from a shirt pocket. I have no shirt to try.

![](/Pictures/Lapochee_rear_open.jpg)
PDZ43 is Mitsubishi factory name of the LaPochée module. Surprisingly, it is referenced as 71PDZ43 on the [original packaging](/Pictures_from_auction_sites/Aucfan_packaging_4.jpg).

![](/Pictures/Lapochee_2xAAA_batteries.jpg)
The device is supposed to work with 2xAAA batteries which was a very fancy norm before the flooding of market with shitty lithium batteries. Because yes, we were still able to use AAA rechargeable batteries (and reuse them elsewhere) in these old times.

![](/Pictures/Lapochee_main_board_with_LCD_mounted.jpg)
The device opens by removing four annoying 3-wings screws similar to any Nintendo products from that era. I guess this was a common trick in Japan to discourage user from sneaking inside electronic products, whatever the brand.

![](/Pictures/Lapochee_head_assembly_2.jpg)
The rotating head itself has two similar screws to remove in order to see the inside. Similarity with the Game Boy camera is immediately striking.

![](/Pictures/Lapochee_empty_head_2.jpg)
You can easily go further in the head assembly / disassembly if you are familiar with the Game Boy Camera. It feels better than a Game Boy Camera thanks to two prongs on the metal ring that safely position the head in normal or selfy position. The design is more refined, while very similar. The sensor ribbon socket is smaller than the Game Boy Camera (must be a JST connector with 1 mm pitch).

![](/Pictures/Lapochee_PCB_front.jpg)
At this step removing the main PCB is very easy. The back side mainly features a Mitsubishi M64916FP chip and an oscillating crystal (6.898594 MHz probably). Although sharing the numbering of Mitsubishi chips (FP termination seems to be used for home appliance, M64 is a common prefix of several Mitsubishi chips from that era), this chip is not documented anywhere. By tracing some connections I conclude that this is probably a custom driver chip for the LCD display and not some kind of MAC-GBD like chip driving the sensor, despite the packaging similarity. This chip would deserve a decapping to see what's inside, maybe in the future.

![](/Pictures/Lapochee_serial_8_pins_connection.jpg)
Some details of the bottom serial connector with the plastic plug removed. It's probably proprietary. It features 8 pins.

![](/Pictures/Lapochee_main_board_with_LCD.jpg)
Front side of the PCB with the LCD mounted on brackets. A black rubber damper ensures a very tight fit within the shell in case of shock. The LCD assembly can be easily removed from the main PCB by just unclipping it. Nothing is glued. It is clearly meant to be easily repairable. As you can see, the LCD display had better days. Both polarizers were dead.

![](/Pictures/Lapochee_PCB_rear.jpg)
The front PCB side (below the LCD display) contains all the meat: LCD voltage driver, flash memory and microcontroller. The flash memory is a 4MB / 3.3V only [M5M29KB800](/Datasheets/Renesas_M5M29KB.PDF) from Mitsubishi, commonly used in mobile phones from that era. The main chip is a 7 to 10 MHz 16-bit [M30610MCA](/Datasheets/Renesas_M5M29KB.PDF) microcontroller, also from Mitsubishi. The marking indicates that this is the 128 KB ROM, 10 KB RAM, mask ROM version 282. This microcontroller also has several 10 bits analog-to-digital converters (A/C or ADC) so I guess that the sensor is directly driven by this chip in input / output, nothing else inbetween is required. I do not see any external ADC anyway.

The last noticeable chip is the Sharp [IR3E05](/Datasheets/Sharp_IR3E05.pdf). The only information I can find is that this is a divided voltage generator for LCD drive, so the chip that sends the high voltage signal to the display individual pixels to twist more or less the liquid crystals. This indicates that the LCD can display several gray levels. A "high voltage" generator circuitry must be present somewhere on the PCB (LCD may require about 20V).

![](/Pictures/Lapochee_LCD_rear.jpg)
The display assembly is very easy to remove and neatly designed. The LCD is a 128x128 pixels Sharp T2 V M1128CP with a 24 pins ribbon connector, probably manufactured in March 1999. I do not find any datasheet for this display. Mine is defective and stay completely dark even with the front polarizer removed. I have very thin hope to find a replacement or a compatible one due to the absence of datasheet for both the LCD and the M64916FP driver chip. They both can be totally custom for this device.

![](/Pictures/Lapochee_lens_front.jpg)
![](/Pictures/Lapochee_lens_rear.jpg)
The lens used is very similar to the Game Boy Camera one with a screw mount to adjust focus in factory.

![](/Pictures/Lapochee_sensor_PCB_ribbon.jpg)
The sensor uses a 9 wire "ribbon". The ribbon is secured at both ends with some adhesive tape (one is missing here because I had to remove it to detach the sensor sub PCB for imaging).

![](/Pictures/Lapochee_sensor_PCB_rear.jpg)
AR SUB is for "Artificial Retina" sub board. All sensors from the M6428X series are called like this because it is much cooler than "el cheapo CMOS sensor" (what it was meant to be).

![](/Pictures/Lapochee_sensor_PCB_front_M64283FP.jpg)
The PCB comprises two caps and one inductance, similar to the Game Boy Camera. I guess this is exactly the same electrical circuit. The two round test pads are connected to floating pins (see next, this is interesting). Strangely enough, one pin has solder residues (maybe accidental).

The marking RF131111B (+AR SUB) is also written near the LCD ribbon socket on the main PCB (+AR MAIN) so I guess this is an internal reference number for the PCB layout.

![](/Pictures/Lapochee_sensor_reference.png)
A quick look under a powerful microscope shows that the image sensor is a 128x128 pixels [M64283FP](https://github.com/Raphael-Boichot/Play-with-the-Mitsubishi-M64283FP-sensor) sensor, successor of the M64282FP sensor used in the Game Boy Camera, as anticipated. A quick look at the front of the PCB shows that STRB and TADD pins, which allows access to the advanced functions via additionnal registers, are just not connected (these are the two pins connected to the round test pads). As the Lapochée module is advertised as taking [96x96 pixels images](https://pc.watch.impress.co.jp/docs/article/990413/tu_ka.htm) (1 bpp or 2 bpp), this implies that images are cropped by software and not by using the random access mode of the sensor. It's a bit deceptive to be honest, but it indicates that management strategy must be close to the Game Boy Camera sensor as registers sent must be similar by design.

![](/Pictures/Lapochee_empty_shell_2.jpg)
A quick look at the empty shell after disassembly. Reassembly is quick and simple in a few minutes. Nothing was broken because good engineering. 

The repository contains additional images not displayed here, do not hesitate to check. To be continued if I find further information like the user manual or a new working device for example...

# Credits
Please credit any image you publish / reuse from this repository like this: **Raphaël BOICHOT, 2025**. And give a link to this repository.

# Acknowledgements
- Author wants to warmly thank **Frédéric Mercier** for the finding of the Lapochée camera module on Mercari in Japan (and some other rare stuff).
- Thanks also to Razole for providing me some factory sealed M64283FPs from under the counter.
