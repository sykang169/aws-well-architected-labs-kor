---
title: "Inventory"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>1. </b>"
weight: 521
---

## Systems Manager: Inventory
You can use [AWS Systems Manager Inventory](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html) to collect operating system (OS), application, and instance metadata from your Amazon EC2 instances and your on-premises servers or virtual machines (VMs) in your hybrid environment. You can query the metadata to quickly understand which instances are running the software and configurations required by your software policy, and which instances need to be updated.

<!--
[AWS Systems Manager 인벤토리](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html)는 Amazon EC2 및 온프레미스 컴퓨팅 환경에 대한 가시성을 제공합니다. 인벤토리를 사용하여 관리형 인스턴스에서 메타데이터를 수집할 수 있습니다. 이 메타데이터를 중앙 Amazon Simple Storage Service(Amazon S3) 버킷에 저장한 후 기본 제공 도구를 사용하여 데이터를 쿼리하고 어느 인스턴스에서 소프트웨어 정책이 요구하는 소프트웨어 및 구성을 실행 중인지, 어느 인스턴스를 업데이트해야 하는지 빠르게 확인할 수 있습니다. 원클릭 절차를 사용하여 모든 관리형 인스턴스에 대해 인벤토리를 구성할 수 있습니다. 또한 여러 AWS 리전 및 계정으로부터 인벤토리 데이터를 구성하고 볼 수 있습니다.
-->


####  Using Systems Manager Inventory to Track Your Instances
   1. Under **Instances & Nodes** in the AWS Systems Manager navigation bar, choose **Inventory**.
   ![/images/operation/ssm-inventory.png](/images/operation/ssm-inventory.png)
   1. Scroll down in the window to the **Corresponding managed instances** section. Inventory currently contains only the instance data available from the EC2 <!--현재 인벤토리에는 EC2에서 사용 가능한 인스턴스 데이터만 포함되어 있습니다.-->
   2. Choose the **InstanceID** of one of your systems.
      ![/images/operation/ssm-inventory-click.png](/images/operation/ssm-inventory-click.png)
   3. Examine each of the available tabs of data under the **Instance ID** heading.The Inventory tab will be empty as it is not yet set up for inventory.
   ![/images/operation/ssm-inventory-menu.png](/images/operation/ssm-inventory-menu.png)

#### Inventory collection must be specifically configured and the data types to be collected must be specified. 
**Limiting inventory collection targets based on resource tags**
{{% notice tip %}}
You can also select all managed instances in your account to get your inventory, but you can also choose inventory instances based on specific tags, such as Environment or Workload, depending on your needs. Of course, you can also manually select specific instances.
{{% /notice%}}
   1. Choose **Inventory** in the navigation bar.
   2. Choose **Setup Inventory** in the top right corner of the window
   ![/images/operation/ssm-inventory-setup.png](/images/operation/ssm-inventory-setup.png)
1. In the **Setup Inventory** screen, define targets for inventory:
   1. Under **Specify targets by**, select **Specifying a tag**
   1. Under **Tags** specify `Environment` for the key and `MasterAccount` for the value
   ![/images/operation/ssm-inventory-targets.png](/images/operation/ssm-inventory-targets.png)

**Schedule the frequency with which inventory is collected**

1. type `InventoryAllInstances` in **Name** of inventory.
2. For **Collect inventory data every**, accept the default **30** Minute(s)
   ![/images/operation/ssm-inventory-schedule.png](/images/operation/ssm-inventory-schedule.png)
3. Under **parameters**, specify what information to collect with the inventory process
   - Please refer to the [link](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html) to learn more about each parameter.
     ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-inventory-finish.png)
<!--
1. (선택사항) 필요한 경우 인벤토리 실행 로그를 지정한 S3 버킷에 수집할 수도 있습니다. (사전에 [로그를 저장할 버킷](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html)이 생성되어 있어야 합니다):
   1. **Advanced**의 **Sync inventory execution logs to an S3 bucket**의 체크박스를 선택하세요.
   2. S3 버킷 이름을 지정합니다.
   3. (선택사항) S3 버킷의 접두어를 지정할 수 있습니다.
2. !-->
3. Not check **Sync inventory execution logs to an S3 bucket**. 
   ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-inventory-advanced.png)
4. reviewing the settings, click **Setup Inventory** at the bottom right. It can take up to 10 minutes to deploy the new inventory policy to your instances.

<!--
1. 새로운 정책을 만드려면 동일 방법으로 추가할 수 있습니다.
2. 기존의 정책을 변경하려면 왼쪽 메뉴의 **State Manager**을 클릭하고 변경할 정책의 **Associations**를 클릭한다음 **Edit**을 선택하세요.
!-->

