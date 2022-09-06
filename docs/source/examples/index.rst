Understanding the Code
========================

All of the code you write should be called from within the main() function, located within code.py. 

This approach will simplify the amount of code that gets run at once, making errors easier to find.

Getting the Robot to Move
-------------------------

Getting the robot to move is a pretty simple task, and WPIGSILib provides 3 main ways to do that:

.. code::
    
    drivetrain.set_effort(left_effort: float, right_effort: float)
    drivetrain.go_straight(distance: float, speed: float = 0.5, timeout: float = None)
    drivetrain.go_turn(turn_degrees: float, speed: float = 0.5, timeout: float = None)

We're gonna start off focusing on set_effort(), since it is the base that the other two are built off of.

A motor's "effort value" is a measure of how much power is set to it from the board. It is bound between -1 and 1, meaning that -1 goes full power in reverse, 1 goes full power forward, and 0 stops it. 
There is also a secondary method drivetrain.stop(), which will set the effort values for both the left and right motors to zero.

.. code::
    
    def main():
        drivetrain.set_effort(left_effort = 1, right_effort = 1)
        time.sleep(1)
        drivetrain.stop()

The above code will drive the robot forwards for 1 second at full power forwards before stopping. You can get a variety of different movements just from adjusting the parameters to the set_effort function, try it out!

go_straight() is very self explanatory. It takes in a distance to be traveled (in cm), 
and optional parameters for an effort value to run the motors at (by default 0.5) and for a timeout (where the function will end early if specified that it should only take a set amount of time).
To drive backwards, you can either set distance or the effort value to a negative value (setting both to be negative will cancel out and the robot will drive forwards)

.. code::

    def main():
        drivetrain.go_straight(20, 0.8)
        print("Hello World")

This code will move the robot forwards 20 cm and then display "Hello World" in the serial log (Instructions for accessing the serial log at the bottom of _`this page` <https://first-plus.readthedocs.io/en/latest/installation/robotlib.html>)

go_turn() is similarly simple. It too takes some distance to turn (this time in degrees), and the same two optional parameters. 
A positive angle denotes a clockwise turn, and similar to go_straight(), you can set either the distance or speed to negative to turn counter-clockwise.

.. code::

    def main():
        drivetrain.go_turn(90, -1)
        print("Hello World")z

This code will now turn 90 degrees counterclockwise (as speed is negative), before displaying the same message in the serial log as before.

Using Sensor Input
------------------

The easiest "sensors" to interact with on the robot are definitely the two buttons on the circuit board. WPIGSILib has two different functions used to interact with them, but the two buttons behave the same.

.. code::

    buttons.is_GP20_pressed()
    buttons.is_GP21_pressed()

These methods take in no parameters and return true if the button is currently pressed, and false otherwise. 

A great application for these buttons can be found in the SampleCode, within sample_miscellaneous.py

.. code::

    def wait_for_button():
        print("Waiting for button signal from either button")

        # Wait until user command before running
        while not (buttons.is_GP20_pressed() or buttons.is_GP21_pressed()):
            time.sleep(.01)

        print("Button input found; Program starting")

This method uses a while loop to wait until there is a button input from either button before continuing to the rest of the code. 
This is very useful to put at the beginning of your main() method, as by default the code will run as soon as you upload the new code to the bot, but with this the code will not run until after you press one of the buttons.

The next sensor we will look at is the ultrasonic distance sensor, which measures the distance from the front of the sonar to the nearest object in a straight line from the sensor. There is just one method we use to get input from the sonar:

.. code::

    sonar.get_distance()

This method takes in no parameters, and returns the distance in centimeters.

Something cool we can do with this sensor is have the robot try to maintain a constant distance from itself to the nearest target:

.. code::

    def standoff(target_distance: float = 10.0):
        KP = 0.2
        while True:
            distance = sonar.get_distance()
            error = distance - target_distance
            drivetrain.set_effort(error * KP, error*KP)
            time.sleep(0.01)

This example takes advantage of a technique called Proportional Control, where the power sent to the motors is some function of the error, which is the difference between the current and target values. It's a very flexible and powerful technique when mastered.

The last sensor(s) on the robot are the reflectance sensors, which measure how much light is reflected off of a nearby surface. Usually, they are mounted below the robot so that they can sense the color or material differences between two points. 


.. code::

    reflectance.get_left_reflectance()
    reflectance.get_right_reflectance()

Neither of these methods take in parameters. The value that the sensor outputs is hard to grasp in terms of real world values (higher number usually means a lighter color or more reflective surface), so most of the time we use the two sensors (right and left) together so that we can compare them.

.. code::

    def line_track():
        base_effort = 0.6
        KP = 0.02
        while True:
            error = reflectance.get_left_reflectance() - reflectance.get_right_reflectance()
            drivetrain.set_effort(base_effort + error * KP, base_effort -  error * KP)

This code does exactly that, taking in the left and right reflectances to get an error, and then uses that to adjust left or right so that the robot can follow a line.

Servo and LED Control
---------------------

On board the robot there is a servo. A servo is a motor with a limited range, meaning that it can only travel a span of 135 degrees. To control the servo, there is only 1 method needed:

.. code::

    servo.set_degrees(degrees: int)

The servo is controlled by an integer number of degrees, so you can only tell it to go to an integer angle.

.. code::

    def main():
        while True:
            if buttons.is_GP20_pressed():
                servo.set_degrees(0)
            if buttons.is_GP21_pressed():
                servo.set_degrees(135)
            time.sleep(0.01)

This sample code shows a way that the robot can respond to user input, checking every 10 milliseconds (0.01 seconds) for a button input, and then moving to a new position if it finds it.

Lastly, the board contains two RGB (Red-Blue-Green) LEDs that can light up in any color, but you do nopt have independent control of the two LEDs, they are always controlled in sync. There are two different functions for controlling the LEDs.

.. code::

    led.set_color(red: int, green: int, blue: int)
    led.set_brightness(brightness: float)

Using the LEDs are a two step process. First, you set the intended color in RGB format (each bound from 0-255), using set_color. Then, you set the brightness of the pixels [From 0 (off) to 1 (full brightness)].

.. code::

    def main():
        led.set_brightness(1)
        while True:
            random_red = random.randint(0,255)
            random_green = random.randint(0,255)
            random_blue = random.randint(0,255)
            led.set_color(random_red,random_green,random_blue)
            time.sleep(1)

This code will change the LEDs to be a random color every second. LEDs could be used functionally to show which step of the code is running or to send signals to the user while running just by setting the color in between larger steps of the program.


How to Use The Existing Sample Code
-----------------------------------

Some sample code (including most of the code used on this page) is contained within the onboard code inside of the SampleCode directory. 

When you first download the library, code.py should already be populated with the following optional imports:

.. code::

    ## Optional imports for use with sample code
    from SampleCode.sample_drive_methods import *
    from SampleCode.sample_sensor_access import *
    from SampleCode.sample_miscellaneous import *

From there, using the sample methods is as simple as placing the calls to them within the provided main function.

.. code::

    def main():
        wait_for_button()
        #
        # Your code goes here!
        #
        polygon(side_length = 10, number_of_sides = 5)

wait_for_button() is also a sample method, located within SampleCode.sample_miscellaneous.py. Placing it at the beginning of main() causes the code to wait for a button input before running, which is often a desireable property.