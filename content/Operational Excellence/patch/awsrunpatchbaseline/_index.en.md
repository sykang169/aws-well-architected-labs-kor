---
title: "Run Command"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 532
---

## AWS Systems Manager: Run Command
[AWS Systems Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html) lets you remotely and securely manage the configuration of your managed instances.  Run Command enables you to automate common administrative tasks and perform ad hoc configuration changes at scale. You can use Run Command from the AWS Management Console, the AWS Command Line Interface, AWS Tools for Windows PowerShell, or the AWS SDKs.


In this lab, we use Run Command to patching.

### AWS Systems Manager: Documents

An [AWS Systems Manager document](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html) defines the actions that Systems Manager performs on your managed instances. Systems Manager includes many pre-configured documents that you can use by specifying parameters at runtime, including 'AWS-RunPatchBaseline'. These documents use JavaScript Object Notation (JSON) or YAML, and they include steps and parameters that you specify.

All AWS provided Automation and Run Command documents can be viewed in AWS Systems Manager **Documents**. You can [create your own documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/create-ssm-doc.html) or launch existing scripts using provided documents to implement custom operations as code activities.


#### AWS-RunPatchBaseline
All AWS provided Automation and Run Command documents can be viewed in AWS Systems Manager **Documents**. You can [create your own documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/create-ssm-doc.html) or launch existing scripts using provided documents to implement custom operations as code activities.

<!--
그리고 Systems Manager **Compliance** tools를 사용하여 볼 수 있는 패치 준수 정보를 볼 수 있습니다. 예를 들어 패치가 없는 인스턴스와 설치되지 않은 패치가 무엇인지 확인할 수 있습니다.


Linux 운영 체제의 경우 인스턴스에 구성된 기본소스 리포지토리, 그리고 사용자지정 패치 기준에 지정한 대체 source repositories의 패치에 준수정보가 제공됩니다. AWS-RunPatchBaseline은 Windows 및 Linux 운영 체제를 모두 지원합니다.
!-->

#### 1. **Examine AWS-RunPatchBaseline in Documents**
1. Click in the **search box**, select **Document name prefix**, and then **Equal**.
   ![/images/operation/ssm-documents-fin.png](/images/operation/ssm-documents.png)
3. Click **search box**,  **Document name prefix**and Click **Equal**.
4. Type `AWS-Run` into the text field and press _Enter_ on your keyboard to start the search.
   ![/images/operation/ssm-document-search-fin.png](/images/operation/ssm-document-search.png)
5. Select AWS-RunPatchBaseline and choose **View details**.
   ![/images/operation/ssm-documents-detail.png](/images/operation/ssm-documents-detail.png)
6. Review the content of each tab in the details page of the document.
   ![](/images/operation/runpatchbaseline.png)
<!--
## AWS Systems Manager: Run Command

[AWS Systems Manager Run Command](https://docs.aws.amazon.com/systems-manager/latest/userguide/execute-remote-commands.html)를 통해 관리형 인스턴스의 구성을 원격으로 안전하게 관리할 수 있습니다. 관리형 인스턴스는 Systems Manager용으로 구성된 하이브리드 환경의 EC2 인스턴스 또는 온프레미스 머신입니다. Run Command를 사용하면 일반적인 관리 작업을 자동화하고 대규모로 애드혹 구성을 변경할 수 있습니다. AWS 콘솔, AWS Command Line Interface, AWS Tools for Windows PowerShell 또는 AWS SDK에서 Run Command를 사용할 수 있습니다. 
!-->

#### Scan Your Instances with AWS-RunPatchBaseline via Run Command
1. Under **Instances and Nodes** in the AWS Systems Manager navigation bar, choose **Run Command**. In the Run Command dashboard, you will see previously executed commands including the execution of AWS-RefreshAssociation, which was performed when you set up inventory.
1. Choose **Run Command** in the top right of the window.
   ![/images/operation/ssm-runcommand-start.png](/images/operation/ssm-runcommand-start.png)
1. In the **Run a command** window, under **Command document**:
   * Choose the search icon and select `Platform types`, and then choose `Linux` to display all the available commands that can be applied to Linux instances.
	* Choose **AWS-RunPatchBaseline** in the list.
   ![/images/operation/ssm-runcommand-select.png](/images/operation/ssm-runcommand-select.png)
1. In the **Command parameters** section, leave the **Operation** value as the default **Scan**.
   ![/images/operation/ssm-runcommand-param.png](/images/operation/ssm-runcommand-param.png)
1. In the **Targets** section:
   * Select **Specify instance tags**.
   * Under **Enter a tag key**, enter `Workload`, and under **Enter a tag value**, enter `Prod` and click **Add**.
   ![/images/operation/ssm-runcommand-targets.png](/images/operation/ssm-runcommand-targets.png)

> **Note**
The remaining Run Command features enable you to:
* Specify **Rate control**, limiting **Concurrency** to a specific number of targets or a calculated percentage of systems, or to specify an **Error threshold** by count or percentage of systems after which the command execution will end.
* Specify **Output options** to record the entire output to a preconfigured **S3 bucket** and optional **S3 key prefix**.
>**Note**<br>Only the last 2500 characters of a command document's output are displayed in the console.
* Specify **SNS notifications** to a specified **SNS Topic** on all events or on a specific event type for either the entire command or on a per-instance basis. This requires Amazon SNS to be preconfigured.
* View the command as it would appear if executed within the AWS Command Line Interface.

1. Choose **Run** to execute the command and return to its details page.
1. Scroll down to **Targets and outputs** to view the status of the individual targets that were selected through your tag key and value pair. Refresh your page to update the status.
1. Choose an **Instance ID** from the targets list to view the **Output** from command execution on that instance.
1. Choose **Step 1 - Output** to view the first 2500 characters of the command output from Step 1 of the command, and choose **Step 1 - Output** again to conceal it.
   ![/images/operation/ssm-runcommand-output1.png](/images/operation/ssm-runcommand-output1.png)
1. Choose **Step 2 - Output** to view the first 2500 characters of the command output from Step 2 of the command.  The execution step for **PatchWindows** was skipped as it did not apply to your Amazon Linux instance.

<!--
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
<!--
#### 5. 패치 후 Patch Compliance 리뷰
!-->

#### Review Patch Compliance After Patching
1. Under **Instances & Nodes** in the the AWS Systems Manager navigation bar, choose **Compliance**.
1. The **Compliance resources summary** will now show that there are 4 systems that have satisfied critical severity patch compliance.

### **The Impact of Operations as Code**

In a traditional environment, you would have had to set up the systems and software to perform these activities. You would require a server to execute your scripts. You would need to manage authentication credentials across all of your systems.

_Operations as code_ reduces the resources, time, risk, and complexity of performing operations tasks and ensures consistent execution. You can take operations as code and automate operations activities by using scheduling and event triggers. Through integration at the infrastructure level you avoid "swivel chair" processes that require multiple interfaces and systems to complete a single operations activity.
