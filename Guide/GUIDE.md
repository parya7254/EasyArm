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

![Finished PCB Placement](image-23.png)

Now we will have to connect the things to each other in our PCB, the blue lines you currently see are called ratlines, they incdicate where a pad in a PCB is connected and shows that the pad is not connected. We will first wire up the receiver side of the PCB. First go to your servo and then select a hole (or pad) you would like to connect first. Then press X to begin wiring (or select the wiring tool):

*Note: something on the front side of the board is red, while something on the back is blue:

![Front Side Trace and Back Side Trace](image-26.png)

![Wiring Tool](image-24.png)

Then the rest of the PCB should go dark other than the things that need to be connected. connect it to where the pad lights up (IMPORTANT: Do not connect the pad to the other part of the PCB (dont connect something in the receiver side to something that lights up in the transmitter side) or your PCB will not work properly). You can click to fix a point of the wire to the PCB just like the schematic. You do not need to wire the pads of the Pico to each other even if they light up. This is what it looked like when I connected the GND of the servo to the GND of the Pico:

![GND of Servo Connected to GND of Pico](image-25.png)

* IMPORTANT TIP: you can press V while you route to place a via. A via transfers a wire from the front side of the PCB to the back side like so: 

![Via on PCB](image-27.png)

* You can also route starting from the back side by selecting the B.Cu layer.

* You can also ignore the GND and 5V ratlines crossing into the other side

This is what my routed PCB looked like:

![Routed PCB](image-28.png)

# Making the PCB Space themed
Since the current Kit-Lab theme is space, we will make our PCB space themed! To do this, find a space-themed picture and download it, for example, I chose this one:

![Space Theme Picture Example](image-29.png)

Now, go to your KiCad main menu, and select the Image Converter:

![KiCad Image Converter Tool](image-30.png)

And then select the "Load Image Source" button and them insert the image you downloaded. After that, select the "Export to Clipboard" button and then simply go back into your PCB to paste the image! You can also change the ourput size before you export if your image is too large/small (I recommend leaving the Lock height / width ratio option on). Here's mine for example:

![PCB With Space Picture](image-31.png)

Make sure you add more than 1!

Now we are one half of the way done! We just now have to make the case and do the arm's firmware!

# Designing the Case

Now that we have finished with the PCB part of this project, we will now start designing the case for our arm! The arm will need a case so that it actually can move pieces.
To start off, go download Fusion360 since that is what we will be using for this proejct's case. You can use other CAD software but it might be harder since the controls and functions might be different.

We will first create a new project, to do this, just click the + button on your top toolbar and you should see a menu pop up. Select "Part Design" and then a new design tab should be there.

Next, press the Create Sketch button on the Solid tab, which looks like this:

![Create Sketch Button](image-32.png)

After you press that, 3 squares should pop up, select the square on the side you want it to be on, I usually select the square on the bottom and with the x and y axis. Now, you should see a sketch palette pop up. 
Press R to start creating a rectangle and then make a random rectangle. This will soon be the base of our Transmitter. Now we will set the length of our sides using the Sketch Dimension tool which looks like this:

![Sketch Dimension tool](image-33.png) 

You also could just press D for it as well. After we select the tool, we will select one side and set it to the width of our PCB and increase it by 1 mm. (my PCB is 100mm so I will set it to 101mm) and also do the same with the height of the PCB.

![Rectangle with Defined Dimensions](image-34.png)

Also create another rectangle that is 20mm bigger on each side on top of the first rectangle.:

![Bigger Rectangle on top of Smaller Rectangle](image-36.png)

And then use the Sketch dimension tool and then select one edge of the smaller rectangle and then select the corresponding edge of the bigger rectangle and then set the value to 10mm. Do the same for the other edge and you only need to do this once for the horizontal edge and once for the vertical edge like so:

![Smaller Rectangle Spaced 10mm per one Horizontal and Vertical Side to Larger Rectangle](image-37.png)

Now click the "Finish Sketch" button on the top right corner:

![Finish Sketch Button](image-35.png)
 
And now there should be two blue retangles. We will now extrude the squares. To do this, select the extrude to or just press E (it should be next to the create sketch button):

![Extrude Tool Button](image-38.png)

And then select the smaller interior square and then set the distance to 2:

![Extrude Window Menu](image-39.png)

Then you will see the outer rectangle go away so select the sketches folder in the browser and then open it's dropdown and then press the eye button on Sketch 1:

![Browser Window with Sketch 1 Visible](image-40.png)

![Visible Bigger Rectangle](image-41.png)

Now select the outer rectangle and extrude it by 12mm and it should finally look like this:

![Extruded Larger Rectangle of Case](image-42.png)

And now that we have created the case for the transmitter, we will now add a hole for the USB port of the Pico.