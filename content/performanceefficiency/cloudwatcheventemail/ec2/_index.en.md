---
title: "EC2 Loadtest"
weight: 323
pre: "<b>3. </b>"
---

### After increasing the CPU usage of EC2, we will check the dashboard:
---
When the CPU usage increases, Autoscaling Group automatically increases the number of EC2 Instances. And we'll see that change on Cloudwatch's dashboard.

#### Web access through application load balancer

1. The DNS address of the Application Load balancer is in the **Output** in **WellArchitectedFrameworkLabsStack** created before.

    Open theCloudFormation Console : https://ap-northeast-2.console.aws.amazon.com/cloudformation/home?region=ap-northeast-2
 
1. Select WellArchitectedFrameworkLabsStack. 
    ![CloudwatchDashboard](/images/war/cloudwatch-stack.png#medium)

1. The `ALBDNS` in output is the DNS address of the Application Load Balancer. After selecting the output in the upper tab, copy the value of `ALBDNS` and put it in the address bar of your web browser.
    ![CloudwatchDashboard](/images/war/cloudwatch-albdns.png#medium)

1. You can see the this screen.
    ![CloudwatchDashboard](/images/war/cloudwatch-ec22.png#medium)
    The CPU usage of this web server is 0%. When you click the Load test button at the top, the screen changes and the CPU load of EC2 rises to 100%.
    ![CloudwatchDashboard](/images/war/cloudwatch-ec2-loadtest2.png#medium)
    CPU load will not go down until you exit this screen.

1. Let's go to the CloudWatch console and see the user dashboard we created earlier.

    Open the CloudWatch : https://console.aws.amazon.com/cloudwatch/ 

1. Select **Dashboards** on right top. 
    ![CloudwatchDashboard](/images/war/cloudwatch-dashboard.png#medium)

1. Select the `warworkshop-default`. 
    ![CloudwatchDashboard](/images/war/cloudwatch-ec2-dashboard.png#medium)

1. The monitoring default pefiod is 5 minutes (this can be changed in settings).Refresh after 5 minutes and you will see the CPUUtilization graph that has changed drastically towards 100%. And after a little more time, you can see that the Autoscaling group has expanded up to 4 instances.
    ![CloudwatchDashboard](/images/war/cloudwatch-change.png)

1. Also check your mail. You can check that the alert has been sent to the previously registered email.
    ![CloudwatchDashboard](/images/war/cloudwatch-alarm-mail.png)
    If you have registered your mobile phone number, you can also receive text messages.

1. If you go to the EC2 Dashboard, you can also check the automatically expanded EC2.
      ![CloudwatchAlarm](/images/war/cloudwatch-ec2-autoscaling.png#medium)

1. you leave the loadtest window, after a while you can see the two instances and the stable graph.

Use Cloudwatch to monitor optimal performance. System performance can degrade over time. Monitor system performance to identify degraded conditions and resolve internal or external factors such as operating system or application load. Create an alarm to check changes in system performance.

---
 