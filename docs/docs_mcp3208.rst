.. module:: mcp3208

*********************
 MCP3204/3208 Module
*********************

This module contains the driver for Microchip MCP3204/3208 analog to digital converter with
SPI serial interface (`datasheet <http://ww1.microchip.com/downloads/en/DeviceDoc/21298e.pdf>`_).

Example: ::
        
        from microchip.mcp3208 import MCP3208
        
        ...
        
        mcp = mcp3208.MCP3208(SPI0, D17)
        value_0 = mcp.get_raw_data(True, 0)
        value_1 = mcp.get_raw_data(False, 2)
    
    
===============
 MCP3208 class
===============


.. class:: MCP3208(spidrv, cs, clk = 400000)

    Creates an instance of the MCP3208 class. This class allows the control of both MCP3204 and MCP3208 devices.
    
    :param spidrv: SPI Bus used '(SPI0, ...)'
    :param cs: Chip select pin
    :param clk: Clock speed, default 400 kHz
    
    
.. method:: get_raw_data(single, channel)
    
    Return the conversion result as an integer between 0 and 4095 (12 bit).
    
    Input mode and channel are selected by *single* and *channel* parameters
    according to the following table.
    
    ========== ========== ====================  ====================
    single      channel    Input Configuration   Channel Selection  
    ========== ========== ====================  ====================
       True        0          single-ended              CH0         
       True        1          single-ended              CH1         
       True        2          single-ended              CH2         
       True        3          single-ended              CH3         
       True        4*         single-ended              CH4         
       True        5*         single-ended              CH5         
       True        6*         single-ended              CH6         
       True        7*         single-ended              CH7         
       False       0          differential      CH0 = IN+ CH1 = IN- 
       False       1          differential      CH0 = IN- CH1 = IN+ 
       False       2          differential      CH2 = IN+ CH3 = IN- 
       False       3          differential      CH2 = IN- CH3 = IN+ 
       False       4*         differential      CH4 = IN+ CH5 = IN- 
       False       5*         differential      CH4 = IN- CH5 = IN+ 
       False       6*         differential      CH6 = IN+ CH7 = IN- 
       False       7*         differential      CH6 = IN- CH7 = IN+ 
    ========== ========== ====================  ====================
    
    .. note:: *channel* values marked with * are available for the MCP3208 only. 
    
    The digital output code is determined by the reference voltage *Vref* and the analog input voltage *Vin*:
    
    Digital output code = 4096 * *Vin* / *Vref*
    
    
