# Extra Credit

There is so much more you can do with Device Defender beyond what we could capture in a single hour. Here are some more advanced actions you can take if you have extra time.

## 1. Trigger Automated Response to Violations
Device Jobs allow a user-specified on-device response to a Job Document. Jobs can be targeted at individual Things, or Thing Groups.  Jobs can run continuously, so that as Things are added to a group, a job is triggered. This pattern works well when there are automated steps we can take to remediate issues.

1. First, let's create a new **Thing** **Group** called "**NeedsUpdate**"

For the sake of not wasting time, let's assume a scenario. In the "acceptablebehavior" Security Profile we created, we could have taken action on devices that were out of tolerance. Actions can include calling a Lambda function, such a a function that would add a Thing to a specific Thing Group. For the following steps, assume this has been created and done. If you wish to test it out and see it occurring, you will have to write your own Lambda script at this time.
    
2. Let’s **Manage** our **Jobs** to start.
    1. A job is just a free-format JSON document, that the device can read to trigger some action or set of actions
3. In a **new tab** download the **config.json** file from <https://github.com/aws/iot-atlas/raw/master/config.json> to use as an example.
4. **Upload** the file you just downloaded to an **S3 bucket** in your account
    1. If you don't have an S3 bucket, just **create a private S3 bucket** for now.
5. Back on the IoT Core console, **Create a job**, using the **Custom** option
6. **Update-temp-firmware** would be a good name for a job targeting **selected devices to update** in the **Thing Group** **NeedsUpdate**.
7. We will **add a job file** by **Selecting** the S3 bucket and .js file we just downloaded.
8. Being this is something  all devices should have, set the **Job Type** to a **continuous** deployment.
9. Accepting the rest of the defaults for now we can **Create** this job.

So what we've just done is created a system by which any IoT device that ends up out of tolerance from our expected behavior gets automatically reflashed with new (example) code of our choosing. This is a great way to automatically detect and remediate issues in your IoT fleet.

## 2. Using IoT Rules, CloudWatch, and CloudWatch events to auto-remediate
1.	If we wanted to **Act** upon certain behaviors, we could use **Rules**
2.	**Create** a rule that could, for example, identify **HighHumidity** coming from the sensor
    1.	This could be defined as Humidity above 50%, or in SQL terms **SELECT Humidity FROM '$aws/things/IoT-Temperature-Device/shadow/update' WHERE Humidity > 50**
    2.	There are now 15 different native actions we could take, and using Lambda nearly infinite. For now let’s **Send message data to CloudWatch**
    3.	We define a metric for CloudWatch.
        1.	**HighHumidity**
        2.	in a namespace like **IoT**
        3.	with a unit of **Count**
        4.	and a value of **1**
    4.	Since we haven’t done this before, we can **Create a new role** named **IoTtoCloudWatchAlerting** to permit Device Defender to send the data
    5.	We don’t need an Error Action, so we can **Create rule**

Let’s kick this action off. First, **plug the yellow cable back in** if you still have it disconnected. The Temperature sensor we are using can be tricked into giving weird readings. To get this effect, **gently hold finger on the front of the sensor for about 60 seconds**. The sensor will either lose its mind, or register a high humidity, or both.

3.	To see which one, let’s open **CloudWatch** in a **new tab** from the Services drop down.
4.	We want to check **Metrics**, specifically **IoT - Rule Metrics** called **HighHumidity**.
5.	**Check the box** to add it to the graph
6.	To see how many times it failed, set the **Graphed Metric** Statistic to **Sum** for a period of **1 minute**.
7.	Set your window size to a **Custom 30 minutes** to see a good example.

Here you see the humidity rule has been tripped. This means something is wrong with the device. Now remember, we didn’t have to just create a CloudWatch alarm, we very easily could have sent notifications to engineering teams using SNS, add rows to a TroubleTicket DynamoDB table, or taken custom action using Lambda scripts. But what else should we do when a sensor is misbehaving and potentially malicious?

## 3. Stopping bad Things from sending data by revoking a certificate
1.	**Close** the CloudWatch tab 
2.	Going back to **Device Defender** (in the breadcrumb navigation) we want to update our **Things** Security
3.	Checking the **Security** of the bad sensor we can see the details of the **Certificate**
4.	A good **Action** to take for a known bad sensor would be to **Revoke** its Certificate
5.	Now let’s monitor the **IoTTemperatureDemoDevice** Thing’s **Activity**
6.	After a minute or so does the Thing stop communicating?
7.	Does this count towards **Violations** of any of the Security Profiles we setup?
    
Now we’re not just auditing against configuration standards, but also auditing and acting upon IoT device behaviors in the real world.
