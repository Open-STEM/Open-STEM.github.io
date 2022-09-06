
Drivetrain
===================================


.. py:function:: drivetrain.go_straight(distance: float, speed: float = 0.5, timeout: float = None) -> None

    Go forward the specified distance in centimeters, and exit function when distance has been reached. Speed is bounded from -1 (reverse at full speed) to 1 (forward at full speed)

    :param distance: The distance for the robot to travel (In Centimeters)
    :type distance: float
    :param speed: The speed for which the robot to travel (Bounded from -1 to 1). Default is half speed forward
    :type speed: float
    :param timeout: The amount of time before the robot stops trying to move forward and continues to the next step (In Seconds)
    :type timeout: float
    :return: if the distance was reached before the timeout
    :rtype: bool

.. py:function:: drivetrain.go_turn(turn_degrees: float, speed: float = 0.5, timeout: float = None) -> bool:
        
    Turn the robot some relative heading given in turnDegrees, and exit function when the robot has reached that heading. Speed is bounded from -1 (turn counterclockwise the relative heading at full speed) to 1 (turn clockwise the relative heading at full speed)

    :param turn_degrees: The number of angle for the robot to turn (In Degrees)
    :type turnDegrees: float
    :param speed: The speed for which the robot to travel (Bounded from -1 to 1). Default is half speed forward.
    :type speed: float
    :param timeout: The amount of time before the robot stops trying to turn and continues to the next step (In Seconds)
    :type timeout: float
    :return: if the distance was reached before the timeout
    :rtype: bool

.. py:function:: drivetrain.set_effort(left_effort: float, right_effort: float) -> None:

    Set the raw effort of both motors individually

    :param left_effort: The power (Bounded from -1 to 1) to set the left motor to.
    :type leftEffort: float
    :param right_effort: The power (Bounded from -1 to 1) to set the right motor to.
    :type rightEffort: float

.. py:function:: drivetrain.stop() -> None:
    
    Stops both drivetrain motors

.. py:function:: drivetrain.get_left_encoder_position() -> float:
        
    Return the current position of the left motor's encoder in degrees.
    
.. py:function:: drivetrain.get_right_encoder_position() -> float:
        
    Return the current position of the right motor's encoder in degrees.
    
.. py:function:: drivetrain.set_encoder_position(left_degrees: float, right_degrees: float) -> None:

    Set the position of the motors' encoders in degrees. Note that this does not actually move the motor but just recalibrates the stored encoder value. If only one encoder position is specified, the encoders for each motor will be set to that position.

    :param left_degrees: The distance to recalibrate the left encoder to.
    :type leftDegrees: float
    :param right_degrees: The distance to recalibrate the left encoder to.
    :type rightDegrees: float
