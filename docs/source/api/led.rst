
LED
===================================

On the Adafruit Maker Pi RP2040, there are two LED lights that can show any color in RGB format, labeled on the board as GP20 and GP21 respectively.


.. py:function:: led.set_color(red: int, green: int, blue: int):

        Sets the color of the led by taking in the RGB representation of the color
        :param red: The red value [0-255]
        :type red: int
        :param green: The green value [0-255]
        :type green: int
        :param blue: The blue value [0-255]
        :type blue: int

.. py:function:: led.set_brightness(brightness: float):
        
        Sets the brightness of the two LEDs on the board
        :param brightness: The brightness to set the LEDs to [Bound from 0 (off) to 1 (max)]
        :type brightness: float
        
   