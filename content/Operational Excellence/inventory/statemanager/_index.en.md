---
title: "State Manager"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 522
---

## Systems Manager: State Manager
<!--
AWS Systems Manager는 Amazon EC2 또는 온프레미스 인스턴스의 구성을 일관되게 유지하는 데 도움이 되는 구성 관리 기능을 제공합니다. Systems Manager에서는 서버 구성, 안티바이러스 정의, 방화벽 설정 등과 같은 구성 세부 정보를 제어할 수 있습니다. AWS Management Console을 통해 서버의 구성 정책을 정의하거나, GitHub 또는 Amazon S3 버킷에서 직접 기존 스크립트, PowerShell 모듈 또는 Ansible 플레이북을 사용할 수 있습니다. Systems Manager는 정의한 시간과 빈도에 따라 인스턴스 전체에 구성을 자동으로 적용합니다. 언제든 Systems Manager를 쿼리하여 인스턴스 구성 상태를 볼 수 있으므로, 규정 준수 상태에 대한 온디맨드 가시성이 제공됩니다.
!-->

### Association
In State Manager, an [association](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-associations.html) is the result of binding configuration information that defines the state you want your instances to be in to the instances themselves. This information specifies when and how you want instance-related operations to run that ensure your Amazon EC2 and hybrid infrastructure is in an intended or consistent state.



<!--
* 또한 연결(Association)은 구성 적용 시 취할 조치도 지정합니다. 
  * 예를 들어, 안티바이러스 소프트웨어에 대한 연결은 하루에 한 번 실행할 수 있습니다. 이러한 소프트웨어가 설치되어 있지 않으면 상태 관리자가 해당 소프트웨어를 설치합니다. 소프트웨어가 설치되어 있으나 서비스가 실행 중이 아닌 경우 연결이 State Manager에 해당 서비스의 시작을 지시할 수 있습니다.
* Association은 대상 세트에 적용 할 상태를 정의합니다. 연결에는 세 가지 구성 요소와 하나의 선택적 구성 요소 집합이 포함됩니다.
  * 상태 정의 문서
  * 타겟(들)
  * 스케줄
  * (선택사항) 런타임 매개변수 등
!-->

#### In fact, we already made a link in the previous chapter, Inventory.

<!--
### 연결의 상태(Status) 확인

1. Systems Manager로 이동하여 **State Manager**를 선택하고 **Actions**을 확인합니다. 앞 단계에서 생성한 **Inventory-Association**의 **Status**는 아직 **Pending**일 수 있습니다. 
   ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-review-start.png)
   1. **Setup Inventory**에서 만든 **Association id**를 선택합니다. 만약 별도의 이름을 설정하지 않았다면 **Association name**은 `Inventory-Association`가 기본 이름으로 설정되었을 것입니다.
   1. **Association ID** 하단에서 사용 가능한 각 데이터 탭을 검사하십시오.
   ![/images/operation/ssm-inventory-detail.png](/images/operation/ssm-review-detail.png)
   1. **Edit**를 선택하세요.
   ![/images/operation/ssm-inventory-edit.png](/images/operation/ssm-review-edit.png)
   1. **Name - optional** 에 좀 더 식별하기 쉬운 이름을 넣어봅시다, 예를들면  `InventoryAllInstances` (공백은 넣을 수 없습니다 ).
   ![/images/operation/ssm-inventory-name.png](/images/operation/ssm-review-name.png)
   1. 하단의 **Save Change**를 클릭합니다.
_Inventory_ 다음과 같이 완성됩니다. :
   * AWS-GatherSoftwareInventory command document에 정의 된 활동.
   * **Parameters** section에 제공된 parameters는 실행 시 document로 전달됩니다.
   * targets은 **Targets** section에서 정의됩니다
   >**중요**<br> 예제에선 single target 와일드 카드가 있습니다. 와일드 카드는 모든 인스턴스를 일치시켜 _all_ targets을 만듭니다.
   * 이 활동의 스케줄은 30 분 간격으로 CRON/Rate 표현식을 사용하기 위해 **Specify schedule** 및 **Specify with**에 정의되어 있습니다.
   * **Output options**을 지정하는 옵션이 있습니다.
   >**Note**<br> command document를 변경하면**Parameters** section이 new command document에 적합하도록 변경됩니다. 
!--> 

1. Navigate to **Managed Instances** under **Instances and Nodes** in the navigation bar. An **Association Status** has been established for the inventoried instances under management.
   ![/images/operation/ssm-inventory-as.png](/images/operation/ssm-review-as.png)
2. Choose one of the **Instance ID** links to go to the inventory of the instance. 
   ![/images/operation/ssm-inventory-inventory.png](/images/operation/ssm-review-inventory.png)
3.  The Inventory tab is now populated and you can track associations and their last activity under the Associations tab.
   ![/images/operation/ssm-inventory-associate.png](/images/operation/ssm-review-associate.png)

1.  Navigate to **Compliance** under **Instances & Nodes** in the navigation bar. Here you can view the overall compliance status of your managed instances in the **Compliance Summary** and the individual compliance status of systems in the **Corresponding managed instances** section below.
   ![/images/operation/ssm-inventory-compilence2.png](/images/operation/ssm-review-compilence2.png)

<!--
>**Note**<br>inventory activity를 완료하는데 최대 10 분이 소요될 수 있습니다. inventory activity이 완료되기를 기다리는 동안 다음 섹션으로 진행할 수 있습니다.
!-->

## Systems Manager: Compliance

You can use AWS Systems Manager Configuration [Compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-compliance.html) to scan your fleet of managed instances for patch compliance and configuration inconsistencies. You can collect and aggregate data from multiple AWS accounts and Regions, and then drill down into specific resources that aren’t compliant.

By default, Configuration Compliance displays compliance data about Systems Manager Patch Manager patching and **Systems Manager State Manager** associations. You can also customize the service and create your own compliance types based on your IT or business requirements. You can also port data to **Amazon Athena** and **Amazon QuickSight** to generate fleet-wide reports.

