# Flight Computer Hardware Documentation

## Components
- Teensy 4.1 (https://www.pjrc.com/teensy/IMXRT1060RM_rev3_annotations.pdf)
             (https://www.etechnophiles.com/teensy-4-1-pinout/)
- BNO0855 IMU (https://cdn-learn.adafruit.com/downloads/pdf/adafruit-9-dof-orientation-imu-fusion-breakout-bno085.pdf)
- MS5611 Barometer (https://www.te.com/usa-en/product-MS561101BA03-50.datasheet.pdf)
- MAX-M10S GPS (https://content.u-blox.com/sites/default/files/MAX-M10S_DataSheet_UBX-20035208.pdf)
  
- DS3218MG Servos
- RFM95W LoRa Radio

-  Power regulators
    - TPS5431 (5V)
    - TPS62130 (3.3V)
 
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
    
