---
title: "패치 관리자"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>1. </b>"
weight: 531
---

## Systems Manager: Patch Manager

AWS Systems Manager [Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html) automates the process of patching managed instances with security related updates.

<!--
>**Note**<br> Linux 기반 인스턴스의 경우 non-security 업데이트 패치를 설치할 수 있습니다.
!-->

<!--운영체제 유형별로 Amazon EC2인스턴스 또는 온프레미스 서버 및 가상머신(VM)을 패치할 수 있습니다. 지원되는 버전은 Windows, Ubuntu Server, RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Amazon Linux가 포함됩니다. 
!-->


> **Warnings**
>  * The [operating systems supported by Patch Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) may vary from those supported by the SSM Agent.
>  * **AWS does not test patches for Windows or Linux before making them available in Patch Manager** .
>  * **If any updates are installed by Patch Manager the patched instance is rebooted**.
>  * **Always test patches thoroughly before deploying to production environments**.


## Patch Baselines

Patch Manager uses **patch baselines**, which include rules for auto-approving patches within days of their release, as well as a list of approved and rejected patches. Later in this lab we will schedule patching to occur on a regular basis using a Systems Manager **Maintenance Window** task. Patch Manager integrates with AWS Identity and Access Management (IAM), AWS CloudTrail, and Amazon CloudWatch Events to provide a secure patching experience that includes event notifications and the ability to audit usage.

<!-- 
이 실습의 뒷부분에서 Systems Manager 유지 관리 기간 작업을 사용하여 정기적으로 패치를 적용하도록 예약합니다. Patch Manager는 AWS Identity and Access Management (IAM), AWS CloudTrail 및 Amazon CloudWatch Events와 통합되어 이벤트 알림 및 사용 감사 기능을 포함하는 안전한 패치 경험을 제공합니다.
!-->

<!--
패치 관리자는 **패치 기준**을 사용합니다. 패치 기준은 인스턴스에 대한 설치가 승인되는 패치를 정의합니다. 패치 승인 또는 거부는 하나씩 지정할 수 있습니다. 또한 자동 승인 규칙을 생성하여 특정 유형의 업데이트(예: 필수 업데이트)가 자동 승인되도록 지정할 수도 있습니다. 거부된 목록은 규칙 및 승인 목록을 모두 재정의합니다.

승인된 패치 목록을 사용하여 특정 패키지를 설치하려면 먼저 모든 자동 승인 규칙을 제거하십시오. 임의 패치를 명시적으로 거부로 구분하면 해당 패치는 자동 승인 규칙의 모든 기준을 만족하더라도 승인 또는 설치되지 않습니다. 또한 패치가 해당 인스턴스에 대해 승인되었더라도 인스턴스의 소프트웨어에 적용되는 경우에만 패치가 인스턴스에 설치됩니다.

패치 관리자는 패치 관리자에서 지원하는 운영 체제마다 사전 정의된 패치 기준을 제공합니다. 이러한 기준은 현재 구성된 대로 사용하거나(사용자 지정할 수 없음) 고유한 사용자 지정 패치 기준을 생성할 수 있습니다. 사용자 지정 패치 기준을 사용하면 환경에 대해 승인 또는 거부되는 패치를 더욱 효과적으로 제어할 수 있습니다. 또한 미리 정의된 기준은 해당 기준을 사용하여 설치된 모든 패치에 Unspecified의 규정 준수 수준을 할당합니다. 규정 준수 값을 할당하려면 미리 정의된 기준의 복사본을 생성하고 패치에 할당할 규정 준수 값을 지정할 수 있습니다. 자세한 내용은 사용자 지정 기준 정보 및 사용자 지정 패치 기준 생성 단원을 참조하십시오.
--> 


### 5.1 Create a Patch Baseline

1. Under **Instances and Nodes** in the **AWS Systems Manager** navigation bar, choose **Patch Manager**.
1. Click the **View predefined patch baselines** link under the **Configure patching** button on the upper right.
   ![/images/operation/ssm-patch-start.png](/images/operation/ssm-patch-start.png)
1. Choose **Create patch baseline**.
   ![/images/operation/ssm-patch-baseline.png](/images/operation/ssm-patch-baseline.png)
