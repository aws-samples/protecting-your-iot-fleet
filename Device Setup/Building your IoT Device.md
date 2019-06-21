If you are starting from scratch for this project, this document will help you find the right parts and build your IoT Device.

# Physical wiring

## Required Components

1.  ESP32 Chip
    1.  <https://smile.amazon.com/gp/product/B0718T232Z/ref=ppx_yo_dt_b_asin_title_o02_s02?ie=UTF8&psc=1>
2.  DHT22 Sensor
    1.  <https://smile.amazon.com/gp/product/B0795F19W6/ref=ppx_yo_dt_b_asin_title_o02_s02?ie=UTF8&psc=1>
3.  Breadboard
    1.  <https://smile.amazon.com/gp/product/B07PCJP9DY/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1>
4.  Jumper Wires
    1.  <https://smile.amazon.com/gp/product/B005TZJ0AM/ref=ppx_yo_dt_b_asin_title_o02_s02?ie=UTF8&psc=1>
5.  5 Volt power supply & USB micro cable
    1.  Any cell phone power supply will work for a single device, standard Micro-b plug as well

## Installation

1.  Place the breadboard down with the numbered rows reading 1-30 top to bottom.
2.  Install the USP32 chip so that the USB port is at the bottom. This will put the last pins are in Row 30. This will put the first pins in row 12. The Pins will go in columns B and I
3.  Install the DHT22 sensor in Column J, Rows 1-3 facing outwards
4.  Install a white jumper wire from **Row 30 Column A** to **Row 30 on the red “+” column** on the far left
    1.  This is the 5V pin on the ESP32 Chip
    2.  You can choose whatever color you want, just be consistent using the same color for the positive and negative
5.  Install a white jumper wire from **Row 1 on the red “+” column** to **Row 3 Column F**
    1.  This will provide 5V power to the DHT22
6.  Install a black jumper wire from **Row 12 Column J** to **Row 30 on the blue “-” column** on the far left
    1.  This is the ground pin on the ESP32 Chip
7.  Install a black jumper wire from **Row 1 on the blue “-” column** to **Row 1 Column F**
    1.  This will provide ground to the DHT22
8.  Install a yellow jumper wire from **Row 23 Column J** to **Row 2 Column F**
    1.  This connects the data pin on the ESP32 to the Control pin on the DHT22

Here is the end result.

![](../images/IoT_device_top_view.png)

![](../images/IoT_device_side_view.png)

Once these steps are complete, you can move on to [Connect devices to your laptop](Connect%20devices%20to%20your%20laptop.md). Here you will install the appropriate software on your computer to connect to the device.
