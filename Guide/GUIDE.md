# Mini Robot Arm!!

In this guide, we will be making a custom wirelessly controlled 2 servo robot arm!

Here are the parts in your Kit Lab kit along with what will be used:
|Kit Parts|Quantity|
|---------|--------|
|RPi Pico|2|
|nRF24L01+|5|
|RGB LED|5|
|INA3221|1|
|MPU6500|1|
|Pushbuttons|20|
|830P Breadboard|1|
|Jumper Wires|1 Bundle|
|Servo Motor|2|
|1N4733A Diodes|5|
|Mixed Value Resistors|1|

|Parts We Will Need|Quantity|
|------------------|--------|
|RPi Pico|2|
|nRF24L01+|2|
|MPU6500|1|
|Servo Motor|2|


Note: Be sure to customize this project and not just directly copy it. (Add a LED, Buttons?)


Lets start with our project now!

# Creating a schamatic

First of all, we need to plan out how things will be connected to our PCB! We don't just wanna mindlessly add and connect things since you would not know what is connected to where, causing you to have a PCB that will not work with your project. This is where schematics come into play. Schamatics help you plan out what things will be used and how they will be connected to each other. We will begin by installing KiCad, KiCad is a simple tool which is really easy to learn and beginner friendly! Go install KiCad at: https://www.kicad.org/ and open it! Next, look at the top-left corner and click the create project button, which looks like this: 

<img width="51" height="70" alt="image" src="https://github.com/user-attachments/assets/b6c5dba1-086a-4486-9e61-73d168e6b997" />

After that, name your project and click on this to open your schematic:

<img width="577" height="96" alt="image" src="https://github.com/user-attachments/assets/98677265-7f5a-4777-bb5f-7a1deb4f1a5c" />

Now, what we want to do is add symbols. Symbols are the modules that you would conenct to your PCB and this will help you connect things. Press A and them type in RP2040, then scroll down and select the Raspberry Pi Pico, this will act like the brain of our robot arm's reciever and transmitter. Then place your Pico somewhere on the schematc area and then add another pico since we will need 2 (one for the reciever and one for the transmitter):

<img width="1581" height="734" alt="image" src="https://github.com/user-attachments/assets/ab8728a3-5f35-4eac-9d80-53c6692cb3b1" />

<img width="3507" height="2480" alt="image" src="https://github.com/user-attachments/assets/cb3dc639-3760-4ef2-b1d6-af3c1d99f14a" />

Now we will add the gyroscope module (MPU-6500) to the schematic.
If we check for the MPU-6500 in the symbools, we will only see the chip of the PCB, but we have a module. The difference is that modules have the tiny chip soldered to it already and can be easily connected with header pins. Now back to KiCad, we do not see that there is a MPU-6500 module so what we will do is just use a 01x10 pin connector. We will add another symbol, select add symbols (or press A) and then search up 01x10 and select Conn_01x10 in the Connector_Generic area and then place it down somewhere.

<img width="1576" height="746" alt="image" src="https://github.com/user-attachments/assets/839163bb-0cee-43dd-bf06-531e05578574" />

Now do the same but add 2 01x03 connectors for the Servos:

<img width="3507" height="2480" alt="image" src="https://github.com/user-attachments/assets/5ce851f0-8db6-46ab-af3e-3f575ae06c7b" />

And for the nRF24L01+, search nRF24L01 (without the +) when you go to add symbols and select the NRF24L01_Breakout symbol and place it somewhere and also add another one since we will use 2 for this project.

<img width="1569" height="737" alt="image" src="https://github.com/user-attachments/assets/fc07f7bc-c3d2-4370-9471-67ce3d8f83ea" />

Lets also name our parts, to do this double click the "A_" on the Pico you want to be the transmitter, a popup window should appear, type in "Transmitter" and the reference name will be changed like so:

![Reference Example](image-1.png)

Do the same for the receiver Pico and also the transmitter/receiver wireless modules (nRF24L01).

Don't forget to name your servos as well!

Here is how it looked like for me: 

![Current Schematic](image-3.png)

# Wiring the Schematic
Lets add power symbols to the schematic by pressing P. Power symbols will redirect all of the pins connected to that symbol to one power pin. I added a 5v and GND power symbol like so (they are highlighted):

![Power Symbols](image-6.png)

Now we will wire up the things in the schematic. This will tell us which pin is connected to where on the PCB. Lets start wiring the servos to the receiver board. You could either press W to wire or just click on the small circles at the pins and then a green wire should appear and wou can click to fix a point of the green wire at that location.  

