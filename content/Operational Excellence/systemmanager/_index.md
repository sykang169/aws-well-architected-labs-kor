---
title: "System Manager 셋팅"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>5-1. </b>"
weight: 51
---

## Management Tools: Systems Manager

[AWS Systems Manager](https://aws.amazon.com/systems-manager/features/)는 IT 운영을 가능하게하는 기능들을 모아놓은 서비스 입니다. 

EC2 인스턴스나 [하이브리드 환경](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html)의 on-premises system
을 Systems Manager로 관리하기 위해서는 [설정](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up.html)과 [사전 조건](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html)이 있습니다.

* 지원되는 운영 체제를 사용해야합니다
   * 지원되는 운영 체제에는 Windows, Amazon Linux, Ubuntu Server, RHEL 및 CentOS 버전이 포함됩니다
* SSM 에이전트가 설치되어 있어야합니다
   * 윈도우 환경의 SSM 에이전트를 사용하는 경우는 PowerShell 3.0이상의 버전이 필요하고 낮은 버전의 경우는[SSM documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html#prereqs-powershell)를 확인해주세요.
   * 실습은 CloudFormation의 경우 EC2는 privatesubnet에 위치해있습니다. System Manager가 public network를 통해 EC2에 접근하는 것이 불가능하기 때문에 VPC endpoint가 필요합니다. 
* 지원되는 지역의 Systems Manager에 액세스해야합니다
* Systems Manager에는 IAM 역할이 필요합니다
   * 명령을 처리 할 인스턴스 용
   * 명령을 실행하는 사용자 용

SSM 에이전트는 기본적으로 다음에 설치됩니다.
* 2017 년 9 월 이후의 Amazon Linux _base_ AMI
* Windows Server 2016 인스턴스
* 2016 년 11 월 이후에 배포된 Windows Server 2003-2012 R2 AMI에서 생성 된 인스턴스

[AWS Systems Manager의 추가적인 사용비용은 없습니다.](https://aws.amazon.com/systems-manager/pricing/). AWS Systems Manager에서 관리하거나 생성한 기본 AWS 리소스 (예 : Amazon EC2 인스턴스 또는 Amazon CloudWatch 지표)에 대해서만 비용을 지불합니다. 사용한만큼만 지불하십시오. 최소 비용과 사전 약정은 없습니다.

### 1 Systems Manager 설정
1. 실습환경을 사용하신다면 PrivateSubnet에 위치한 EC2 인스턴스를 위해 VPC endpoint를 생성할 것입니다. EC2에 설치된 System Manager Agent가 System Manager와 통신하기 위해서 필요합니다. AWS Services 메뉴의 VPC로 갑니다. 그리고 왼쪽 메뉴의 **endpoint**를 클릭합니다. 그리고 **Create endpoint**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-create.png)
1. **Service category**의 **AWS Service**를 클릭하고 **Service Name**의 검색창에 ec2를 검색합니다. 그리고 com.amazonaws.<region>.ec2 을 선택하고 맨 아래 **Create endpoint**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-select.png)
1. **VPC**를 선택합니다. 실습에서 생성한 `WellArchitectedLabsStack/VPC`를 검색하여 선택합니다. **Subnets**은 `ùs-west-2a`, `us-west-2b`의 체크박스를 선택하고 모두 **PrivateSubnet**을 선택합니다.
   ![/images/war-operationalexcellence/ssm-agent-vpc.png](/images/war-operationalexcellence/ssm-agent-vpc.png)
1. **Security Group**를 선택합니다. Description에서 EC2인스턴스와 동일한 보안그룹을 선택합니다. 실습환견에서는 `WellArchitectedLabsStack/ASG/InstanceSecurityGroup`을 선택하면 됩니다. 
   ![/images/war-operationalexcellence/ssm-agent-sg.png](/images/war-operationalexcellence/ssm-agent-sg.png)
1. 동일한 방법으로 **SSM**을 검색하여 *com.amazonaws.< region >.ssm*도 선택합니다. 최종적으로 생성된 엔드포인트는 아래와 같이 ec2와 ssm의 엔드포인트가 있어야합니다. 
   ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-endpoint-fin.png)
