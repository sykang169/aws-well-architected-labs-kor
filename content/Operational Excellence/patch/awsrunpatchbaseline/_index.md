---
title: "Run Command"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 532
---

## AWS Systems Manager: Run Command
AWS Systems Manager에서는 **서버에 로그인하지 않고** **대규모로 인스턴스를 원격으로 안전하게 관리**할 수 있는 기능을 제공하므로, 배스천 호스트, SSH 또는 원격 PowerShell이 필요 없습니다. 레지스트리 편집, 사용자 관리, 소프트웨어 및 패치 설치와 같은 **일반적인 관리 작업을** 인스턴스 그룹 전체에서 **자동화**하는 간단한 방법을 제공합니다. AWS Identity and Access Management(IAM)와의 통합을 통해 세분화된 권한을 적용하여 사용자가 인스턴스에 수행할 수 있는 작업을 **제어**할 수 있습니다. Systems Manager가 수행한 모든 작업이 AWS CloudTrail에 기록되기 때문에 환경 전체의 **변경 사항을 감사**할 수도 있습니다. Run Command는 무료로 제공됩니다.

이번 실습에서는 Run Command를 이용해 패치 작업을 수행합니다.

### AWS Systems Manager: 문서 (Documents)

AWS Systems Manager의 [문서](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html)는 관리형 인스턴스에서 수행하는 작업을 정의합니다. Systems Manager에는 'AWS-RunPatchBaseline'을 포함하여 런타임에 파라미터를 지정하여 사용하실 수 있는 사전 구성된 문서를 제공합니다. 문서는 JSON (JavaScript Object Notation) 또는 YAML 기반이며 사용자가 작업 단계와 매개 변수를 담고 있습니다.

