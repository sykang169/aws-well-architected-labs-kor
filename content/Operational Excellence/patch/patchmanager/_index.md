---
title: "패치 관리자"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>1. </b>"
weight: 531
---

## Systems Manager: 패치 관리자(Patch Manager)

AWS Systems Manager [패치 관리자](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-patch.html)는 보안 관련 및 기타 유형의 업데이트로 관리형 인스턴스에 패치를 적용하는 프로세스를 자동화해 줍니다.

>**Note**<br> Linux 기반 인스턴스의 경우 non-security 업데이트 패치를 설치할 수 있습니다.

운영체제 유형별로 Amazon EC2인스턴스 또는 온프레미스 서버 및 가상머신(VM)을 패치할 수 있습니다. 지원되는 버전은 Windows, Ubuntu Server, RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Amazon Linux가 포함됩니다. 인스턴스를 스캔하여 누락된 패치에 대한 보고서만 보거나 누락된 모든 패치를 스캔하고 자동으로 설치할 수 있습니다. Amazon EC2 태그를 사용하여 인스턴스를 개별적으로 또는 대규모 그룹으로 패치를 수행할 수도 있습니다.

> **Warnings**
>  * 패치 관리자를 통해 고객에게 패치를 제공하기 전 AWS는 별도로 Windows 또는 Linux 패치를 테스트하지 않습니다. 
>  * 패치관리자가 업데이트를 수행 시 패치 된 인스턴스는 재부팅 됩니다.
>  * 프로덕션 환경에 적용하기 전 철저히 패치를 테스트 해야 합니다.


## 패치 기준(Patch Baseline)


Patch Manager는 패치 기준(Patch Baseline)을 사용합니다. 여기에는 패치가 출시 된 후 며칠 이내에 패치를 자동 승인하는 규칙과 승인 및 거부 된 패치 목록이 포함됩니다. 이 실습의 뒷부분에서 Systems Manager 유지 관리 기간 작업을 사용하여 정기적으로 패치를 적용하도록 예약합니다. Patch Manager는 AWS Identity and Access Management (IAM), AWS CloudTrail 및 Amazon CloudWatch Events와 통합되어 이벤트 알림 및 사용 감사 기능을 포함하는 안전한 패치 경험을 제공합니다.

<!--
패치 관리자는 **패치 기준**을 사용합니다. 패치 기준은 인스턴스에 대한 설치가 승인되는 패치를 정의합니다. 패치 승인 또는 거부는 하나씩 지정할 수 있습니다. 또한 자동 승인 규칙을 생성하여 특정 유형의 업데이트(예: 필수 업데이트)가 자동 승인되도록 지정할 수도 있습니다. 거부된 목록은 규칙 및 승인 목록을 모두 재정의합니다.

승인된 패치 목록을 사용하여 특정 패키지를 설치하려면 먼저 모든 자동 승인 규칙을 제거하십시오. 임의 패치를 명시적으로 거부로 구분하면 해당 패치는 자동 승인 규칙의 모든 기준을 만족하더라도 승인 또는 설치되지 않습니다. 또한 패치가 해당 인스턴스에 대해 승인되었더라도 인스턴스의 소프트웨어에 적용되는 경우에만 패치가 인스턴스에 설치됩니다.

패치 관리자는 패치 관리자에서 지원하는 운영 체제마다 사전 정의된 패치 기준을 제공합니다. 이러한 기준은 현재 구성된 대로 사용하거나(사용자 지정할 수 없음) 고유한 사용자 지정 패치 기준을 생성할 수 있습니다. 사용자 지정 패치 기준을 사용하면 환경에 대해 승인 또는 거부되는 패치를 더욱 효과적으로 제어할 수 있습니다. 또한 미리 정의된 기준은 해당 기준을 사용하여 설치된 모든 패치에 Unspecified의 규정 준수 수준을 할당합니다. 규정 준수 값을 할당하려면 미리 정의된 기준의 복사본을 생성하고 패치에 할당할 규정 준수 값을 지정할 수 있습니다. 자세한 내용은 사용자 지정 기준 정보 및 사용자 지정 패치 기준 생성 단원을 참조하십시오.
--> 

>**Warning**<br> [패치 관리자가 지원하는 운영 체제](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html)는 SSM 에이전트가 지원하는 운영 체제와 다를 수 있습니다.


### 1. 패치 기준 생성

1. **AWS Systems Manager**의 **Instances and Nodes**에서 **패치 관리자**를 클릭합니다.
1. **Configure patching** 버튼 아래 **View predefined patch baseline** 버튼을 클릭합니다.
   ![/images/operation/ssm-patch-start.png](/images/operation/ssm-patch-start.png)
1. **Create patch baseline**를 클릭합니다.
   ![/images/operation/ssm-patch-baseline.png](/images/operation/ssm-patch-baseline.png)
1. **Create patch baseline**의 **Provide patch baseline details** 섹션은 아래와 같이 작업합니다:
   1. **Name** 에 `AmazonLinuxSecAndNonSecBaseline`를 입력합니다.
   1. **Description**은 `Amazon Linux patch baseline including security and non-security patches`를 입력합니다.
   1. **Operation system**은 **Amazon Linux2**를 선택합니다.
   ![/images/operation/ssm-patch-detail.png](/images/operation/ssm-patch-detail.png)
