---
title: "Attach CloudWatch IAM role to selected EC2 Instances"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 2
---

1. We are now going to attach the IAM Role created on the previous step in one of our EC2 Instances, to do that let's go to the **Amazon EC2 Dashboard**.
    ![Images/MemInstall01.png](/cost/200_aws_resource_optimization/Images/MemInstall01.png)

1. On the left bar, click on **Instances**.
    ![Images/MemInstall02.png](/cost/200_aws_resource_optimization/Images/MemInstall02.png)

1. Click on **Launch Instance** and select **Linux 2 AMI (HVM)** and **t2.micro** (free tier eligible) on the following screens. Click **Review and launch**:
    ![/images/war-cost/2cost-cloudwatch-agent.png](/images/war-cost/cost-cloudwatch-agent2.png)

1. Look for the created IAM role *CloudWatchAgentServerRole* under the **IAM role** box, select it and apply.
    ![Images/MemInstall04.png](/cost/200_aws_resource_optimization/Images/MemInstall04.png)

1. Confirm that the *CloudWatchAgentServerRole* was sucessfully attached to your **EC2 instance**
    ![Images/MemInstall05.png](/cost/200_aws_resource_optimization/Images/MemInstall05.png)

1. Validade if the IAM role *CloudWatchAgentServerRole* is attached to the desired instance
    ![/images/war-cost/cost-cloudwatch-agent.png](/images/war-cost/cost-cloudwatch-agent-check.png)

