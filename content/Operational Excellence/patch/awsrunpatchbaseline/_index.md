---
title: "패치 실행"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 532
---

## AWS-RunPatchBaseline

[AWS-RunPatchBaseline](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html#patch-manager-ssm-documents-recommended-AWS-RunPatchBaseline)은 패치 기준을 사용하여 패치승인을 제어 할 수있는 명령문서입니다. 그리고 Systems Manager **Compliance** tools를 사용하여 볼 수 있는 패치 준수 정보를 볼 수 있습니다. 예를 들어 패치가 없는 인스턴스와 설치되지 않은 패치가 무엇인지 확인할 수 있습니다.

Linux 운영 체제의 경우 인스턴스에 구성된 기본소스 리포지토리, 그리고 사용자지정 패치 기준에 지정한 대체 source repositories의 패치에 준수정보가 제공됩니다. AWS-RunPatchBaseline은 Windows 및 Linux 운영 체제를 모두 지원합니다.


## AWS Systems Manager: 문서

[AWS Systems Manager 문서](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html)는 Systems Manager가 관리형 인스턴스에서 수행하는 작업을 정의합니다. Systems Manager에는 `AWS-RunPatchBaseline`을 포함하여 런타임시 매개 변수를 지정하여 사용할 수있는 많은 **사전-구성 문서**가 포함되어 있습니다. 이 문서는 JSON(JavaScript Object Notation) 또는 YAML을 사용하며 실행단계 및 매개변수를 포함합니다.

AWS가 제공하는 모든 자동화 및 실행 명령 **문서**는 AWS Systems Manager **문서**에서 볼 수 있습니다. 제공된 문서를 사용하여 고유한 문서를 만들거나 기존 스크립트를 시작하여 사용자 지정 작업을 operations as code로 구현할 수 있습니다.

### 1 **문서의 AWS-RunPatchBaseline 검사**

문서의 AWS-RunPatchBaseline를 검사하려면:

1. AWS Systems Manager 메뉴의 **Shared Resources**의 **Documents**를 클릭합니다.
   ![/images/operation/ssm-documents-fin.png](/images/operation/ssm-documents.png)
1. **search box**를 클릭하고, **Document name prefix**를 클릭하고 이어서 **Equal**을 클릭합니다.
1. 그리고 `AWS-Run`입력하고 엔터를 칩니다.
   ![/images/operation/ssm-document-search-fin.png](/images/operation/ssm-document-search.png)
1. **AWS-RunPatchBaseline**를 클릭하고 **View details**을 확인합니다.
1. 문서의 세부 사항 페이지에서 각 탭의 컨텐츠를 검토하십시오.
   ![/images/operation/ssm-documents-detail.png](/images/operation/ssm-documents-detail.png)


## AWS Systems Manager: Run Command

[AWS Systems Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html)를 통해 관리형 인스턴스의 구성을 원격으로 안전하게 관리할 수 있습니다. 관리형 인스턴스는 Systems Manager용으로 구성된 하이브리드 환경의 EC2 인스턴스 또는 온프레미스 머신입니다. Run Command를 사용하면 일반적인 관리 작업을 자동화하고 대규모로 애드혹 구성을 변경할 수 있습니다. AWS 콘솔, AWS Command Line Interface, AWS Tools for Windows PowerShell 또는 AWS SDK에서 Run Command를 사용할 수 있습니다. Run Command는 무료로 제공됩니다.

### 2 Run Command를 통한 AWS-RunPatchBaseline사용하여 인스턴스 스캔
1. **Instances and Nodes** 아래  **Run Command**를 클릭하세요.
1. 오른쪽 상단의 **Run Command**를 클릭하세요.
   ![/images/operation/ssm-runcommand-start.png](/images/operation/ssm-runcommand-start.png)
1. **Run a command**의 **Command document** 섹션:
   * 탐색창을 클릭하고 `Platform types`선택한 다음 `Linux`를 선택합니다. 그리고 다시 탐색창을 클릭하여 `Document name prefix`를 선택하고 `Èquals`를 선택한 다음 `AWS-Run`을 입력합니다.
	* **AWS-RunPatchBaseline**을 선택합니다.
   ![/images/operation/ssm-runcommand-select.png](/images/operation/ssm-runcommand-select.png)
1. **Command parameters**섹션, **Operation**의 기본값 **Scan**을 선택합니다.
   ![/images/operation/ssm-runcommand-param.png](/images/operation/ssm-runcommand-param.png)
1. **Targets** 섹션:
   * **Specify instance tags**를 선택합니다.
   * **Tag key**에 `Workload`, **Tag value**에 `Prod`를 입력하고 **Add**를 클릭합니다.
   ![/images/operation/ssm-runcommand-targets.png](/images/operation/ssm-runcommand-targets.png)

다음 Run Command 기능으로 아래와 같은 것들을 할 수 있습니다:
* **Rate control**를 지정하여 동시에 Run Command가 실행되는 타겟의 숫자를 제한하세요. 
* **Error threshold**를 지정하여 문제가 생긴 인스턴스의 시스템의 숫자나 백분율에 따라 Run Command을 멈출 수 있습니다.
* **Output options** 을 지정하면 사전 구성된 **S3 bucket**및 선택적 **S3 key prefix**를 추가하여 기록할 수 있습니다.
>**Note**<br> 명령 문서의 출력은 마지막 2500자만 콘솔에 표시됩니다.

* 전체 이벤트나 인스턴스별, 모든이벤트 또는 특정이벤트 유형에 대해 경보를 받기위해선 **SNS Topic**에 **SNS notifications**을 지정하십시오. 이를 위해서는 Amazon SNS를 미리 구성해야합니다.
* AWS Command Line Interface 내에서 실행될 경우 명령창을 확인하십시오.

1. **Run**을 클릭해 명령을 실행시키면 세부사항이 나옵니다.
1. 스크롤을 내려 **Targets and outputs**에서 각각 타켓의 상태와 tag의 key와 value가 맞게 설정되어있는지 확인하세요. 페이지를 리프레시하다보면 상태가 업데이트 될 것입니다.
1. 타겟의 **Instance ID**를 클릭하여을 인스턴스가 실행한 명령을 **Output**에서 확인하세요.
1. **Step 1 - Output** 를 확장하면 Step 1 에서 실행한 명령의 2500자 까지 확인할 수 있습니다.
   ![/images/operation/ssm-runcommand-output1.png](/images/operation/ssm-runcommand-output1.png)
1. **Step 2 - Output** 를 확장하면 Step 2 에서 실행한 명령의 2500자 까지 확인할 수 있습니다. **PatchWindows**단계는 Amazon Linux instance는 적용되지 않기 때문에 생략되었습니다.


### 3 초기 Patch Compliance 리뷰

1. **Instances & Nodes**의 **Compliance**를 클릭합니다.
1. **Compliance**에서 **Compliance resources summary**를 보면, critical severity compliance issues가 있는 인스턴스들을 볼 수 있습니다. 아래 **Resources**리스트에서, 개별적인 준수상태와 자세한 내용을 볼 수 있습니다.
   ![/images/operation/ssm-runcommand-compliance.png](/images/operation/ssm-runcommand-compliance.png)


### 4 Run Command를 통한 AWS-RunPatchBaseline사용하여 인스턴스 패치

1. **Instances and Nodes**에서 **Run Command**를 클릭합니다.
1. 상단의 **Run Command**를 클릭합니다.
   ![/images/operation/ssm-patch-install.png](/images/operation/ssm-patch-install.png)
1. **Run a command** 창의, **Command document**섹션에서 아래와 같이 해주세요:
   1. 검색창에 `Platform types`를 입력하여 선택하고 `Linux`검색하여 선택합니다.
   1. 다시 검색창에 `Document name prefix`와 `Equals`를 선택하고 `AWS-Run`을 검색합니다.
   1. **AWS-RunPatchBaseline** 를 선택합니다.
   ![/images/operation/ssm-patch-runcommand.png](/images/operation/ssm-patch-runcommand.png)
1. **Command parameters** 섹션에서 **Operation**를 **Install**로 선택해주세요.
   ![/images/operation/ssm-patch-param.png](/images/operation/ssm-patch-param.png)
1. **Targets** 섹션에서 아래와 같이 해주세요:
   1. **Specify instance tag** 를 선택해주세요.
   1. **Specify instance tags** 의 **Tag Key**에 `Workload`를 입력하고 **Tag value**에 `Prod`를 입력하세요.
   ![/images/operation/ssm-patch-tag.png](/images/operation/ssm-patch-tag.png)
>**Note** **Choose instances manually** 을 선택하고 목록의 체크박스를 체크하여 표시된 모든 인스턴스를 선택하거나 개별적으로 선택할 수 있습니다.
1. **Rate control** 섹션에서는 아래와 같이 해주세요:
   1. **Concurrency**의 **targets**을 선택하고 `1`을 입력해주세요.
   >**Tip**<br>동시에 수행되는 인스턴스의 숫자를 제한하면 패치 응용 프로그램 설치나 재부팅 주기가 늦어질 수 있습니다. 인스턴스가 동시에 재부팅되지 않도록하려면 별도의 태그를 만들어 대상 그룹을 정의하고 별도의 시간에 패치 적용을 예약하십시오.
   2. **Error threshold**의 **error**를 선택하고 `1`을 입력해주세요.
  ![/images/operation/ssm-patch-tag.png](/images/operation/ssm-patch-tag.png)

1. **Run**을 클릭하고 명령을 실행합니다. 
1. 업데이트 된 상태를 보고 실행이 성공하면 페이지를 새로 고칩니다.
  ![/images/operation/ssm-patch-run.png](/images/operation/ssm-patch-run.png)

>**Warning**<br>Patch Manager가 업데이트를 설치하면 패치 된 인스턴스가 재부팅됩니다.

### 5 패치 후 패치 준수 검토

1. **Instances & Nodes** 아래 **Compliance**를 클릭합니다.
1. The **Compliance resources summary**에 중요한 심각도 패치 컴플라이언스를 충족하는 2개의 시스템이 있음이 표시됩니다.

### **The Impact of Operations as Code**
전통적인 환경에서는 이러한 활동을 수행하기 위해 시스템과 소프트웨어를 설정해야했습니다. 그리고 스크립트를 실행하려면 서버가 필요합니다. 또한 모든 시스템에서 인증 자격 증명을 관리해야합니다.
코드로서의 운영은 운영작업수행의 자원, 시간, 위험 및 복잡성을 줄이고 일관된 실행을 보장합니다. 스케줄링 및 이벤트 트리거를 사용하여 모든조작을 코드로 수행하고 자동화 할 수 있습니다. 무엇보다 인프라수준의 통합을 통해 단일작업 활동을 완료하기 위해 여러 인터페이스와 시스템을 왔다갔다하는 "회전의자" 프로세스를 피할 수 있습니다.