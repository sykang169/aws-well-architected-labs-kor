---
title: "Subscribe e-mail and mobile number"
weight: 322
pre: "<b>2. </b>"
---

### SNS e-mail Confirm
---

email attached SNS topic have to re-approved in the account to receive Alarm. Find the email from `ÀWS Notification` in the your inbox when setting up the previous step.
   ![CloudwatchAlarm](/images/war/cloudwatch-confirm.png#medium)

Click **Confirm subription**. finished subscribe. 
   ![CloudwatchAlarm](/images/war/cloudwatch-confirm-fin.png#medium)

{{% notice info %}}
The Step below are available in regions that provide SNS.(서울리전은 불가)
{{% /notice %}}

Now, let's add a mobile phone number to the SNS topic so that we can send a mobile text message when an alarm occurs.

Open Amazon SNS console : https://console.aws.amazon.com/sns/ 

1. Select Topics from the left menu.
    ![CloudwatchAlarm](/images/war/sns-topics.png)

1. Select the SNS topic `Default_CloudWatchAlarms_Topic` that you created while creating the alarm.
    ![CloudwatchAlarm](/images/war/sns-topics-select.png#medium)

1. Scroll down and look at **Subscriptions** to see the email you registered when you created the alert. You can add new subscribers here by selecting **Create Subscription**.
    ![CloudwatchAlarm](/images/war/sns-topics-create-sub.png#medium)

1. Select **Protocol** of subscription creation by SMS. (You can use various protocols here.) Then, enter your mobile phone number in the endpoint. (ex+821012345678) And click the **Create Subscription** button at the bottom.
    ![CloudwatchAlarm](/images/war/sns-topics-create-sub-fin.png#medium)

1. If you select `Default_CloudWatchAlarms_Topic` from the previous Topics menu, you can see the email and mobile phone information associated with the topic.

[Now let's see what happens when the CPU usage of EC2 Instance increases.](/en/performanceefficiency/cloudwatcheventemail/ec2)
 