{{% notice note %}}
Several Inventory specifications can also be created. These are stored as **Associations** within the Systems Manager State Manager. We will learn more in the next chapter.
{{% /notice%}}

<!--
## Systems Manager: State Manager
 
State Manager에서 [Association](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-associations.html)은 관리형 인스턴스에 할당되는 구성입니다. 이러한 구성은 인스턴스에서 관리하려는 상태를 정의합니다. 예를 들어, 연결은 인스턴스에서 안티바이러스 소프트웨어가 설치되어 실행 중이어야 하는지 또는 특정 포트가 닫혀 있어야 하는지를 지정할 수 있습니다. 연결은 구성이 다시 적용되는 시점에 대한 일정을 지정합니다. 또한 연결은 구성 적용 시 취할 조치도 지정합니다. 예를 들어, 안티바이러스 소프트웨어에 대한 연결은 하루에 한 번 실행할 수 있습니다. 이러한 소프트웨어가 설치되어 있지 않으면 State Manager가 해당 소프트웨어를 설치합니다. 소프트웨어가 설치되어 있으나 서비스가 실행 중이 아닌 경우 연결이 State Manager에 해당 서비스의 시작을 지시할 수 있습니다.


Association은 대상 세트에 적용 할 상태를 정의합니다. 연결에는 세 가지 구성 요소와 하나의 선택적 구성 요소 집합이 포함됩니다.
  * 상태 정의 문서
  * 타겟(s)
  * 스케쥴
  * (선택사항) 런타임 매개변수.

이전 과정을 잘 수행했다면 이미 **Setup Inventory** 작업을 수행 할 때 상태 관리자에서 연결을 만들었습니다.

### 3 Association Status 리뷰

1.  **State Manager**를 선택하고 **Actions**을 확인하세요. 지금, 방금 만든 inventory-Association의 **Status**는 아마 완료되지 않았을 것입니다.
   ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-review-start.png)
   1. **Setup Inventory**에서 만든 *Association id*를 선택하세요. 만약 별도의 이름을 설정하지 않았다면 **Association name**은 `Inventory-Association`가 기본 이름으로 설정되었을 것입니다.
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
 

1. 메뉴의**Instances and Nodes**의  **Managed Instances**를 클릭합니다. 관리중인 인벤토리 instances에 대한 **Association Status**가 설정된 것을 확인할 수 있습니다.
   ![/images/operation/ssm-inventory-as.png](/images/operation/ssm-review-as.png)
1. **Instance ID** 중 하나를 선택하여 인스턴스 인벤토리로 이동하십시오. 이제 인벤토리 탭이 채워진 것을 확인할 수 있습니다.
   ![/images/operation/ssm-inventory-inventory.png](/images/operation/ssm-review-inventory.png)
1.  Associations 탭에서 associations 및 마지막 활동을 추적 할 수 있습니다.
   ![/images/operation/ssm-inventory-associate.png](/images/operation/ssm-review-associate.png)

1. **Instances & Nodes**의 **Compliance**로 이동합니다. **Compliance Summary** 섹션에서는 관리되는 인스턴스의 전체 준수 상태와 **Compliance Summary**를 볼 수 있습니다.
   ![/images/operation/ssm-inventory-compilence2.png](/images/operation/ssm-review-compilence2.png)

>**Note**<br>inventory activity를 완료하는데 최대 10 분이 소요될 수 있습니다. inventory activity이 완료되기를 기다리는 동안 다음 섹션으로 진행할 수 있습니다.

## Systems Manager: Compliance

AWS Systems Manager Configuration [Compliance](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-compliance.html)를 사용하여 관리형 인스턴스 집합에 대해 패치 규정 준수 및 구성 일관성을 검사할 수 있습니다. 여러 AWS 계정 및 리전의 데이터를 수집하여 집계한 후 규정을 준수하지 않는 특정 리소스로 드릴다운할 수 있습니다. 기본적으로 구성 규정 준수는 Systems Manager 패치 관리자 패치 및 Systems Manager State Manager 연결에 대한 현재의 규정 준수 데이터를 표시합니다. Systems Manager 규정 준수에는 다음과 같은 추가적인 장점 및 기능이 있습니다.

기본적으로 Configuration Compliance는 **Systems Manager Patch Manager** 패치 및 **Systems Manager State Manager** associations에 대한 준수 데이터를 표시합니다. IT 또는 비즈니스 요구사항에 따라 서비스 사용자를 지정하고 고유한 규정 준수유형을 만들 수도 있습니다. 데이터를 Amazon Athena 및 Amazon QuickSight로 보내 전체 보고서를 생성 할 수도 있습니다.
-->