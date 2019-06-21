In this set of instructions we will use our AWS account to create an IoT Device Thing and Shadow. We will also create the certificates and policies required for communication and execution of steps in the Session.

## Creating Certificates and Things for your IoT Device

1.  Go to your AWS Account
    1.  Make sure you’re in a region that supports IoT – We have tested in us-east-1
2.  Go to the IoT Core Service
3.  Click on “Manage” in the left-hand navigation
    1.  Notice you start in the “Things” interface
4.  Click on “Register a thing”
    1.  If you already have Things created, click on “Create” on the top right
5.  Click “Create a single thing”
6.  Type “IoT-Temperature-Device” in the “Name” field
7.  Click the “Create a type” Button
    1.  Type “ESP32-Things” in the “Name” field
    2.  Type “Purpose” in the “Tag name” field
    3.  Type “Demo” in the “Value “ field
    4.  Click the “Create thing type” button
8.  Click “Create group”
    1.  Type “TemperatureSensors” in the “Name” field
    2.  In the “Set group attributes” type “Core” in the “Attribute Key” field
    3.  Type “ESP32” in the “Value “ field
    4.  Click “Add another”
    5.  Type “Sensor” in the “Attribute Key” field
    6.  Type “DHT22” in the “Value “ field
    7.  Click the “Create thing group” button
9.  Click the “Next” button
10. Click the “Create certificate” button
11. Download all three certificates in your project folder
12. In a new window open the link to download the root CA for AWS IoT Certificate in your project folder
    1.  This link takes you to another page (<https://docs.aws.amazon.com/iot/latest/developerguide/managing-device-certs.html#server-authentication>)
    2.  Download the RSA 2048 bit key to your project folder by right clicking and “Save Link As”
13. Back in the AWS IoT Console, click the “Activate” button
14. Click the “Attach a policy” button
    1.  We haven’t built a policy, so we will attach that later
15. Click the “Register Thing” button
16. Click on “Secure” in the left-hand navigation
    1.  Notice you start in the “Certificates” interface
17. Click on “Policies” in the left-hand navigation
18. Click “Create a policy”
    1.  Type “TemperatureSensorPolicy” in the “Name” field
    2.  Type “iot:\*” in the “Action” field
    3.  In the “Resource ARN” field, replace the entire ARN with “\*”
    4.  Click on the right box before “Allow”
    5.  Click the “Create” button
19. Click on “Manage” on the left-hand navigation
20. Click on “Thing Groups” on the left-hand navigation
21. Click on the group you created
22. Click on “Security” on the left-hand navigation
23. Under “Select a policy to attach to this group”, click on “Select”
24. Click on the sensor policy you created
25. Click on Save

We now have an AWS Thing created with a policy and a certificate. We now gather information needed to communicate with the AWS IoT Thing.

26.  Click on the left arrow in the top left
27.  Click on “Things” on the left-hand navigation
28.  Click on the Thing you created
29.  Click on “Interact” on the left-hand navigation
30.  Open a text editor
31.  Copy the Rest API Endpoint listed under “HTTPS” and put it in the text editor
    1.  This will look like {random characters}-ats.iot.{region}.amazonaws.com
32.  Copy the name of your Thing and put this in the text editor
    1.  This can easily be found at the top of the screen
33.  Copy the field labeled “Update to this thing shadow” under “MQTT” and put this in the text editor

With these steps complete we now have the device built, connectivity to our computer, and the necessary information to push to the device for communication to open with AWS IoT Core. The next steps will be to create a Arduino sketch with the code to execute and the appropriate certificate file. This will be done in [Push files to your IoT Device](Set%20up%20devices.md).