1. **Approval rules** 섹션은 아래와 같이 작업합니다:
   1. 옵션을 검토하고 **Product**, **Classification**, 그리고 **Severity** 가 **All**값을 갖는지 확인합니다.
   1. **Auto approval delay**는 기본값인 **0 days**로 셋팅합니다.
   1. **Compliance reporting - optional** 의 값을 **Critical**로 선택합니다.
   ![/images/operation/ssm-patch-rule1.png](/images/operation/ssm-patch-rule1.png)
   1. **Add rule**을 클릭하여 규칙을 하나 더 추가 합니다.
   1. **Compliance reporting - optional** 의 값을 **Medium**로 선택합니다.
   1. 모든 Amazon Linux 업데이트에 비보안 업데이트를 포함하려면 **Include non-security updates**를 체크합니다.
   ![/images/operation/ssm-patch-rule2.png](/images/operation/ssm-patch-rule2.png)
1. **Patch exceptions** 섹션에서 **Rejected patches - optional** 텍스트 박스에 `system-release.*`입력합니다. 이것은 새로운 Amazon Linux 배포될때,[패치 관리자가 지원하는 운영체제](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html)가 관리할 수 있는 버전보다 앞선다면 새로운 릴리지를 테스트하기 전까지 [패치를 거부합니다.](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-approved-rejected-package-name-formats.html)
1. Linux 운영 체제의 경우 [대체 patch source repository](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-how-it-works-alt-source-repository.html)를 선택적으로 정의 할 수 있습니다. 빈 patch source 정의를 제거하려면 **Patch sources** 영역에서 **X**를 선택하십시오. 이번 실습에서는 아무것도 선택하지 않습니다.
**Create patch baseline**을 선택하면 AWS에서 제공 한 기본 **패치기준** 페이지로 이동합니다.
![/images/operation/ssm-patch-exception.png](/images/operation/ssm-patch-exception.png)
1. 하단의 **Create patch baseline**을 클릭하여 생성을 완료합니다.
   승인 된 패치가 누락 되면 **Compliance reporting**에서 선택한 옵션에 따라 `Critical` 또는 `Medium`의 컴플라이언스 위반의 심각도가 결정되며 System Manager **Compliance**로 보고됩니다.


## 패치 그룹

[패치 그룹](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-patch-patchgroups.html)은 패치를 위해 인스턴스를 구성하는 방법중 하나입니다. 예를들어, 다른운영체제 (Linux 또는 Windows), 다른환경(개발,테스트 및 프로덕션) 또는 다른서버기능(웹서버, 파일서버, 데이터베이스)에 대한 패치 그룹을 작성할 수 있습니다. 패치 그룹을 사용하면 잘못된 인스턴스 세트에 패치를 배포하지 않아도 됩니다. 그리고 테스트하기 전에 패치배포가 배포되는 것을 피할 수 있습니다.
 
Amazon EC2 태그를 사용하여 패치 그룹을 생성합니다. Systems Manager의 다른 태깅 시나리오와 달리 패치 그룹은 태그 키 `Patch Group`으로 정의해야합니다 (태그 키는 대소 문자를 구분 함). 임의의 값 (예 :`web servers`)을 지정할 수 있지만 키는`Patch Group`이어야합니다.

>**Note**<br> 인스턴스는 하나의 패치 그룹에만 있을 수 있습니다.

패치 그룹 및 태그 인스턴스를 생성 한 후 패치 기준에 패치 그룹을 등록 할 수 있습니다. 패치 기준에 패치 그룹을 등록하면 패치실행 할 때 올바른 패치를 실행할 수 있습니다. 
* 인스턴스가 패치 그룹에 할당 된 경우 시스템은 해당 그룹에 등록 된 패치 기준을 확인합니다.
* 해당 그룹에 대한 패치 기준이있는 경우 시스템은 해당 패치 기준을 적용합니다.
* 인스턴스가 패치 그룹에 할당되지 않은 경우 시스템은 현재 구성된 default 패치 기준을 자동으로 사용합니다.

### 2. 패치 그룹 할당하기

1. 새로 생성된 baseline **Baseline ID**를 클릭하여 세부 정보 화면을 입력합니다.(Baseline ID가 보이지 않는다면 페이지를 넘겨보세요. 이 실습에서 만든 baseline name은 `AmazonLinuxSecAndNonSecBaseline`입니다.)
![/images/operation/ssm-patch-pg.png](/images/operation/ssm-patch-pg.png)
1. **Actions**을 클릭하고 **Modify patch groups**를 클릭합니다.
![/images/operation/ssm-patch-pg-set.png](/images/operation/ssm-patch-pg-set.png)
1. **Modify patch groups** 아래 **Patch groups** 박스에, `Critical`를 입력하고 **Add**클릭합니다,
![/images/operation/ssm-patch-pg-critical.png](/images/operation/ssm-patch-pg-critical.png)
1. **Close**를 클릭하여 **Patch Baseline**으로 되돌아가 세부정보를 확인합니다.
![/images/operation/ssm-patch-fin.png](/images/operation/ssm-patch-fin.png)
인스턴스가 패치 그룹에 할당 된 경우 시스템은 해당 그룹에 등록 된 패치 기준을 확인합니다.
해당 그룹에 대한 패치 기준이있는 경우 시스템은 해당 패치 기준을 적용합니다.
인스턴스가 패치 그룹에 할당되지 않은 경우 시스템은 현재 구성된 기본 패치 기준을 자동으로 사용합니다.
