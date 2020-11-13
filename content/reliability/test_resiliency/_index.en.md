---
title: "Testing for Resiliency of EC2, RDS, and AZ"
menutitle: "Test Resiliency EC2, RDS, & AZ"
description: "Use code to inject faults simulating EC2, RDS, and Availability Zone failures. These are used as part of Chaos Engineering to test workload resiliency"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 1
tags:
  - test_resiliency
---

{{< rawhtml >}}
<center>
<video width="600" height="450" controls>
  <source src="https://d3h9zoi3eqyz7s.cloudfront.net/Reliability/Videos/chaos1.mp4" type="video/mp4">
</video>
</center>
{{< /rawhtml >}}

## Authors

* Rodney Lester, Senior Solutions Architect Manager, AWS Well-Architected
* Adrian Hornsby, Principal Tech Evangelist, AWS
* Seth Eliot, Principal Reliability Solutions Architect, AWS Well-Architected
* Seyong Kang, Solutions Architect

## Introduction

The purpose if this lab is to teach you the fundamentals of using tests to ensure your implementation is resilient to failure by injecting failure modes into your application. This may be a familiar concept to companies that practice Failure Mode Engineering Analysis (FMEA). It is also a key component of Chaos Engineering, which uses such failure injection to test hypotheses about workload resiliency. One primary capability that AWS provides is the ability to test your systems at a production scale, under load.

It is not sufficient to only design for failure, you must also test to ensure that you understand how the failure will cause your systems to behave. The act of conducting these tests will also give you the ability to create playbooks how to investigate failures. You will also be able to create playbooks for identifying root causes. If you conduct these tests regularly, then you will identify changes to your application that are not resilient to failure and also create the skills to react to unexpected failures in a calm and predictable manner.

In this lab, you will deploy a 3-tier resource, with a reverse proxy (Application Load Balancer), Web Application on Amazon Elastic Compute Cloud (EC2), and MySQL database using Amazon Relational Database Service (RDS). There is also an option to deploy the same stack into a different region, which provides you the ability to progress from simpler component failure testing to failure testing under a simulated AWS regional failure.

The skills you learn will help you build resilient workloads in alignment with the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

## Goals:

* Reduce fear of implementing resiliency testing by providing examples in common development and scripting languages
* Resilience testing of EC2 instances
* Resilience testing of RDS Multi-AZ instances
* Resilience testing using Availability Zones failures
* Resilience testing of S3 objects
* Learn how to implement resiliency using those tests
* Learn how to think about what a failure will cause within your infrastructure
* Learn how common AWS services can reduce mean time to recovery (MTTR)


## Steps:
{{% children /%}}

