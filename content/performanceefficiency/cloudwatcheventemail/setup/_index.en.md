---
title: "Custom Alram Configuration"
weight: 321
pre: "<b>1. </b>"
---

### CloudWatch Alram
---
We will measure the CPU usage and number of instances in WellArchitectedFrameworkLabsStack which is created in CloudFormation.
 
Open CloudWatch : https://console.aws.amazon.com/cloudwatch/ 

1. From the left menu, select Alarms, and click **Create alarm**
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm.png#medium)

1. Click Select metric.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-metric.png#medium)

1. Paste the value of ASGName from the previously copied output into the All metrics search bar. Select `EC2 > By Auto Scaling group`.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-asg.png#medium)

1. Find the  Metric **CPUUtilization**, and check the box, and click the **Select Metric** button.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-cpu.png#medium)

1. Let`s configure **Specify metric and conditions**. We make alram when CPUUtilization **metric** is over 90%. Select **p90** in **Statistic**. For **Period,** select **1 minute**.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-setting.png#medium)

1. For **Conditions**, select **Static** for a Threshold type. Select **Greater** for 'Whenever CPUUtilization is..' Lastly, type 95 for **than..**.
    ![CloudwatchAlarm](/images/war/cloudwatch-percent.png#medium)

1. Click **Next**.

1. Let's make new SNS topic. Select  **in alarm** at **Alarm state trigger**, check **Create new topic** radio bax in **Select an SNS topic** panal. and typing `Default_CloudWatch_Alarms_Topic` in  **Create a new topic...** box, enter your email address in **Email Endpoint**, click **Create topic** button. 
    ![CloudwatchAlarm](/images/war/cloudwatch-create-topic.png#medium)
1. Click **Next**.
1. Enter the following in Add **Alarm name** and **Alarm description**.
    - **Alarm name** : `CloudWatch-CPU-Alarm`
    - **Alarm description - optional** : `for WAR workshop`
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-fin.png#medium)

1. Click **Create alram**. 

[let's add an email and mobile to alram.](/en/performanceefficiency/cloudwatcheventemail/snstopic)

[or you can start load testing right now!](/en/performanceefficiency/cloudwatcheventemail/ec2)


 
