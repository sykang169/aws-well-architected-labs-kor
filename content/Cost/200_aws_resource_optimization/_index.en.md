---
title: "EC2 Right Sizing(MEM)"
#menutitle: "Lab #3"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 7
pre : "<b>4-2. </b>"
---
## Authors
- Jeff Kassel, AWS Technical Account Manager
- Arthur Basbaum, AWS Cloud Economics
- +Seyong Kang, Solutions Architect

## Feedback
If you wish to provide feedback on this lab, there is an error, or you want to make a suggestion, please email: costoptimization@amazon.com

## Introduction
 This hands-on lab will guide you through the steps to install the CloudWatch agent to collect memory utilization (% GB consumption) and analyze how that new datapoint can help during EC2 right sizing exercises with the AWS Resource Optimization tool.

## Goals
- Learn how to check metrics like CPU, Network and Disk usage on Amazon CloudWatch
- Learn how to install and collect Memory data through a custom metric at Amazon CloudWatch
- Enable AWS Resource Optimization and observe how the recommendations are impacted by this new datapoint (Memory)

## Prerequisites
- Root user access to the management account
- Enable AWS Resource Optimization at *AWS Cost Explorer > Recommendations* no additional cost.

## Permissions required
- Root user access to the management account
- NOTE: There may be permission error messages during the lab, as the console may require additional privileges. These errors will not impact the lab, and we follow security best practices by implementing the minimum set of privileges required.

## Steps:
{{% children  /%}}
