---
title: "Preparation for Failure Injection"
menutitle: "Preparation for Failure Injection"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>1. </b>"
weight: 1
---

**Failure injection** (also known as **chaos testing**) is an effective and essential method to validate and understand the resiliency of your workload and is a recommended practice of the [AWS Well-Architected Reliability Pillar](https://aws.amazon.com/architecture/well-architected/). Here you will initiate various failure scenarios and assess how your system reacts.

### Preparation

Before testing, please prepare the following:

1. Get VPC ID
      * A VPC (Amazon Virtual Private Cloud) is a logically isolated section of the AWS Cloud where you have deployed the resources for your service
      * For these tests you will need to know the **VPC ID** of the VPC you created as part of deploying the service
      * Navigate to the VPC management console: <https://console.aws.amazon.com/vpc>
      * In the left pane, click **Your VPCs**
            * 1 - Tick the checkbox next to **WellArchitectedLabsStack/VPC**
            * 2 - Copy the **VPC ID**

      ![setvpc](/images/reliability/reliability-vpc.png)      

     * Save the VPC ID - you will use later whenever `<vpc-id>` is indicated in a command

1. Let`s move the script that will be used for **fault injection** to Cloud9. Download the file below.         
      * [fail_az.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/fail_az.sh)
      * [fail_instance.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/fail_instance.sh)
      * [failover_rds.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/failover_rds.sh)

1. Start Cloud9([Open AWS Cloud9 Console로](https://ap-northeast-2.console.aws.amazon.com/cloud9/home?region=ap-northeast-2#)). Select `WellArchitectedWorkshop's Cloud9` in console.
      ![](/images/reliability/reliability-cloud9-start.png)      
1. Upload download file to Cloud9. top menu, select **File** -> **Upload Local Files**..., choose files for upload..
      ![](/images/reliability/reliability-cloud9-upload.png)      



1. When the upload is complete, you can check the uploaded file in Cloud9.

      ![](/images/reliability/reliability-cloud9-fin.png)      

1. Grant execute permission to the file. Enter the following into CLoud9's terminal.

      ```bash
      sudo chmod 755 ./fail_instance.sh
      sudo chmod 755 ./fail_az.sh
      sudo chmod 755 ./failover_rds.sh
      ```
1. Make sure that `jq` is installed in Cloud9 (requires version 1.4 or higher).

      ```bash
      $ jq --version
      jq-1.5-1-a5b5cbe
      ```

1. If it is not installed, enter the following into CLoud9's terminal.

      ```bash
      sudo yum install jq -y
      ```

1. If you type jq --version again as above, you are ready.

    | |
    |:---:|
    |**Availability Zones** (**AZ**s) are isolated sets of resources within a region, each with redundant power, networking, and connectivity, housed in separate facilities. Each Availability Zone is isolated, but the Availability Zones in a Region are connected through low-latency links. AWS provides you with the flexibility to place instances and store data across multiple Availability Zones within each AWS Region for high resiliency.|
    |*__Learn more__: After the lab [see this whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/global-infrastructure.html) on regions and availability zones*|
