Now that you're create the physical device, we will install the appropriate software for you to communicate with it.

## Installing the necessary software packages

1.  Create a folder in your “Documents” to keep all non-applications files for your project
    1.  You can create the folder somewhere else, but use this for reference.
2.  Download the Arduino IDE
    1.  Go to the Arduino download page - <https://www.arduino.cc/en/Main/Software>
        1.  These instructions have been tested with Arduino 1.8.9 on Windows
        2.  On Mac – menu instructions will be found under the Arduino Menu
    2.  Install Arduino with the defaults, or modify as you see fit
3.  After installing Arduino, install the appropriate ESP32 Chipset
    1.  Open Arduino
    2.  Click on File in the top navigation
    3.  Click on Preferences
    4.  Enter “<https://dl.espressif.com/dl/package_esp32_index.json>” in the “Additional Boards Manager URL’s” field
    5.  Click OK
    6.  Click on Tools in the top navigation
    7.  Click on Board, then click on Boards Manager
    8.  In the search field, type “ESP32”
    9.  Click on “esp32 by Espressif Systems”
    10. Select the latest version
    11. Click on “Install”
4.  Next, we need to download the DHT22 drivers
    1.  In Arduino, click on Tools in the top navigation
    2.  Click on "Library Manager"
    3.  In the search filed, type "DHT22"
    4.  Click on "DHT Sensor Library by Adafruit"
    5.  Select the latest version
    6.  Click on "Install"
    7.  Close the Library Manager
5.  Last we install the AWS_IoT Drivers. Since we don’t need the full library, we will use the Hornbill library for the subset
    1.  Go to the Hornbill GitHub repo - <https://github.com/ExploreEmbedded/Hornbill-Examples>
    2.  Click on “Clone or download” on the left
    3.  Click “Download Zip”
        1.  Save this file to your project folder
    4.  Navigate through the following folders
        1.  Hornbill-Examples-master
        2.  arduino-esp32
    5.  Copy the AWS_IOT Folder to the Arduino IDE installation Libraries folder
        1.  The default on Windows is “C:\\Program Files (x86)\\Arduino\\libraries\\”
        2.  The default for Mac’s is “ \~/Documents/Arduino/libraries/”
    6.  Open the folder called “AWS_IOT”
    7.  Open the folder called “src” inside “AWS_IOT”
    8.  Rename the file “aws_iot_certificates.c” to “aws_iot_certificates.c.old”
6.  With the board drivers installed, now select the board in Arduino
    1.  Close and reopen Arduino
    2.  Click on Tools in the top navigation
    3.  Click on Board
    4.  Select the “DOIT ESP32 DEVKIT V1” board
7.  Close Arduino for now

Once complete, we can begin creating the necessary connection to AWS IoT Core. This will give us the appropriate information and credentials we need to push code to connect to the AWS IoT Core service. Please move on to [Register your devices to AWS IoT Core](Register%20devices%20to%20AWS%20IoT.md).
