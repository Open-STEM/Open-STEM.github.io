Line following
==============
We have always heard our school teachers instructing us to walk in a line, right? So, this task of following a line isn't something new for you. However, what if I tell you that it's your turn to teach your robot to follow a line?
As we start exploring the capabilities of our robot, I think line following is an interesting challenge, to begin with.

Why follow lines?
----------------
We see lines everywhere, don't we? The joint between two floor tiles or a linear pattern on the carpet?
We see lines on the road that separate the oppositely moving traffic. Lines on the roads also highlight special areas like zebra crossings, bicycle lanes, etc. As a roboticist, you might come across a challenge to design software for self-driving cars that might need line following.
Did you know Tesla uses line following up to some extent as well?
Isn't that interesting? You are about to start learning about this cool idea of teaching your robot to follow a line. Something so fundamental and yet so impactful that real cars on the street use it daily.
So are you excited to begin?

Characterizing the sensors
--------------------------
So let us start by observing ourselves. How do we see lines and patterns in the environment?
You may say that our eyes show us everything! My next question is, how do you know that you are looking at a line?
What is so special about a line that makes it stand out from the other features in your sight? It is dark or bright with respect to its surrounding. Isn't it?

That is a clever observation! Now, let us look closer. The difference in color or brightness is caused due to a difference in reflectivity of the material appearing as a line. For our robot, we will be using colored tape on the floor to mimic a line. We will use the difference in the reflectivity of the tape and the ground material to recognize a line and then teach the robot to follow it. 

Are you wondering how can we do that without having a camera? Well, you don't need a camera. Your robot is equipped with a sensor that distinguishes between different materials based on their incoming light reflections.  
Isn't that interesting?

The sensor is manufactured by a company named Pololu. The sensor is a linear array of six Infrared light emitters and receivers. The infrared light emitted by the sensors is reflected from the tape and the floor. Since there is a change in reflectivity between different materials, the reflected light is not the same. The receivers can make out the difference between the reflections from the ground and those from the tape. 
This difference is sensed by the sensor and it shall be enough to recognize and follow a line. Are you excited to learn how that is possible? And what can we do with it? Please read on. 
Please think about what you would receive from the sensor and what would you want the robot to do with this information. Here is a hint, the sensor is going to send reflectivity values to your robot. Now, what can you do with this information?  
Here is how the code could look like :

# Characterize line sensors
def checkLineSensors():
    while True:
        print("Left:", refl.left(), "Right:", refl.right())
        time.sleep(0.5)
checkLineSensors()

Let us build some motivation for taking on this challenge. Some of the cool things  a robot would be able to do if you teach it to recognize and follow a line are:

Stopping at a line
------------------
The Robot would be able to approach and stop at a line. Or you could have a no-robot zone and would like your robot to not escape a demarked area. In that case, you can use this algorithm to prevent the robot from crossing a line.
Or if your robot is in a maze, you would not want it to cross a line, right? These kinds of navigation tasks can be tackled by using line following algorithms.

Can you think of the logic to execute this task?
You can continuously read the values from the sensor and the moment the sensor intercepts a line (tape), we will see a reading corresponding to the tape and you can then command the robot to do a certain task.
Here is how the code would look like:

# Drive upto a line and stop
def driveToLineAndStop():
    driveBase.setEffort(0.6, 0.6)
    while refl.left() < 5 and refl.right() < 5:
        time.sleep(0.01)
    driveBase.setEffort(0, 0)

driveToLineAndStop()

Staying in a circle
-------------------
You could program a robot to go in circles or a specific pattern. You could draw a pattern using this logic. Wouldn't that be cool?
Here is a program that instructs the robot to turn around a line:
def driveToLineAndStop():
    while True:
        driveBase.setEffort(0.6, 0.6)
        while refl.left() < 5 and refl.right() < 5:
            time.sleep(0.01)
        driveBase.turn(180)
driveToLineAndStop()

Think of how you can use this logic to drive your robot in a circle.

Line following
--------------
Some of the industrial robots still follow lines on the shop floor to move around in the factories. Modern self-driving cars use lines on the roads to maintain lanes. And if that excites you, you are going to enjoy what we learn next! So stay tuned.

Since we know that the tape and ground are going to have different reflectivity values, let us read these values and acknowledge the difference.
So now, when you get a new reading from the sensor, you can make out if the sensor is above the tape or the ground. Isn't it?

To make things interesting, you can use a single sensor or two sensors to do this job. Let us see both of these approaches and decide the best one.

Single sensor line following
----------------------------
Can you think of a logic that would need only one sensor to follow a line?
Here are some hints:
    If the robot is on the line turn off of it
    If the robot is off the line turn towards it

This will result in the robot following an edge of the line. Here is the code for it:
# Single sensor line tracking
def oneSensorLineTrack():
    while True:
        high = 0.75
        low = 0.4
        r = refl.right()
        if (r > 5):
            driveBase.setEffort(high, low)
        else:
            driveBase.setEffort(low, high)
        time.sleep(0.01)
Here is the diagramtic interpretaion of the above code:

.. image:: single_sensor_line_following.png 
    :align: center 
Two sensor line following
-------------------------
Similarly here is the logic if you can use two sensors:

# Two sensor digital line tracking
def twoSensorLineTrack():
    while True:
        high = 0.75
        low = 0.4
        r = refl.right()
        l = refl.left()
        if (r > 5):
            driveBase.setEffort(high, low)
        elif (l > 5):
            driveBase.setEffort(low, high)
        else:
            driveBase.setEffort(high, high)
        time.sleep(0.01)


Proportional control for line following
---------------------------------------
The strategy is that you are trying to minimize the error. The error in the reading from the right or left sensors.
A clever appraoch would be to add the error value to the left wheel and subtract it from the right wheel. We can introduce a constant gain to improve the correction.

Here is a sample code:
def lineTrack():
    baseEffort = 0.6
    Kp = 0.02
    while True:
        error = refl.right() - refl.left()
        driveBase.setEffort(0.6 + error * Kp, 0.6 - error * Kp)

Proportional control with one sensor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Proportional control with two sensors
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Driving around a course for best time
-------------------------------------

