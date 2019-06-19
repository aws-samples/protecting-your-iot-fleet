1. [Use the console to validate a “Thing” exists and how it is used](#1-validate-and-understand-aws-iot-things)
2. [See how certificates authorize Things to talk to AWS IoT](#2-thing-authorization---certificate-based)
3. [Evaluate Device Groups to set permissions on groups of Things](#3-evaluating-groups-and-permissions)
4. [Monitor Thing Activity from the console](#4-monitoring-the-sensor-in-front-of-you)
5. [Device Defender ‘Audit’ - continuous audit against detect security deviations](#5-Device-Defender-Audit---continuous-audit-against-detect-security-deviations)
6. [Device Defender ‘Detect’ - Security Monitoring and Anomaly Detection in devices](#6-Device-Defender-Detect---Security-Monitoring-and-Anomaly-Detection-in-devices)
7. [Statistical Anomaly Detection - Security Profiles with percentile based behaviors](#7-Statistical-Anomaly-Detection---Security-Profiles-with-percentile-based-behaviors)

For ease of experience, this document outlines the general steps you will take instead of a direct "click here and then here and then here...". This lab should help you learn the interface, so these instructions are more of a guide (with some pretty blatent hints) than a tutorial. 

## 1. Validate and Understand AWS IoT "Things"
1. Go to the **IoT Core** service in the console
    1. Click on Getting Started if you haven't seen this before
2. Looks like we're **Monitoring** something already connected and configured. Right?
3. Since the device is already connected, let's **Manage** the IoT Things.

Looks like you already have a sensor configured. What details can you see about the **Thing**? Make sure to expand the help icon on the right for more information. Can you now piece together how the Thing interacts with the real world?

## 2. Thing Authorization - Certificate-based
1. Go back to the **IoT Core** console {Left arrow on the left}
2. Whre would you expect to find **Security** related configurations like Certificates?
3. What **Details** would you want to know about your certificates?
4. How do we know which Certificates are attached to which **Things**?
5. What **Actions** would you potentially want to see performed on Certificates?

It's important to make sure we trust the messages coming from our sensors. By using certificate based authentication and authorization, we make sure the devices are who they claim to be.

## 3. Evaluating Groups and Permissions

1. Go back to the **IoT Core** console {Left arrow on the left}
2. Permissions can be set in multiple places, but groups help us keep track of like devices. So **Managing Thing Groups** can help us maintain those associates and permissions with them.
3. What **Things** are part of what **Groups** in this demo?
4. What **Security** permissions have been allocated to this group?

Does that policy look right to you?

## 4. Monitoring the sensor in front of you

1. Let's go back to the **Thing** in front of you
2. Is there any **Activity** going on right now? Wouldn"t it be great to **Shadow** the device's changes?
3. How does the real world Thing **Interact** with the shadow?

Okay, so now you have a primer on what exactly the IoT Sensor in front of you is doing and how it interacts with the AWS IoT Core service. You could have dozens, or hundreds of thousands of these devices and they would all work the same way. But auditing dozens vs. hundreds of thousands could be cumbersome if you don"t have the right tools. So let's look at the tools **AWS IoT Device Defender** provides.

## 5. Device Defender ‘Audit’ - continuous audit against detect security deviations

1. Using Device **Defender** you"ll setup on-demand or periodic **audits**.
2. **Getting started with an audit** is a great way to ensure your IoT account is configured securely and stays that way.
3. After **Reviewing Permission** for the Device Defender service, we can approve the defaults and move to what's **Next**.
4. Let's review the **Checks** we can select. What Checks do you think are most relevant to your needs around IoT? Are service-side or IoT side risks more of a threat?
    1. It makes sense to **enable all checks** before moving on to what's **Next**.
5. We're not too worried about alerting right now, so simply **Enabling the audits** would be good for now.
6. While we can see a Daily audit is a great default, let's **Create** our own audit to run now.
7. Let's create one with **all the checks** and **run the audit now** to get a good sense of what our account looks like.
8. After a minute we can view the **Results** of our **On-demand**. 
9. Do the results surprise you? Does **expanding** the compliant checks provide insight on how it can scan thousands of authentication issues very quickly?

These audits will ensure your Account configuration, your Device configuration, and your Authentication configuration to all be audited. There are some good questions that you can ask yourself as you create your IoT ecosystem including:
1. How do you ensure your permissions are set up right and follow the principle of least privilege (PoLP)?
2. How do you ensure that your certificates are secure?
3. If your devices use ClientID are they re-using clientID causing legitimate connections to be dropped (DoS)?

The last question also bring up a new question - what about device behavior? What about monitoring devices and acting upon issues in real time? What would that look like?

## 6. Device Defender ‘Detect’ - Security Monitoring and Anomaly Detection in devices

1. If we want to **Detect** behavior changes in a Thing, we need to define the right **Security profiles**

The first question we have to ask ourselves is: what should the device behavior actually look like? There's also an opportunity here  when grouping devices so that all devices with similar expected behavior are in the same group.

2. To **Create your first Security Profile**, we need to 
3. We can define a **Profile** of **acceptablebehavior** then create some behaviors for some things we care about – 
    1. Auth Failures should always be less than 0 (unless someone is trying to do something they do not have permissions to)
        1. Behavior named **GoodAuthentication** could be defined as **Authorization failures** of **Absolute Value** **Less than or equals** **"0"** **every 5 minutes**. Today we don't want to notify anyone, but we do want to **Attach to** a **Specific Things Group**, say the **TemperatureSensors**. We should **Save** that idea and **Continue**.
    2. Message size less than 1 (since message size and # of messages are a cost factor, we want to guard against billing abuse) 
        1. Additionally, we know our **SmallMessages** should be defined as **Message Size** of **less than** "**1**". We still don't want to notify anyone, but this should apply to **All Things**.
        2. But when we set this alert up, we realize we want to **retain additional metrics** around the **Connection Attempts**. This way we can track where bad messages are coming from and visualize it later.
4. Checking out the **Profile Name** of the Security Profile we setup, we can see if Things have any **Violations**
5. We can also check the **Defender Metrics** to visualize the data we've captures.
6. Looking at the **Connection Attempts** **Average** over the **last 24 hours** for example will show us whether the alerms have additional, actionable telemetry.

In reality we would set the message size higher, but this allows us to see how, if an IoT sensor starts sending bad data we could sense it and create an alarm. But what about acting upon issues in real time? What would that look like?

## 7. Statistical Anomaly Detection - Security Profiles with percentile based behaviors  

It's always nice when you know the exact behavior of you devices, but what about when there's variation you may not be able to predict. How can we use statistical anomaly detection to identify things out of bounds?

1. Let's **Create** another Security Profile
2. A profile named **SensorDisconnect** describing the behavior of **NoData** when **Messages Received** fall out of a **Statistical Threshold** **less than** **P50** for **5 minutes** with **1** data point to alarm on. We would not notify anyone, but we would **Attach** this to **All things**. Of course we **Save** and **Continue** with this.
    1. This will alert us when a device falls below 50% of the expected Messages Received for 5 minutes based on past data.

Now to trigger this last finding, we will disconnect the DHT22 sensor from the device. Gentle grasp the yellow wire and pull it out of the breadboard. Now we can wait 5 minutes and watch as the sensor doesn't update and the alarm will get triggered.

3. Checking out the **SensorDisconnect** **Profile Name**, we can see if Things have any **Violations**.
    1. Here we should see that the device has fallen below the threshold (as long as enough time has passed) and is in alarm

With one device all of this was easy to see and literally put our hands on. But again - imagine tens of thousands of devices. Instead of having to monitor them and manage them as individuals, we can use Things, Certificates, Groups, and Detection capabilities to ensure we have a high degree of Confidentially, Integrity, and Availability for our customers. If you want to take it further and see how you can then **Act** upon these alarms, use CloudWatch events to monitor data metrics, or even execute lambda functions straight from Device Defender, check out the [Extra Credit](extra-credit.md).

This completes the session around how to use AWS IoT Device Defender to protect your IoT fleet at scale. If you want to clean up the work you've done here, use the [Cleanup Instructions](../Clean%20up.md)
