# Flight Computer Hardware Documentation

## Components
- Teensy 4.1 (https://www.pjrc.com/teensy/IMXRT1060RM_rev3_annotations.pdf)
             (https://www.etechnophiles.com/teensy-4-1-pinout/)
- BNO0855 IMU (https://cdn-learn.adafruit.com/downloads/pdf/adafruit-9-dof-orientation-imu-fusion-breakout-bno085.pdf)
            https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bno055-ds000.pdf 
- MS5611 Barometer (https://www.te.com/usa-en/product-MS561101BA03-50.datasheet.pdf)
- MAX-M10S GPS (https://content.u-blox.com/sites/default/files/MAX-M10S_DataSheet_UBX-20035208.pdf)
  
- DS3218MG Servos
- RFM95W LoRa Radio

-  Power regulators
    - TPS5431 (5V) for servos
    - TPS62130 (3.3V) for mcu
 
-  battery
    - 3S LiPo (11.1V)
    - 1300mAh minimum
    - 75C discharge rate
 
-  Power budget
Component    Voltage    Current Draw    Peak Current
Teensy 4.1   3.3V      100mA          150mA
BNO055       3.3V      12mA           -
MS5611       3.3V      1mA            -
MAX-M10S     3.3V      25mA           40mA
Servos       5V        500mA          2A (each)
Radio        3.3V      100mA          120mA
    
Connections______________________________________________________________________________________________
1. **MCU -> IMU.** 
   - use spi for faster data rate, fast updates(100HZ) for attitude control
SCL - This is also the SPI Clock pin / SCK, it's an input to the chip
 SDA - Doubles as the Data Out / Microcontroller In Sensor Out / MISO pin, for
 data sent from the BNO08x 
DI - Datal In / Microcontroller Out Sensor In / MOSI pin, for data sent from your
 processor to the BNO08x
 CS - this is the Chip Select pin, pull it low to start an SPI transaction. It's an input
 to the chip
 INT - Interrupt- Active Low. Indicates that the BNO085 needs the host's
 attention. Required for stable SPI operation
 RST- Reset- Active Low - Pull low to GND to reset the sensor. Required for
 stable SPI operation

4. MCU -> Barometer
   - Use SPI but on different chip select pin than the IMU, good for medium updates (50Hz) for altitude
The external microcontroller clocks in the data through the input SCLK (Serial CLocK) and SDI (Serial Data In). In 
the SPI mode module can accept both mode 0 and mode 3 for the clock polarity and phase. The sensor responds 
on the output SDO (Serial Data Out). The pin CSB (Chip Select) is used to enable/disable the interface, so that 
other devices can talk on the same SPI bus. The CSB pin can be pulled high after the command is sent or after the 
end of the command execution (for example end of conversion). The best noise performance from the module is 
obtained when the SPI bus is idle and without communication to other devices during the ADC conversion. 

6. MCU -> GPS
   - Deosnt have SPI but I2C is fine due to slower updates rate (10Hz) for position
I2C?, use clock(SCL) and data (SDA)
