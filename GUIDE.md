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


