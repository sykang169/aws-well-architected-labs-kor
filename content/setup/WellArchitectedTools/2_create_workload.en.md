---
title: "Creating a workload"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---




1. Log-in AWS console, typing `Well-Architected Tools` in service search bar. 
    you can go to this link : [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).

    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT0.png)

    Well-Architected Reviews are conducted per [workload](https://wa.aws.amazon.com/wat.concept.workload.en.html). A workload identifies a set of components that deliver business value. The workload is usually the level of detail that business and technology leaders communicate about.

1. Click the **Define Workload** button on the landing page:
    ![ClickWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT1.png)

1. If you have already created a workload, a list of workloads will appear. Similarly, on this screen, click the **Define Workload** button.
    ![ClickWorkload2](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT2.png)

1. On the Define Workload interface, enter the necessary information:
    - Name: `Workload for AWS Workshop`  
    - Description: `wellarchitectedlabs workshop`  
    - Environment: Select **Pre-production**  
    - Review owner: workload owner`s email addres or alias.
    - Account ID: \<AWS ACCOUNT_NUMBER\>
    - Regions: Select AWS Regions, example:**(Seoul)/ap-northeast-2**  
    ![EnterWorkloadDetails](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload.png)
  
    - Industry Type: `InfoTech`(option) 
    - Industry: `Internet`(option)  
    ![DefineWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload2.png)
    All clear, Click **Next** button:

1. in **Apply lenses** tab, Click checkbox **AWS Well-Architected Framework**. **AWS Well-Architected Framework** The AWS Well-Architected Tool helps you review the state of your workloads and compares them to the latest AWS architectural best practices.   You can also choose a other Lense for your workload which specific workload.:
    ![DefineWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload3.png)
    Click **Define workload** and finished.
