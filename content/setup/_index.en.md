---
title: "Setup"
weight: 21
pre: "<b>2. </b>"
---

{{% notice note %}}
This CloudFormation stack includes all the environments for each pillar`s labs.
{{% /notice%}}
 

#### Enviroment
![AWS-Code-Cycle](/images/war/awswellarchitected.svg)

#### Services in use
![AWS-Code-Cycle](/images/war/awsservice.svg)


| Name | Description|
|:---|:---|
| **Amazon EC2** | Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. Amazon EC2’s simple web service interface allows you to obtain and configure capacity with minimal friction. It provides you with complete control of your computing resources and lets you run on Amazon’s proven computing environment. |
| **Application Load Balancer** | A load balancer serves as the single point of contact for clients. The load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. This increases the availability of your application. You add one or more listeners to your load balancer.|
| **Amazon RDS** | Amazon Relational Database Service (Amazon RDS) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient and resizable capacity while automating time-consuming administration tasks such as hardware provisioning, database setup, patching and backups. It helps you to focus on your applications so you can give them the fast performance, high availability, security and compatibility they need. | 
| **AWS Auto Scaling** | AWS Auto Scaling monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost. Using AWS Auto Scaling, it’s easy to setup application scaling for multiple resources across multiple services in minutes. The service provides a simple, powerful user interface that lets you build scaling plans for resources including Amazon EC2 instances and Spot Fleets, Amazon ECS tasks, Amazon DynamoDB tables and indexes, and Amazon Aurora Replicas. AWS Auto Scaling makes scaling simple with recommendations that allow you to optimize performance, costs, or balance between them. If you’re already using Amazon EC2 Auto Scaling to dynamically scale your Amazon EC2 instances, you can now combine it with AWS Auto Scaling to scale additional resources for other AWS services. With AWS Auto Scaling, your applications always have the right resources at the right time.| 

-[Let's deploy Cloud9 & CloudFomration stack.](/en/setup/cloud9) 
