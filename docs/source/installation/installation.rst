Installing Mu
=============

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

This indicates that Mu has not detected a robot device attached to the computer. In order to write and download programs to the robot, you'll need to connect your computer to the robot via a Micro USB cable. Turn your robot on.

.. figure:: connected.png
	:scale: 50%

Once you've done this, the red 'x' on the symbol should disappear, and this indicates you've successfully connected to the robot.