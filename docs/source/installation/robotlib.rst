Installing the robot library
=========================

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

Then, click the 'Save' button. You should see the robot immediately start going forward for 20 centimeters. At the end, it should log "Hello World" on your computer through serial output. If nothing goes wrong, then you have successfully set up the software and are ready to write more intricate code!