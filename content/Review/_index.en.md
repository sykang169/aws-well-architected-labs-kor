---
title: "Review Again(Machanism)"
weight: 80
pre: "<b>8. </b>"
---

So far, we've applied the best practices provided by 5 pillars on the 3-tier web.
Now, let's look at the things that have changed from the first review.

#### First Environment
![AWS-Code-Cycle](/images/war/awswellarchitected.svg)

#### Best Practices Applied
If you have performed HoL for each pillar, you can apply the following best practices to your existing environment.

| pillar| name | description|
|:---|:---|:---|
|Performance Efficiency| **Monitoring** with **CloudWatch** | Use CloudWatch's dashboard to measure and monitor your current EC2 usage. |
|Performance Efficiency| **Alarm** with **CloudWatch** | When the CPU usage monitored by CloudWatch rises above a certain level, an alarm is sent to the user via e-mail.| 
|Cost Optimization| **Right Sizeing** of **EC2** | Activate Cost Explorer's Recommendation to find the appropriate size of the EC2 you are using. Recommend and change the appropriate EC2 for your usage.|
|Cost Optimization| **Right Sizing** accuracy improvement through memory metric collection of **CloudWatch Agent**  | You can improve the accuracy of right sizing by collecting additional memory metrics.|
|Operational Excellence| Resource Central Management with **System Manager** | Collects, monitors, and manages information on EC2 instances created through System Mangager's inventory. | 
|Operational Excellence| Patch management using **System Manager** | Easily apply and automate security-related and updates to instances through System Manager's patch manager. | 
|Reliability| Workload reliability testing with **Chaos testing** | Through a script that stops EC2, RDS, and AZ, it verifies the resilience of the workload in the event of a corresponding failure and evaluates how the system responds to various failure scenarios. | 

#### Environment after the first Well-Architected Framework Review
![AWS-Code-Cycle](/images/war/awswellarchitected-after2.svg)


Now, in line with the best practices we've applied, we'll go back to the workload review of Well-Architected tools.