
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
