---
title: "CloudWatch Custom Dashboard"
weight: 312
pre: "<b>2. </b>"
---

### CloudWatch Custom Dashboard
---
 
Let's measure CPU utilization and Instance Count attached ALB.

1. First you need Auto scaling group name, and Application load balancer name.  

    Go to CloudFormation console : https://ap-northeast-2.console.aws.amazon.com/cloudformation/home?region=ap-northeast-2

1. Output's `ASGName` is name of Auto scaling group. `ALBName` is name of Application Load Balancer 
    Click `MasterAccountStack` at CloudFormation console. 
    ![CloudwatchDashboard](/images/war/cloudwatch-stack.png#medium)

    Click Output tab and copy somewhere value `ASGName`and `ALBName`.
    ![CloudwatchDashboard](/images/war/cloudwatch-stack-output.png#medium)

    Let`s make CloudWatch Dashboard.
    Go to CloudWatch : https://ap-northeast-2.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-2

1. Select **Dashboards** where right top.
    ![CloudwatchDashboard](/images/war/cloudwatch-dashboard.png#medium)

1. Click **Create Dashboard** button. 
    ![CloudwatchDashboard](/images/war/cloudwatch-createdashboard.png#medium)
 
1. typing at `warworkshop-default` dashboard name. And click **Create dashboard** button for generate basic dashboard.
    ![CloudwatchDashboard](/images/war/cloudwatch-create-fin.png#medium)

1. Now we add widget for watch EC2 CPU utilization at dashboard. Select **Line Compare metrics over time** and click **Configure**.
    ![CloudwatchDashboard](/images/war/cloudwatch-detail.png#medium)

1. Paste the valut of ASGName from the previously copied output into the All metrics search bar. And click enter and choose **EC2 > By Auto Scaling Group**
    ![CloudwatchDashboard](/images/war/cloudwatch-metric.png#medium)

1. You can show variable Metrics. Now click **CPUUtilization** Metric name. Click **Create Widget** button. 
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-cpuutilization.png#medium)

1. Check dashboard added CPUUtilization. next we add EC2 instance count widget. Click **Add Widget** button at menu bar
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-widget.png#medium)

1. In this case, We use **Number** type. Select **Number** type and click Configure button.
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-widget-select.png#medium)

1. Paste the valut of ASGName from the previously copied output into the All metrics search bar. And click enter and choose **ApplicationELB > Per AppELB, per TG Metrics**
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-alb.png#medium)

1. Select `HealthyHostCount` and click **Create widget** button.
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-healthy.png#medium)

1. You can see that there are very low CPU usage and 2 instances. Save the dashboard.
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-fin.png#medium)


[Now let's create a Cloudwatch alarm so users can immediately notice changes in CPU utilization.](/en/performanceefficiency/cloudwatcheventemail)
 
