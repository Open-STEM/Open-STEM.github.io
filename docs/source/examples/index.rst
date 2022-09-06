Understanding the Code
========================

All of the code you write should be called from within the main() function, located within code.py. 

This approach will simplify the amount of code that gets run at once, reducing errors overall (code not wrapped in functions get called on import).

Getting the Robot to Move
-------------------------

Getting the robot to move is a pretty simple task, and WPIGSILib provides 3 main ways to do that:

..code::
    
    drivetrain.set_effort(left_effort: float, right_effort: float)
    drivetrain.go_straight(distance: float, speed: float = 0.5, timeout: float = None)
    drivetrain.go_turn(turn_degrees: float, speed: float = 0.5, timeout: float = None)

We're gonna start off focusing on set_effort(), since it is the base that the other two are built off of.

A motor's "effort value" is a measure of how much power is set to it from the board. It is bound between -1 and 1, meaning that -1 goes full power in reverse, 1 goes full power forward, and 0 stops it. 
There is also a secondary method drivetrain.stop(), which will set the effort values for both the left and right motors to zero.

.. code::
    
    def main():
        drivetrain.set_effort(1,1)
        time.sleep(1)
        drivetrain.stop()

The above code will drive the robot forwards for 1 second at full power forwards before stopping.

How to Use The Existing Sample Code
-----------------------------------

Sample code is contained within the onboard code inside of the SampleCode directory. 

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

wait_for_button() is also a sample method, located within SampleCode.sample_miscellaneous.py. Placing it at the beginning of main() causes the code to wait for the button input before running, which is often a desireable property.