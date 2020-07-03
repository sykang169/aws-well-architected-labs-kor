---
title: "Setup"
weight: 20
pre: "<b>2. </b>"
---

{{% notice note %}}
The CloudFormation`s stack created in the next chapter includes all infrastructure and the CI/CD pipeline of master and develop.
{{% /notice%}}

This lab include how to improve your code quality using AWS services. developers can commit, test, and deploy code with minimal effort. The deployment and testing environment is automated.

#### infrastructure
![AWS-Code-Cycle](/images/aws.svg)

#### Service
![AWS-Code-Cycle](/images/awsservice.svg)


| Name | contents|
|:---|:---|
| **CodeCommit** | this is code repository, the development code is **JAVA** and Gradle. |
| **CodeBuild** | The build tool is **CodeBuild**. It using Junit for UnitTest and the result is report to xml. The printed report can be viewed directly from the console using CodeCommit's report group. |
| **CodeDeploy** | Tested code is automatically deployed to the Dev environment. The code pushed to the Develop Branch is deploy to the DevWebApp01 instance and starts profiling by CodeGuru's profiler. And when all tests pass and merge into Master, the code is automatically deployed as ProdWebApp01.| 
| **CodePipeline** | Visualize the series of steps above as **CodePipeline**. Developers can immediately find out where the pushed code has a problem. |
| **CodeGuru** | When Pull-Request, Code-Review is automatically performed. Profiling of the code deployed on DevWebapp01, ProdWebapp01. |


-[let`s set up the lab environment using CloudFomration.](/en/setup/lab-setup) 