AWS에서 제공하는 모든 자동화 및 Run Command 문서는 AWS Systems Manager **문서**에서 확인하실 수 있습니다. AWS가 제공하는 문서를 사용하여 기존 스크립트를 실행할 수도, 또는 [사용자가 직접 고유한 문서를 생성하여 사용자 지정 작업을 코드로 구현](https://docs.aws.amazon.com/systems-manager/latest/userguide/create-ssm-doc.html)할 수도 있습니다.

#### AWS-RunPatchBaseline
인스턴스에 패치를 설치하거나 인스턴스를 스캔하여 패치가 누락되었는지 확인하는 **문서**로, AWS가 기본으로 제공합니다. 해당 문서에 대한 상세 설명은 다음 [링크](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-ssm-documents.html#patch-manager-ssm-documents-recommended-AWS-RunPatchBaseline)를 참고합니다.
<!--
그리고 Systems Manager **Compliance** tools를 사용하여 볼 수 있는 패치 준수 정보를 볼 수 있습니다. 예를 들어 패치가 없는 인스턴스와 설치되지 않은 패치가 무엇인지 확인할 수 있습니다.


Linux 운영 체제의 경우 인스턴스에 구성된 기본소스 리포지토리, 그리고 사용자지정 패치 기준에 지정한 대체 source repositories의 패치에 준수정보가 제공됩니다. AWS-RunPatchBaseline은 Windows 및 Linux 운영 체제를 모두 지원합니다.
!-->

#### 1. 문서(Documents)에서 AWS-RunPatchBaseline가 담고 있는 내용을 직접 확인해 보겠습니다.
1. AWS Systems Manager 메뉴의 **Shared Resources**의 **Documents**를 클릭합니다.
   ![/images/operation/ssm-documents-fin.png](/images/operation/ssm-documents.png)
3. **search box**를 클릭하고, **Document name prefix**를 클릭하고 이어서 **Equal**을 클릭합니다.
4. 그리고 `AWS-Run`입력하고 엔터를 쳐서 검색합니다.
   ![/images/operation/ssm-document-search-fin.png](/images/operation/ssm-document-search.png)
5. **AWS-RunPatchBaseline**를 찾아 선택한 후 **View details**을 클릭합니다.
<<<<<<< HEAD
6. 해당 문서의 각 탭의 내용을 살펴봅니다. 특히 **Contents** 탭을 클릭하면 이 문서가 담고 있는 **실행 명령**의 상세 내용을 확인할 수 있습니다.
   ![/images/operation/ssm-documents-detail.png](/images/operation/ssm-documents-detail.png)

=======
   ![/images/operation/ssm-documents-detail.png](/images/operation/ssm-documents-detail.png)
6. 해당 문서의 각 탭의 내용을 살펴봅니다. 특히 **Contents** 탭을 클릭하면 이 문서가 담고 있는 **실행 명령**의 상세 내용을 확인할 수 있습니다.
   ![](/images/operation/runpatchbaseline.png)
>>>>>>> 10ff751802894533b4d2ed100b73d3961dc3be45
<!--
## AWS Systems Manager: Run Command

[AWS Systems Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html)를 통해 관리형 인스턴스의 구성을 원격으로 안전하게 관리할 수 있습니다. 관리형 인스턴스는 Systems Manager용으로 구성된 하이브리드 환경의 EC2 인스턴스 또는 온프레미스 머신입니다. Run Command를 사용하면 일반적인 관리 작업을 자동화하고 대규모로 애드혹 구성을 변경할 수 있습니다. AWS 콘솔, AWS Command Line Interface, AWS Tools for Windows PowerShell 또는 AWS SDK에서 Run Command를 사용할 수 있습니다. 
!-->

#### 2. Run Command에서 AWS-RunPatchBaseline를 사용하여 인스턴스 스캔을 실행하기
1. **Instances and Nodes** 아래  **Run Command**를 클릭하세요.
1. 오른쪽 상단의 **Run Command**를 클릭하세요.
   ![/images/operation/ssm-runcommand-start.png](/images/operation/ssm-runcommand-start.png)
1. **Run a command**의 **Command document** 섹션:
   * 탐색창을 클릭하고 `Platform types`선택한 다음 `Linux`를 선택합니다. 그리고 다시 탐색창을 클릭하여 `Document name prefix`를 선택하고 `Equals`를 선택한 다음 `AWS-Run`을 입력합니다.
	* **AWS-RunPatchBaseline**을 선택합니다.
   ![/images/operation/ssm-runcommand-select.png](/images/operation/ssm-runcommand-select.png)
1. **Command parameters**섹션, **Operation**의 기본값 **Scan**을 선택합니다.
   ![/images/operation/ssm-runcommand-param.png](/images/operation/ssm-runcommand-param.png)
1. **Targets** 섹션:
   * **Specify instance tags**를 선택합니다.
   * **Tag key**에 `Workload`, **Tag value**에 `Prod`를 입력하고 **Add**를 클릭합니다.
   ![/images/operation/ssm-runcommand-targets.png](/images/operation/ssm-runcommand-targets.png)

> **Note**
> Run Command에서 다음 옵션들이 제공하는 기능을 알아봅시다:
> * **Rate control**를 지정하여 동시에 Run Command가 실행되는 타겟의 숫자를 제한합니다. **Error threshold**를 지정하여 문제가 생긴 인스턴스의 시스템의 숫자나 백분율에 따라 Run Command을 중단합니다.
> * **Output options**을 지정하면 **S3 bucket**에 (선택시) **S3 key prefix**를 추가하여 로깅합니다. 
> * **SNS Topic**에 **SNS notifications**을 지정하여 전체 이벤트나 인스턴스별, 모든 이벤트 또는 특정 이벤트 유형에 대해 경보를 설정합니다. 
> * AWS command line interface command에서 실행될 CLI 명렁어를 확인할 수 있습니다. 

1. **Run**을 클릭해 명령을 실행시키면 세부사항이 나옵니다.
2. 스크롤을 내려 **Targets and outputs**에서 각각 타켓의 상태와 tag의 key와 value가 맞게 설정되어있는지 확인합니다. 페이지를 새로고침 하다보면 상태가 업데이트 될 것입니다.
3. 타겟의 **Instance ID**를 클릭하여 인스턴스가 실행한 명령을 **Output**에서 확인합니다.
4. **Step 1 - Output** 를 펼쳐 내용을 확인합니다. Step 1에서 리눅스 대상 패치를 스캔한 명령을 확인할 수 있습니다.
   ![/images/operation/ssm-runcommand-output1.png](/images/operation/ssm-runcommand-output1.png)
5. **Step 2 - Output** 를 펼쳐 내용을 확인합니다. Step 2에서는 윈도우 대상 패치이므로 생략했음을 확인할 수 있습니다. 
<<<<<<< HEAD


=======

<!--
>>>>>>> 10ff751802894533b4d2ed100b73d3961dc3be45
#### 3. Patch Compliance 현재 상태 리뷰 (패치 적용 전)

1. **Instances & Nodes**의 **Compliance**를 클릭합니다.
1. **Compliance**에서 **Compliance resources summary**를 보면, critical severity compliance issues가 있는 인스턴스들을 볼 수 있습니다. 아래 **Resources**리스트에서, 개별적인 준수상태와 자세한 내용을 볼 수 있습니다.
   ![/images/operation/ssm-runcommand-compliance.png](/images/operation/ssm-runcommand-compliance.png)


#### 4. Run Command를 통한 AWS-RunPatchBaseline를 이용해 패치 적용하기

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

<!-- 
>**Warning**<br>
> * Patch Manager가 업데이트를 설치하면 패치 된 인스턴스가 재부팅됩니다.
!-->
<<<<<<< HEAD

#### 5. 패치 후 Patch Compliance 리뷰

1. **Instances & Nodes** 아래 **Compliance**로 이동합니다.
1. The **Compliance resources summary**에 중요한 심각도 패치 컴플라이언스를 충족하는 2개의 시스템이 있음이 표시됩니다.
=======
<!--
#### 5. 패치 후 Patch Compliance 리뷰
!-->

#### 패치 스캔 후 Compliance 리뷰
1. **Instances & Nodes** 아래 **Compliance**로 이동합니다.
2. The **Compliance resources summary**에 **Compliance type** **Patch**를 준수하는 2개의 리소스가 있다는 것을 확인할 수 있습니다. 만약 Non-Compliant라면 리뷰 후 Run Command에서 이번에는 **Scan**이 아닌 **Install**로 조치를 취할 수 있을 것입니다.
>>>>>>> 10ff751802894533b4d2ed100b73d3961dc3be45

### **코드로 운영하기가 가져다주는 기대효과**
전통적인 환경에서는 이러한 활동을 수행하기 위해 시스템과 소프트웨어를 직접 설정해야 했습니다. 그리고 스크립트를 실행하기 위한 서버도 필요했지요. 모든 시스템의 인증 자격 증명을 관리해야 할 필요도 있었습니다. 
**코드로 운영하기**는 운영에 필요한 작업을 수행하는 데에 들여야 하는 자원, 시간, 위험 및 복잡성을 줄일 뿐만 아니라 일관된 실행을 보장합니다. 스케줄링 및 이벤트 트리거를 사용하여 모든 조작을 코드로 수행하고 자동화할 수 있습니다. 무엇보다 인프라 수준의 통합을 통해 단일 작업 활동을 완료하기 위해 여러 인터페이스와 시스템을 왔다 갔다할 필요가 없어졌습니다.