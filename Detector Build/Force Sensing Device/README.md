# Force Sensing Device
While this folder is specifically for the Mass sensing device the concepts can be applied to other categories

# Detector schematics
#### I have these two circuit schematics for detectors with different complexities.

## Using the built in ADC of the Atmega328p
![Schematic](https://i.imgur.com/cdL5cyd.png)
I used a similar design for my first three years of this event. It works well and is simple. This is the bare minimum to get solid results.

## Using a secondary ADC
![Schematic](https://i.imgur.com/GRMG1O0.png)
This is a new design that I have chosen to go with this year. Using an additional ADC there is a lot more data but a lot more parts.

### Pros and Cons
The only real difference is the device that does the reading from the voltage divider. The Atmega328p has a 10 bit analog to digital converter (ADC). When analog read is called you can get between 0 and 1023 as $2^{10} = 1024$. The second design uses an [ADS1015](https://www.ti.com/lit/ds/symlink/ads1015.pdf) or could be changed to use an [ADS1115](https://www.ti.com/lit/ds/symlink/ads1115.pdf). The big advantage with these chips is that they are 12 or 16 bit ADCs. These chips give us a total of $2^{12}=4096$ or $2^{16}=65536$ values! They also use I<sup>2</sup>C to talk to the arduino which is great if you are using an I<sup>2</sup>C display. We can get a lot more accurate readings but there is a massive catch. These only come in QFN and VSSOP packages and not DIP packages.

![rules](https://i.imgur.com/kiXHyrn.png)
In order to use a chip like a secondary board that can be easily purchased would break this rule. However "*surface mount adapter boards*" are allowed. This adds complexity as there are additional parts needed for the ADS chip to work. Some parts like the ferrite beads could be skipped but its not recommended as they suppress signals on the voltage line. There are also two capacitors which protect the chip from voltage spikes. The final addition are the three 10k pull up resistors. **Do not** remove these they are needed for I<sup>2</sup>C communication.

> In short you have to choose between a simpler circuit or more accuracy.

### Possible changes. 
You could use a [WS2811](https://cdn-shop.adafruit.com/datasheets/WS2811.pdf), [SK6812](https://cdn-shop.adafruit.com/product-files/1138/SK6812+LED+datasheet+.pdf), [WS2812](https://cdn-shop.adafruit.com/datasheets/WS2812.pdf), or other similar addressable LED instead of three individual led. This switch would need a change to the code but it would also cut down on the number of parts. You would only need one led compared to three and you could cut down the number of resistors used.