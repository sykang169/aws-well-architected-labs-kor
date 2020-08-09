---
title: "인벤토리"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>1. </b>"
weight: 521
---

## Systems Manager: 인벤토리

[AWS Systems Manager 인벤토리](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-inventory.html)A는 Amazon EC2 및 온프레미스 컴퓨팅 환경에 대한 가시성을 제공합니다. 인벤토리를 사용하여 관리형 인스턴스에서 메타데이터를 수집할 수 있습니다. 이 메타데이터를 중앙 Amazon Simple Storage Service(Amazon S3) 버킷에 저장한 후 기본 제공 도구를 사용하여 데이터를 쿼리하고 어느 인스턴스에서 소프트웨어 정책이 요구하는 소프트웨어 및 구성을 실행 중인지, 어느 인스턴스를 업데이트해야 하는지 빠르게 확인할 수 있습니다. 원클릭 절차를 사용하여 모든 관리형 인스턴스에 대해 인벤토리를 구성할 수 있습니다. 또한 여러 AWS 리전 및 계정으로부터 인벤토리 데이터를 구성하고 볼 수 있습니다.

### 2 Systems Manager 인벤토리를 사용하여 인스턴스 추적

1. AWS Systems Manager 메뉴의 **Instances & Nodes** 아래 **Inventory**를 선택하세요.
   ![/images/operation/ssm-inventory.png](/images/operation/ssm-inventory.png)
   1. 스크롤을 내려 **Corresponding managed instances** 을 선택합니다. 현재 인벤토리에는 EC2에서 사용 가능한 인스턴스 데이터만 포함되어 있습니다.
   1. 당신의 **InstanceID**중 하나를 클릭하세요.
      ![/images/operation/ssm-inventory-click.png](/images/operation/ssm-inventory-click.png)
   1. **Instance ID**이름 아래 다양한 사용 가능한 데이터들을 검토하세요.
   ![/images/operation/ssm-inventory-menu.png](/images/operation/ssm-inventory-menu.png)
1. 이제 인벤토리 수집을 구체적으로 구성하고 수집 할 데이터 유형을 지정해야합니다.
   1. 메뉴의 **Inventory**를 클릭합니다.
   1. 오른쪽 상단의 **Setup Inventory**를 클릭합니다.
   ![/images/operation/ssm-inventory-setup.png](/images/operation/ssm-inventory-setup.png)
1. **Setup Inventory** 화면에서, 인벤토리 대상을 정의하세요:
   1. **Targets**의 **Specify targets by**리스트 중 **Specifying a tag**를 클릭합니다.
   1. **Tags**의 key 값은 `Environment` , value는 `MasterAccount`로 지정하세요.
   >**Note**<br>이 계정에서 모든 관리형 인스턴스를 선택하여 해당 인스턴스의 인벤토리를 확보 할 수 있습니다. Environment 또는 Workload와 같은 특정 태그가있는 인스턴스로 인벤토리 인스턴스를 제한 할 수도 있습니다. 또는 인벤토리의 특정 인스턴스를 수동으로 선택할 수 있습니다.
   ![/images/operation/ssm-inventory-targets.png](/images/operation/ssm-inventory-targets.png)
1. 인벤토리 수집 주기 시간을 설정합니다(기본설정은 30분입니다).
   - **Collect inventory data every**를 **30**분으로 설정합니다.
   ![/images/operation/ssm-inventory-schedule.png](/images/operation/ssm-inventory-schedule.png)
1. **parameters**에서 어떤 정보를 인벤토리에서 수집할지 지정하십시오.
   - 옵션들을 검토하고 기본값들을 선택하세요.
1. (선택사항) 원하는 경우 인벤토리 실행 로그를 수신하도록 S3 버킷을 지정할 수 있습니다(옵션지정 전에 [로그를 저장할 버킷](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) 을 생성해야합니다):
   1. **Advanced**의 **Sync inventory execution logs to an S3 bucket**의 체크박스를 선택하세요.
   1. S3 버킷 이름을 지정합니다.
   1. (선택사항) S3 버킷의 접두어를 지정할 수 있습니다.
   ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-inventory-advanced.png)
1. 아래의 **Setup Inventory**를 선택합니다.(새 인벤토리 정책을 인스턴스에 배포하는 데 최대 10 분이 소요될 수 있습니다).
   ![/images/operation/ssm-inventory-advanced.png](/images/operation/ssm-inventory-finish.png)
1. 새로운 정책을 만드려면 동일 방법으로 추가할 수 있습니다.
1. 기존의 정책을 변경하려면 왼쪽 메뉴의 **State Manager**을 클릭하고 변경할 정책의 **Associations**를 클릭한다음 **Edit**을 선택하세요.

>**Note**<br>여러 Inventory specifications을 생성 할 수 있습니다. 이들은 각각 Systems Manager State Manager 내에 **Associations**으로 저장됩니다.

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