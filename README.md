# Protecting-your-IoT-Fleet
This repository contains a list of instruction for Builder Session SDD307 at AWS 2019 re:Inforce. It provide instruction on how to use AWS IoT to securely manage your IoT Devices

# Prerequisite: set up and configure devices
If you follow this lab as part of Builder Session at re:Inforce 2019, devices are already configured. You will not need to do this prerequisite. This step is required if you do this lab on your own.

[Build your IoT Device](Device%20Setup/Building%20your%20IoT%20Device.md) - This set of instructions will walk you through the building of your IoT Device for this Session

[Connect devices to your laptop](Device%20Setup/Connect%20devices%20to%20your%20laptop.md) - After building thde device, these instructions help you install the appropriate software on your computer to connect to the device.

[Register your devices to AWS IoT Core](Device%20Setup/Register%20devices%20to%20AWS%20IoT.md) - And last, these instructions then connect the device to your AWS IoT Account

[Push files to your IoT Device](Device%20Setup/Set%20up%20devices.md) - Once connected, these instructions walk you through pushing the appropriate code and certificates to your IoT Device.

# Protecting your fleet using AWS IoT Device Defender
Welcome to learning how to protect your IoT fleet at scale using AWS IoT Device Defender. In this session we will perform the following actions to get familiar with how this service can help you manage and maintain a secure fleet of IoT devices.

1. Use the console to validate a “Thing” exists and how it is used
2. See how certificates authorize Things to talk to AWS IoT
3. Evaluate Device Groups to set permissions on groups of Things
4. Monitor Thing Activity from the console
5. Create and review Audit Schedules for your account
6. Use Device Defnder to Detect rule-based and anomoloy-based deviations in behavior
7. Enable automated remediations in response to these events
 
Follow this [instruction to start the lab](Instructions/Instruction.md) 

Once done, we recommend you clean up the elements you created to ensure you don't get charged for your demo environment.

# Remember to clean up if you do this lab at your own pace.
Follow this [instruction to clean up](Clean%20up.md)

## License Summary

The documentation is made available under the Creative Commons Attribution-ShareAlike 4.0 International License. See the LICENSE file.

The sample code within this documentation is made available under the MIT-0 license. See the LICENSE-SAMPLECODE file.

