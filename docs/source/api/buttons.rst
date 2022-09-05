
Buttons
===================================

Getting button input
--------------------

On the Adafruit Maker Pi RP2040, there are two buttons that can recieve input accessible in the code, labeled on the board as GP20 and GP21 respectively. 

.. py:function:: buttons.is_GP20_pressed() -> bool
    
    Get whether the GP20 button on the RP2040 microcontroller has been pressed
    
    :return: if the GP20 button was pressed
    :rtype: bool

.. py:function:: buttons.is_GP21_pressed() -> bool
    
    Get whether the GP21 button on the RP2040 microcontroller has been pressed

    :return: if the GP21 button was pressed
    :rtype: bool
   