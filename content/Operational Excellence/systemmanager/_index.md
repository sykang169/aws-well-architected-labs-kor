---
<<<<<<< HEAD
title: "AWS System Manager"
=======
title: "System Manager 구성"
>>>>>>> upstream/master
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>5-1. </b>"
weight: 51
---

<<<<<<< HEAD

### 운영 우수성과 AWS System Manager

{{% notice note %}}
여러 AWS 서비스의 운영 데이터를 중앙집중화하고 AWS 리소스 전체에서 작업을 자동화할 수 있습니다. 애플리케이션, 애플리케이션 스택의 다양한 계층 또는 프로덕션 환경 대 개발 환경 같은 논리적 리소스 그룹을 만들 수 있습니다. Systems Manager에서는 리소스 그룹을 선택하여 리소스 그룹의 최근 API 작업, 리소스 구성 변경, 관련 알림, 운영 경보, 소프트웨어 인벤토리, 패치 규정 준수 상태를 볼 수 있습니다. 운영상 필요에 따라 각 리소스 그룹에 대한 조치를 취할 수도 있습니다. 상세 내용은 [링크](https://aws.amazon.com/ko/systems-manager/features/)를 참고합니다. 
{{% /notice%}}

#### 인벤토리
AWS Systems Manager는 인스턴스와 인스턴스에 설치된 소프트웨어에 대한 정보를 수집하여 시스템 구성과 설치된 애플리케이션에 대해 이해할 수 있도록 지원합니다. 애플리케이션, 파일, 네트워크 구성, Windows 서비스, 레지스트리, 서버 역할, 업데이트, 기타 시스템 속성을 수집할 수 있습니다. 수집된 데이터를 통해 애플리케이션 자산을 관리하고, 라이선스를 추적하고, 파일 무결성을 모니터링하고, 기존 설치 프로그램으로 설치하지 않은 애플리케이션을 찾을 수 있습니다.

#### Run Command
AWS Systems Manager에서는 서버에 로그인하지 않고 대규모로 인스턴스를 원격으로 안전하게 관리할 수 있는 기능을 제공하므로, 배스천 호스트, SSH 또는 원격 PowerShell이 필요 없습니다. 레지스트리 편집, 사용자 관리, 소프트웨어 및 패치 설치와 같은 일반적인 관리 작업을 인스턴스 그룹 전체에서 자동화하는 간단한 방법을 제공합니다. AWS Identity and Access Management(IAM)와의 통합을 통해 세분화된 권한을 적용하여 사용자가 인스턴스에 수행할 수 있는 작업을 제어할 수 있습니다. Systems Manager가 수행한 모든 작업이 AWS CloudTrail에 기록되기 때문에 환경 전체의 변경 사항을 감사할 수도 있습니다.

#### 패치 관리자
AWS Systems Manager는 대규모 Amazon EC2 그룹 또는 온프레미스 인스턴스 전체에서 자동으로 운영 체제 및 소프트웨어 패치를 선택 및 배포하도록 지원합니다. 패치 기준선을 통해 운영 체제 또는 높은 심각도 패치 등 선택한 카테고리의 패치를 자동 승인하도록 규칙을 설정할 수 있고, 이러한 규칙을 무시하고 자동 승인 또는 거부할 패치 목록을 지정할 수 있습니다. 또한, 미리 설정된 시간에만 패치가 적용되도록 패치에 대한 유지 관리 기간을 예약할 수 있습니다. Systems Manager는 소프트웨어를 최신으로 유지하고 규정 준수 정책을 충족하는 데 도움이 됩니다.

#### 유지 관리 기간
AWS Systems Manager를 사용하면 인스턴스 전체에서 관리 및 유지 보수 작업을 실행할 시간대를 예약할 수 있습니다. 따라서 패치 및 업데이트를 설치하거나 다른 구성 변경 사항을 적용할 편리하고 안전한 시간을 선택할 수 있으므로 서비스와 애플리케이션의 가용성과 안정성을 향상할 수 있습니다.

#### Run Command
AWS Systems Manager에서는 서버에 로그인하지 않고 대규모로 인스턴스를 원격으로 안전하게 관리할 수 있는 기능을 제공하므로, 배스천 호스트, SSH 또는 원격 PowerShell이 필요 없습니다. 레지스트리 편집, 사용자 관리, 소프트웨어 및 패치 설치와 같은 일반적인 관리 작업을 인스턴스 그룹 전체에서 자동화하는 간단한 방법을 제공합니다. AWS Identity and Access Management(IAM)와의 통합을 통해 세분화된 권한을 적용하여 사용자가 인스턴스에 수행할 수 있는 작업을 제어할 수 있습니다. Systems Manager가 수행한 모든 작업이 AWS CloudTrail에 기록되기 때문에 환경 전체의 변경 사항을 감사할 수도 있습니다.


{{% notice note %}}
[AWS Systems Manager](https://aws.amazon.com/systems-manager/features/)는 IT 운영에서 활용할 수 있는 [많은 기능들을 제공](https://aws.amazon.com/ko/systems-manager/features/)합니다. EC2 뿐ㅁ나 아니라 하이브리드 환경도 지원하므로 AWS Systems Manager를 사용하면 AWS와 온프레미스 데이터 센터에서 실행되는 서버를 모두 단일 인터페이스에서 관리할 수 있습니다. Systems Manager는 서버에 설치된 경량 에이전트와 안전하게 통신하여 관리 작업을 수행합니다. 
AWS Systems Manager로 EC2 인스턴스 및 [하이브리드 환경](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html)을 관리하기 위해 필요한 [요구 사항](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) 및 [필요한 설정](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up.html)에 대한 상세 내용은 문서를 참고합니다.
{{% /notice%}}

[AWS Systems Manager의 추가 사용 요금은 없습니다.](https://aws.amazon.com/systems-manager/pricing/) AWS Systems Manager에서 관리하거나 생성한 기본 AWS 리소스(예: Amazon EC2 인스턴스 또는 Amazon CloudWatch 지표)에 대해서 사용한 만큼만 비용을 지불합니다. 최소 비용과 사전 약정은 없습니다.

=======
{{% notice note %}}
[AWS Systems Manager](https://aws.amazon.com/systems-manager/features/)는 IT 운영에서 활용할 수 있는 [많은 기능들을 제공](https://aws.amazon.com/ko/systems-manager/features/)합니다. EC2 뿐ㅁ나 아니라 하이브리드 환경도 지원하므로 AWS Systems Manager를 사용하면 AWS와 온프레미스 데이터 센터에서 실행되는 서버를 모두 단일 인터페이스에서 관리할 수 있습니다. Systems Manager는 서버에 설치된 경량 에이전트와 안전하게 통신하여 관리 작업을 수행합니다. 
AWS Systems Manager로 EC2 인스턴스 및 [하이브리드 환경](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html)을 관리하기 위해 필요한 [요구 사항](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) 및 [필요한 설정](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up.html)에 대한 상세 내용은 문서를 참고합니다.
{{% /notice%}}

[AWS Systems Manager의 추가 사용 요금은 없습니다.](https://aws.amazon.com/systems-manager/pricing/) AWS Systems Manager에서 관리하거나 생성한 기본 AWS 리소스(예: Amazon EC2 인스턴스 또는 Amazon CloudWatch 지표)에 대해서 사용한 만큼만 비용을 지불합니다. 최소 비용과 사전 약정은 없습니다.

>>>>>>> upstream/master
<!--
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
* 2017년 9월 이후의 Amazon Linux _base_ AMI
* Windows Server 2016 인스턴스
* 2016년 11월 이후에 배포된 Windows Server 2003-2012 R2 AMI에서 생성된 인스턴스
!-->
<<<<<<< HEAD

  
### AWS Systems Manager 구성
본 실습을 진행하기 위해서는 AWS Systems Manager에 다음 작업들이 사전에 진행되어야 합니다.
1. **VPC 엔드포인트 생성** 
: 실습 환경에서는 EC2가 Private Subnet에 위치하고 있습니다. 본 실습에서는 AWS Systems Manager가 퍼블릭 IP 필요 없이 [VPC 엔드포인트](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-endpoints.html)를 통해 비공개로 연결하도록 구성합니다.
2. **IAM 역할 생성 및 EC2에 할당**
: AWS Systems Manager로 관리할 EC2 인스턴스에 연결할 IAM 역할을 생성하여 권한을 부여합니다. 


=======

  
### AWS Systems Manager 구성
본 실습을 진행하기 위해서는 AWS Systems Manager에 다음 작업들이 사전에 진행되어야 합니다.
1. **VPC 엔드포인트 생성** 
: 실습 환경에서는 EC2가 Private Subnet에 위치하고 있습니다. 본 실습에서는 AWS Systems Manager가 퍼블릭 IP 필요 없이 [VPC 엔드포인트](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-endpoints.html)를 통해 비공개로 연결하도록 구성합니다.
2. **IAM 역할 생성 및 EC2에 할당**
: AWS Systems Manager로 관리할 EC2 인스턴스에 연결할 IAM 역할을 생성하여 권한을 부여합니다. 


>>>>>>> upstream/master
#### VPC 엔드포인트 생성
1. AWS Services 메뉴의 [VPC](https://console.aws.amazon.com/vpc)로 이동합니다. 그리고 왼쪽 메뉴의 **endpoint**를 클릭합니다. 그리고 **Create endpoint**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-create.png)
1. **Service category**의 **AWS Service**를 클릭하고 **Service Name**의 검색창에 ec2를 검색합니다. 그리고 com.amazonaws.<region>.ec2 을 선택하고 맨 아래 **Create endpoint**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-select.png)
<<<<<<< HEAD
2. **VPC**를 선택합니다. 실습에서 생성한 `WellArchitectedLabsStack/VPC`를 검색하여 선택합니다. **Subnets**은 `us-west-2a`, `ap-northeast-2b`의 체크박스를 선택하고 모두 **PrivateSubnet**을 선택합니다.
=======
2. **VPC**를 선택합니다. 실습에서 생성한 `WellArchitectedLabsStack/VPC`를 검색하여 선택합니다. **Subnets**은 `ap-northeast-2b`, `ap-northeast-2b`의 체크박스를 선택하고 모두 **PrivateSubnet**을 선택합니다.
>>>>>>> upstream/master
   ![/images/war-operationalexcellence/ssm-agent-vpc.png](/images/war-operationalexcellence/ssm-agent-vpc.png)
3. **Security Group**를 선택합니다. Description에서 EC2인스턴스와 동일한 보안그룹을 선택합니다. 실습환견에서는 `WellArchitectedLabsStack/ASG/InstanceSecurityGroup`을 선택하면 됩니다. 
   ![/images/war-operationalexcellence/ssm-agent-sg.png](/images/war-operationalexcellence/ssm-agent-sg.png)
4. 동일한 방법으로 **SSM**을 검색하여 *com.amazonaws.< region >.ssm*도 선택합니다. 
5. 최종적으로 생성된 엔드포인트는 아래와 같이 ec2와 ssm의 2개의 최소한 엔드포인트가 있어야 합니다.  
   ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-endpoint-fin.png)

<!--
{{% notice tip %}}
필요에 따라 아래의 인터페이스를 생성할 수도 있습니다. 
{{% /notice%}}
   - **com.amazonaws.region.ssm**: Systems Manager 서비스에 대한 엔드포인트
   - **com.amazonaws.region.ec2messages**: Systems Manager에서는 이 엔드포인트를 사용하여 SSM 에이전트에서 Systems Manager 서비스로 호출합니다.
   - **com.amazonaws.region.ec2**: Systems Manager를 사용하여 VSS 지원 스냅샷을 만든 경우, EC2 서비스에 대한 엔드포인트가 있어야 합니다. EC2 엔드포인트가 정의되어 있지 않으면 연결된 EBS 볼륨을 표시하는 호출이 실패하고 이에 따라 Systems Manager 명령이 실패합니다.
   - **com.amazonaws.region.ssmmessages**: 이 엔드포인트는 Session Manager를 사용하여 보안 데이터 채널을 통해 인스턴스에 연결하는 경우에만 필요합니다. 자세한 내용은 AWS Systems Manager Session Manager 및 참조: ec2messages, ssmmessages 및 기타 API 호출 단원을 참조하십시오.

5. 게이트웨이 엔드포인트 생성의 단계에 따라 Amazon S3에 대한 다음 게이트웨이 엔드포인트를 생성할 수도 있습니다.
   1. **com.amazonaws.region.s3**: Systems Manager는 이 엔드포인트를 사용하여 SSM 에이전트를 업데이트하고 S3 버킷 저장을 선택한 출력 로그 업로드, 버킷에 저장한 스크립트 또는 기타 파일 검색 등의 작업에 사용합니다.
!-->

#### IAM 역할 생성 및 EC2에 할당

#### 이 과정이 무슨 과정이지
1. [Systems Manager 콘솔](https://console.aws.amazon.com/systems-manager/)로 이동합니다.
2. 왼쪽 메뉴에서 **Managed Instances** 를 선택합니다. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)
   * 해당 환경에서 사용되는 인스턴스는 Amazon Linux AMI 2017.09입니다. 이 버전의 [운영체제가 지원하며](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) 사전에 [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html)를 기본으로 설치한 버전입니다.

#### IAM 역할 생성: AWS Systems Manager가 관리할 인스턴스가 사용할 프로파일을 생성합니다.
   1. [IAM console](https://console.aws.amazon.com/iam/)로 이동합니다.
   2. 왼쪽 메뉴중 **Roles**를 클릭합니다.
   3. **Create role**를 클릭합니다.
   4. **Select type of trusted entity** 섹션에서, **AWS service**를 클릭합니다.
   5. 그리고 **Choose the service that will use this role** 섹션에서, 첫번째 선택지인 **EC2**(EC2 Allows EC2 instances to call AWS services on your behalf)를 선택합니다. 그리고 **Next Permission**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-agent.png)

  
1.  **Attached permissions policy** 아래, `AmazonEC2RoleforSSM`을 검색하여 선택합니다. 그리고 **Next: Tags**를 클릭합니다.
 ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2.png)

1. **Next Review**를 클릭합니다.

  
1. **Review** 섹션에서는:
   1. **Role name**을 입력합니다: `ManagedInstancesRole`.
   1. 필요하다면 **Role description**도 입력합니다.
   1. **Create role**를 선택합니다.

#### EC2에 IAM 역할 연결: 방금 생성한 ManagedInstancesRole을 Systems Manager로 관리하려는 인스턴스에 연결합니다.
   1. [EC2 Console](https://console.aws.amazon.com/ec2/)로 이동한 후 **Instances**를 클릭합니다.
   2. IAM role를 연결하려는 인스턴스를 클릭한 후. 상단의 **Actions**, **Instance Settings**, 그리고 **Attach/Replace IAM Role**를 클릭합니다. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach.png)
   3. **Attach/Replace IAM Role**의, `ManagedInstancesRole`를 검색한 뒤 리스트의 해당 role을 선택한 후 **Apply**를 누릅니다.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach-select.png)
   1.  **Systems Manager**로 관리하려는 다른 인스턴스에도 **ManagedInstancesRole** role을 연결합니다.

1. [Systems Manager console](https://console.aws.amazon.com/systems-manager/)로 간 다음, 메뉴의 **Managed Instances**를 클릭합니다. 인스턴스가 목록에 나타날 때까지 주기적으로 **Managed Instances**를 선택하십시오. 몇 분 이 지나야 인스턴스가 **Managed Instances** 목록에 채워집니다.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)

2. 최종적으로 Managed Instance에 등록한 인스턴스를 볼 수 있습니다. 
  ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-agent-fin.png)   

{{% notice tip %}}
AWS Systems Manager는 인프라 가시성 및 제어를 위해 여러 기능을 제공하는 만큼, AWS Systems Manager에 접근하는 사용자를 제한하고 사용자 별 권한을 구분할 필요가 있습니다. 다음 문서에서 [IAM 사용자 및 그룹을 생성하고 권한을 부여](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-access-user.html)하는 방법을 알아봅니다. 
{{% /notice %}}