1. On the **Create patch baseline** page in the **Provide patch baseline details** section:
   1. Enter a **Name** for your custom patch baseline, such as `AmazonLinuxSecAndNonSecBaseline`.
   1. Optionally enter a description, such as `Amazon Linux patch baseline including security and non-security patches`.
   1. Select **Amazon Linux2** to **Operation system**.
   ![/images/operation/ssm-patch-detail.png](/images/operation/ssm-patch-detail.png)
1. In the **Approval rules** section:
   1. Examine the options in the lists and ensure that **Product**, **Classification**, and **Severity** have values of **All**.
   1. Leave the **Auto approval delay** at its default of **0 days**.
   1. Change the value of **Compliance reporting - optional** to **Critical**.
   ![/images/operation/ssm-patch-rule1.png](/images/operation/ssm-patch-rule1.png)
   1. Choose **Add another rule**.
   1. In the new rule, change the value of **Compliance reporting - optional** to **Medium**.
   1. Check the box under **Include non-security updates** to include all Amazon Linux updates when patching.
   ![/images/operation/ssm-patch-rule2.png](/images/operation/ssm-patch-rule2.png)


1. In the **Patch exceptions** section in the **Rejected patches - optional** text box, enter `system-release.*` This will [reject patches](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-approved-rejected-package-name-formats.html) to new Amazon Linux releases that may advance you beyond the [Patch Manager supported operating systems](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) prior to your testing new releases.
1. For Linux operating systems, you can optionally define an [alternative patch source repository](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-how-it-works-alt-source-repository.html). Choose the **X** in the **Patch sources** area to remove the empty patch source definition.
Choose **Create patch baseline** and you will go to the **Patch Baselines** page where the AWS provided default patch baselines, and your custom baseline, are displayed.
![/images/operation/ssm-patch-exception.png](/images/operation/ssm-patch-exception.png)
1. Click **Create patch baseline** button and finish.
   If an approved patch is reported as missing, the option you choose in **Compliance reporting**, such as `Critical` or `Medium`, determines the severity of the compliance violation reported in System Manager **Compliance**.

## Patch Groups

A [patch group](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-patchgroups.html) is an optional method to organize instances for patching. For example, you can create patch groups for different operating systems (Linux or Windows), different environments (Development, Test, and Production), or different server functions (web servers, file servers, databases). Patch groups can help you avoid deploying patches to the wrong set of instances. They can also help you avoid deploying patches before they have been adequately tested.

You create a patch group by using Amazon EC2 tags. Unlike other tagging scenarios across Systems Manager, a patch group must be defined with the tag key: `Patch Group` (tag keys are case sensitive). You can specify any value (for example, `web servers`) but the key must be `Patch Group`.

>**Note**<br>An instance can only be in one patch group.

After you create a patch group and tag instances, you can register the patch group with a patch baseline. By registering the patch group with a patch baseline, you ensure that the correct patches are installed during the patching execution. When the system applies a patch baseline to an instance, the service checks if a patch group is defined for the instance.
* If the instance is assigned to a patch group, the system checks to see which patch baseline is registered to that group.
* If a patch baseline is found for that group, the system applies that patch baseline.
* If an instance isn't assigned to a patch group, the system automatically uses the currently configured default patch baseline.


#### Assign a Patch Group

1. Choose the **Baseline ID** of your newly created baseline to enter the details screen.(If you don't see the Baseline ID, turn the page. The baseline name created in this lab is `AmazonLinuxSecAndNonSecBaseline`.)
![/images/operation/ssm-patch-pg.png](/images/operation/ssm-patch-pg.png)
1. Choose **Actions** in the top right of the window and select **Modify patch groups**.
![/images/operation/ssm-patch-pg-set.png](/images/operation/ssm-patch-pg-set.png)
1. In the **Modify patch groups** window under **Patch groups**, enter `Critical`, choose **Add**, and then choose **Close** to be returned to the **Patch Baseline** details screen.
![/images/operation/ssm-patch-pg-critical.png](/images/operation/ssm-patch-pg-critical.png)
1. Click **Close**, and back to **Patch Baseline** page for check detail information.
![/images/operation/ssm-patch-fin.png](/images/operation/ssm-patch-fin.png)

> **Note**
> * If an instance is assigned to a **patch group**, the system checks **based on the patch registered in that group**.
> * If there is a patch criterion for that group, the system applies that patch criterion. Except for Bastion Host, the two instances belong to a patch group called **Critical**, so they follow the **patch criteria** you just created.
> *If an instance is **not** assigned to a patch group, the system will **automatically** use the **default patch baseline** currently configured.