![Wiring Servo](image-4.png)

Here is a picture of the servo pinout to help: 

![Servo Pinout](image-5.png)

Lets wire servo 1 to GPIO14 and servo 2 to GPIO15 of the receiver Pico:

![Wired Servos](image-7.png)

Now we will wire the nRF24L01+ Module which uses a SPI communication protocol. The defaust SPI0 Pins of our Pico are:  GPIO19 (MOSI/TX), GPIO18 (SCK), GPIO17 (CS) and GPIO 16 (MISO/RX). Connect CE to GPIO 20 and place a no connect flag on IRQ by pressing Q to place it. Use the same pinout while connecting the other nRF24L01+ module to its respective Pico.

![Wired nRF24L01](image-8.png)

Now lastly, we have to wire the MPU-6500 gyroscope to the transmitter. Here is a helpful pinout diagram:

![MPU-6500 Pinout](image-9.png)

The MPU-6500 supports the I2C protocol which only needs 2 pins for data. So, we only have to connect the power pins and the I2C pins (SCL and SDA) to get it to work. Connect the SCL pin to GPIO5 and SDA to GPIO4.

![Wired MPU-6050](image-10.png)
![Finshed Schematic](image-11.png)

Now this is the last thing you have to do before moving on to designing the PCB, you have to assign the footprint to the header pins. A footprint is an identity an object has on an PCB, in our case, it will be the holes for the header pins. To do this click on the assign footprints button on your toolbar at the top: 

![Assign Footprints Button](image-12.png)

After that if you get a popup that says "Annotate Schematic", then press the annotate button and after it is done, press close. If you do not get this popup, you are fine. Your assign footprints window should be like this:

![Assign Footprints Window](image-13.png)

And then for the Conn_01x10, search, "Connector_PinHeader_2.54mm:Pinheader_1x10_P2.54mm_Vertical" and select it (do not select the SMD one, just the normal one), for the 1x3 conn, look up, "Connector_PinHeader_2.54mm:Pinheader_1x03_P2.54mm_Vertical" and select that. It should look like this at the end:

![Assigned Footpritns](image-14.png)

Then click, "Apply, Save Schematic, & Continue"

Now we are finished with the schematic and ready to move on to designing the PCB!

# Designing the PCB

We will first open our PCB, to do this, press the PCB button in your KiCad toolbar, it should look like this: 

![PCB Button in Schematic Toolbar](image-15.png)

Now once we are in out PCB editor, we will import everything from our schematic, click this button in your toolbar:

![Import From Schematic Button](image-16.png)

And after clicking it, press the "Update PCB" button and then close the popup. What we will be doing is we are going to create one PCB and that PCB will have 2 sides: once side where the receiver parts will be soldered, and another side where the transmitter side will be soldered. When you order a PCB, the minimun quantity will most likely be more that 1 so we can solder only the transmitter parts to the transmitter and only the receiver parts to the receiver side of the PCB. So make sure that you move your parts and seperate them. 

Before you start moving your parts, select te Edge.Cuts layer (on your right side) and then click the square icon and then make a square. After you make a square, select it and then press E. You will get a popup, Select "Corner and Size" and set the size you want your PCB to be. The maximum size for your PCB is 100x100mm. 

![Edge.Cuts Layer](image-19.png)
![Create Square Button](image-20.png)

After you make the size of your board, start arranging your components into an order you would like, but I recommend arranging your transmitter components on one size, and the receiver components on the other. Make sure that the Pico's "USB Cable Keep Out" areas are outside the board outline like so:

![Example of USB Keep out area outside the PCB outline.](image-17.png)


* You can press R to rotate an object

This is what it looked like after I finished arranging my parts:

![Finished PCB Layout](image-18.png)

Dont forget to brand your PCB!! To do this, select the F.Silkscreen layer and then select the text button: 

![Insert Text Button](image-21.png)

After selecting it, click anywhere in your PCB editor area and you should get a popup. You can also change the width, height, and font of the text in the popup you get. And after finishing with the popup, place it somewhere in your PCB

# Recommended Step:
I recommend dividing the transmitter and receiver side of your PCB to avoid confusion while soldering parts. To do this, select the F.Silkscreen layer and then click the line tool:

![Line Tool Button](image-22.png)

Then click the points of where you want your line to be and then press Escape if your line tool does not stop placing lines. Then, if you would like, add text indicating which side is the transmitter and which side is the receiver. This should be the end result:

![Finished PCB](image-23.png)

Congrats on finishing your PCB!!

# Code