1. 필요에 따라 아래의 인터페이스를 생성할 수도 있습니다. 
   1. **com.amazonaws.region.ssm**: Systems Manager 서비스에 대한 엔드포인트
   1. **com.amazonaws.region.ec2messages**: Systems Manager에서는 이 엔드포인트를 사용하여 SSM 에이전트에서 Systems Manager 서비스로 호출합니다.
   1. **com.amazonaws.region.ec2**: Systems Manager를 사용하여 VSS 지원 스냅샷을 만든 경우, EC2 서비스에 대한 엔드포인트가 있어야 합니다. EC2 엔드포인트가 정의되어 있지 않으면 연결된 EBS 볼륨을 표시하는 호출이 실패하고 이에 따라 Systems Manager 명령이 실패합니다.
   1. **com.amazonaws.region.ssmmessages**: 이 엔드포인트는 Session Manager를 사용하여 보안 데이터 채널을 통해 인스턴스에 연결하는 경우에만 필요합니다. 자세한 내용은 AWS Systems Manager Session Manager 및 참조: ec2messages, ssmmessages 및 기타 API 호출 단원을 참조하십시오.

1. 게이트웨이 엔드포인트 생성의 단계에 따라 Amazon S3에 대한 다음 게이트웨이 엔드포인트를 생성할 수도 있습니다.
   1. **com.amazonaws.region.s3**: Systems Manager는 이 엔드포인트를 사용하여 SSM 에이전트를 업데이트하고 S3 버킷 저장을 선택한 출력 로그 업로드, 버킷에 저장한 스크립트 또는 기타 파일 검색 등의 작업에 사용합니다.

1. 이제 인스턴스에 IAM role을 추가하겠습니다. 마스터 계정을 사용하여 Systems Manager 콘솔에 접속합니다: <https://console.aws.amazon.com/systems-manager/>.
1. 왼쪽 메뉴에서 **Managed Instances** 를 선택합니다. Systems Manager의 사전조건을 만족하지 않았다면, Start 페이지가 나타나게 됩니다. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)
   * 해당 환경에서 사용되는 인스턴스는 Amazon Linux AMI 2017.09입니다. 이 버전의 [운영체제가 지원하며](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) 사전에 [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html)를 기본으로 설치한 버전입니다.
1. Systems Manager가 관리할 인스턴스를 위한 인스턴스 프로파일을 생성하겠습니다.
   1. [IAM console](https://console.aws.amazon.com/iam/)로 갑니다.
   1. 왼쪽 메뉴중 **Roles**를 클릭합니다.
   1. **Create role**를 클릭합니다.
   1. **Select type of trusted entity** 섹션에서, **AWS service**를 클릭합니다.
   1. 그리고 **Choose the service that will use this role** 섹션에서, 첫번째 선택지인 **EC2**(EC2 Allows EC2 instances to call AWS services on your behalf)를 선택합니다. 그리고 **Next Permission**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-agent.png)

  
1. **Attached permissions policy** 아래, `AmazonEC2RoleforSSM`을 검색하고 체크박스를 선택합니다. 그리고 **Next: Tags**를 클릭합니다.
 ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2.png)

1. **Next Review**를 클릭합니다.

  
1. **Review** 섹션에서는:
   1. **Role name**을 입력합니다: `ManagedInstancesRole`.
   1. 필요하다면 **Role description**도 입력합니다.
   1. **Create role**를 선택합니다.
1. **Systems Manager**로 관리하려는 인스턴스에 이 역할을 적용하십시오.
   1. [EC2 Console](https://console.aws.amazon.com/ec2/)로 가서 **Instances**를 클릭합니다.
   1. IAM role를 연결하려는 인스턴스를 클릭한 후. 상단의 **Actions**, **Instance Settings**, 그리고 **Attach/Replace IAM Role**를 클릭합니다. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach.png)
   1. **Attach/Replace IAM Role**의, `ManagedInstancesRole`를 검색한 뒤 리스트의 해당 role을 선택한 후 **Apply**를 누릅니다.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach-select.png)
   1.  **Systems Manager**로 관리하려는 다른 인스턴스에도 **ManagedInstancesRole** role을 연결합니다.

1. [Systems Manager console](https://console.aws.amazon.com/systems-manager/)로 간 다음, 메뉴의 **Managed Instances**를 클릭합니다. 인스턴스가 목록에 나타날 때까지 주기적으로 **Managed Instances**를 선택하십시오. 몇 분 이 지나야 인스턴스가 **Managed Instances** 목록에 채워집니다.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)

1. 최종적으로 Managed Instance에 등록한 인스턴스를 볼 수 있습니다. 
  ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-agent-fin.png)   
{{% notice info %}}
보안을 위해 [제한적인 권한](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-access-user.html)을 사용하여 Systems Manager에 대한 액세스 권한을 부여 할 수 있습니다.
{{% /notice %}}
