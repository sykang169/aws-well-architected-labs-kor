---
title: "Operational Excellence"
## menutitle: "Lab #1"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 50
hidden: false
pre: "<b>5. </b>"
---

## Author
* Mahanth Jayadeva, Solutions Architect, Well-Architected
* +Seyong Knag, Solutions Architect
* ++Jimin kim, Solutions Architect

{{% notice note %}}
For more information about Operational Excellence on AWS visit the Well-Architected tool in the AWS console, and read the AWS [Well-Architected Operational Excellence](https://d1.awsstatic.com/whitepapers/architecture/AWS-Operational-Excellence-Pillar.pdf) whitepaper.
{{% /notice%}}

### What is Operational Excellence?
The Operational Excellence pillar includes the ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.

### Design Principles for Operational Excellence
#### Perform operations as code
In the cloud, you can apply the same engineering discipline that you use for application code to your entire environment. You can define your entire workload (applications, infrastructure) as code and update it with code. You can implement your operations procedures as code and automate their execution by triggering them in response to events. By performing operations as code, you limit human error and enable consistent responses to events.


#### Make frequent, small, reversible changes
Design workloads to allow components to be updated regularly. Make changes in small increments that can be reversed if they fail (without affecting customers when possible).

#### Refine operations procedures frequently
As you use operations procedures, look for opportunities to improve them. As you evolve your workload, evolve your procedures appropriately. Set up regular game days to review and validate that all procedures are effective and that teams are familiar with them.

#### Anticipate failure
Perform “pre-mortem” exercises to identify potential sources of failure so that they can be removed or mitigated. Test your failure scenarios and validate your understanding of their impact. Test your response procedures to ensure that they are effective, and that teams are familiar with their execution. Set up regular game days to test workloads and team responses to simulated events.

#### Learn from all operational failures
Drive improvement through lessons learned from all operational events and failures. Share what is learned across teams and through the entire organization.

Steps:
{{% children %}}