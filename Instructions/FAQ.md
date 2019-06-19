# Frequently Asked Questions

## Setup and Build

1.  When I try to compile my IoT device code it complains with a “DHT.h” missing error.
    *  This means the Adafruit sensor library was not downloaded appropriately. Please return to Step 4 of the [Connect devices to your laptop](./Device%20Setup/Connect%20devices%20to%20your%20laptop.md) instructions.
2.  I’m getting an compile error: “libraries/AWS_IOT/aws_iot_certficates.c.o:(.rodata.aws_root_ca_pem+0x0): multiple definition of aws_root_ca_pem, certificate_pem_crt, or private_pem_key”
    * This means Arduino has found two versions of the aws_iot_certificate.c file. Likely you have not renamed the aws_iot_certificates.c c within the AWS_IOT library folder per Step 5 of the [Connect devices to your laptop](./Device%20Setup/Connect%20devices%20to%20your%20laptop.md) instructions. Make sure that you rename the file in the AWS_IOT folder to aws_iot_certificates.c.old.
3.  The port for my device is not showing up on my Macbook. This only has USB-C ports and uses a dongle to for USB 2.0, 3.0.
    * This is likely due to you not using the Apple dongle or you are missing a driver. If you are using the Apple dongle but do not see the USB port, you will need to install the ESP32 driver for Mac. The best instructions for that can be found in step 5 Lab 0 of the [AWS IoT Workshop lab](https://github.com/aws-samples/aws-iot-workshop#lab-0-this-environment-doesnt-seem-that-hostile).
4.  I can connect to the IoT Device and see the default executable searching for wifi. But when I try to push my code I see
        ```
        Connecting........_____....._____....._____....._____....._____....._____....._____
        A fatal error occurred: Failed to connect to ESP32: Timed out waiting for packet header
        ```
    * This means the ESP32 chip is not going into flash/upload mode automatically. You can solve this problem by holding-down the “BOOT” button in your ESP32 board when you see the "Connecting....." text. The "BOOT" button if the one to the right of the USB plug.
