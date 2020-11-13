---
title: "Patch Management"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 53
pre: "<b>5-3. </b>"
---

In the cloud, you can apply the same engineering principles you use for application code across your entire environment. The entire workload (application, infrastructure, etc.) can be defined in code and updated with code. You can script and automate execution of task procedures by triggering task procedures in response to events. Performing work in code reduces human error and helps ensure consistent execution of work activities.

Systems Manager features related to this lab.

#### Patch Manager
AWS Systems Manager Patch Manager automates the process of patching managed instances with both security related and other types of updates. You can use Patch Manager to apply patches for both operating systems and applications. (On Windows Server, application support is limited to updates for Microsoft applications.) You can use Patch Manager to install Service Packs on Windows instances and perform minor version upgrades on Linux instances. You can patch fleets of EC2 instances or your on-premises servers and virtual machines (VMs) by operating system type. This includes supported versions of Windows Server, Amazon Linux, Amazon Linux 2, CentOS, Debian Server, Oracle Linux, Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES), and Ubuntu Server. You can scan instances to see only a report of missing patches, or you can scan and automatically install all missing patches.

#### Run Command
AWS Systems Manager Run Command lets you remotely and securely manage the configuration of your managed instances. A managed instance is any EC2 instance or on-premises machine in your hybrid environment that has been configured for Systems Manager. Run Command enables you to automate common administrative tasks and perform ad hoc configuration changes at scale. You can use Run Command from the AWS console, the AWS Command Line Interface, AWS Tools for Windows PowerShell, or the AWS SDKs. Run Command is offered at no additional cost.

In this lab, you apply the concepts of _Infrastructure as Code_ and _Operations of Code_ to the following activities.

Steps:
{{% children  %}}
