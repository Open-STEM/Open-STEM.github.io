.. WPIGSILib documentation master file, created by
   sphinx-quickstart on Sun Aug 21 08:33:06 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Installation
===================================

.. note

   This project is under active development and the API references are subject to change at any time.

Installing Mu
-------------

Mu is a simple and concise editor that allows us to edit our CircuitPython code, and view serial output from our robot. To install, go to the following webpage:
https://codewith.mu/en/download

You'll see a page like this:

.. figure:: mu.png
	:scale: 50%

Download the file corresponding to your operating system, and then open the file and follow the installation prompts that pop up.

Mu gives you the option to run different implementations of Python for different microcontrollers. In our case, we want to run CircuitPython, which is compatible with our Maker Pi RP2040. Select the "Mode" button shown below.

.. figure:: selectmode.png
	:scale: 50%

Now, select CircuitPython and confirm by clicking 'Ok'.

.. figure:: selectmode2.png
	:scale: 50%

In the figure below, you'll notice a symbol of a red 'x' on a microchip.

.. figure:: disconnected.png
	:scale: 50%

This indicates that Mu has not detected a robot device attached to the computer. In order to write and download programs to the robot, you'll need to connect your computer to the robot via a Micro-USB cable. Turn your robot on.

.. figure:: connected.png
	:scale: 50%

Once you've done this, the red 'x' on the symbol should disappear, and this indicates you've successfully connected to the robot.

Installing the robot library
----------------------------

Our robot library makes it easy to give different commands to the robot. Go to [link], download the zipped folder, and unzip it.

With your robot connected to your computer, you should see an external drive labelled 'CIRCUITPY'.

.. figure:: drive.png
	:scale: 50%

This is your robot's drive, and where you'll be writing and storing your programs! Delete anything that is currently in the drive, and copy the entire folder you downloaded to the CIRCUITPY drive.

.. figure:: load.png
	:scale: 50%

Then, open the Mu application and click the "Load" button as shown above. Navigate to the CIRCUITPY drive and open code.py.

You should see something liks this:

.. figure:: opencode.png
	:scale: 50%

code.py is where all your code will run! In order to run a program, simply write code, save your changes, and your code will automatically start executing on the robot!

Before we write any code though, click the 'Serial' button. If the robot is connected to the computer, this will allow you to view your robot's logs on your computer while running your program, which is very useful for debugging.

.. figure:: serial.png
	:scale: 50%

Finally, let's test some code out. Add the following code to code.py:

.. figure:: helloworld.png
	:scale: 50%

Then, click the 'Save' button. Note that pressing Control-D will also run your code.

You should see the robot immediately start going forward for 20 centimeters. At the end, it should log "Hello World" on your computer through serial output. If nothing goes wrong, then you have successfully set up the software and are ready to write more intricate code!