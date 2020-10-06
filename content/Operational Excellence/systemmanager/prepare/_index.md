---
title: "사전 준비"
chapter: false
pre: "<b>1. </b>"
weight: 51
---


{{% notice note %}}
본 실습을 진행하기 위해서는 AWS Systems Manager가 사용할 VPC 엔드포인트 생성 및 IAM 역할 생성 및 EC2에 할당하는 작업들이 사전에 진행되어야 합니다.
{{% /notice%}}


### 1. VPC 엔드포인트 생성
실습 환경에서는 EC2가 Private Subnet에 위치하고 있습니다. 본 실습에서는 AWS Systems Manager가 퍼블릭 IP 필요 없이 [VPC 엔드포인트](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-endpoints.html)를 통해 비공개로 연결하도록 구성합니다.
1. AWS Services 메뉴의 [VPC](https://console.aws.amazon.com/vpc)로 이동합니다. 그리고 왼쪽 메뉴의 **endpoint**를 클릭합니다. 그리고 **Create endpoint**를 클릭합니다.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-create.png)
<<<<<<< HEAD
1. **Service category**의 **AWS Service**를 클릭하고 **Service Name**의 검색창에 ec2를 검색합니다. 그리고 com.amazonaws.<region>.ec2 을 선택하고 맨 아래 **Create endpoint**를 클릭합니다.
=======
1. **Service category**의 **AWS Service**를 클릭하고 **Service Name**의 검색창에 ec2를 검색합니다. 그리고 `com.amazonaws.<region>.ec2` 을 선택하고 맨 아래 **Create endpoint**를 클릭합니다.
>>>>>>> 10ff751802894533b4d2ed100b73d3961dc3be45
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-select.png)
2. **VPC**를 선택합니다. 실습에서 생성한 `WellArchitectedLabsStack/VPC`를 검색하여 선택합니다. **Subnets**은 `ap-northeast-2b`, `ap-northeast-2b`의 체크박스를 선택하고 모두 **PrivateSubnet**을 선택합니다.
   ![/images/war-operationalexcellence/ssm-agent-vpc.png](/images/war-operationalexcellence/ssm-agent-vpc.png)
3. **Security Group**를 선택합니다. Description에서 EC2인스턴스와 동일한 보안그룹을 선택합니다. 실습환견에서는 `WellArchitectedLabsStack/ASG/InstanceSecurityGroup`을 선택하면 됩니다. 
   ![/images/war-operationalexcellence/ssm-agent-sg.png](/images/war-operationalexcellence/ssm-agent-sg.png)
<<<<<<< HEAD
4. 동일한 방법으로 **SSM**을 검색하여 **com.amazonaws.< region >.ssm**도 선택합니다. 
=======
4. 동일한 방법으로 **SSM**을 검색하여 `com.amazonaws.< region >.ssm`도 선택합니다. 
>>>>>>> 10ff751802894533b4d2ed100b73d3961dc3be45
5. 최종적으로 생성된 엔드포인트는 아래와 같이 ec2와 ssm의 2개의 최소한 엔드포인트가 있어야 합니다. 
   * **com.amazonaws.ap-northeast-2.ec2**
   * **com.amazonaws.ap-northeast-2.ssm** 
   ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-endpoint-fin.png)

<!--
{{% notice tip %}}
필요에 따라 아래의 인터페이스를 생성할 수도 있습니다. 
{{% /notice%}}
   - **com.amazonaws.region.ssm**: Systems Manager 서비스에 대한 엔드포인트
   - **com.amazonaws.region.ec2messages**: Systems Manager에서는 이 엔드포인트를 사용하여 SSM 에이전트에서 Systems Manager 서비스로 호출합니다.
   - **com.amazonaws.region.ec2**: Systems Manager를 사용하여 VSS 지원 스냅샷을 만든 경우, EC2 서비스에 대한 엔드포인트가 있어야 합니다. EC2 엔드포인트가 정의되어 있지 않으면 연결된 EBS 볼륨을 표시하는 호출이 실패하고 이에 따라 Systems Manager 명령이 실패합니다.
   - **com.amazonaws.region.ssmmessages**: 이 엔드포인트는 Session Manager를 사용하여 보안 데이터 채널을 통해 인스턴스에 연결하는 경우에만 필요합니다. 자세한 내용은 AWS Systems Manager Session Manager 및 참조: ec2messages, ssmmessages 및 기타 API 호출 단원을 참조하십시오.

1. 게이트웨이 엔드포인트 생성의 단계에 따라 Amazon S3에 대한 다음 게이트웨이 엔드포인트를 생성할 수도 있습니다.
   1. **com.amazonaws.region.s3**: Systems Manager는 이 엔드포인트를 사용하여 SSM 에이전트를 업데이트하고 S3 버킷 저장을 선택한 출력 로그 업로드, 버킷에 저장한 스크립트 또는 기타 파일 검색 등의 작업에 사용합니다.
!-->

### 2. IAM 역할 생성 및 EC2에 할당

#### 1) Managed Instance 확인
1. [Systems Manager 콘솔](https://console.aws.amazon.com/systems-manager/)로 이동합니다. 참고로 실습용 EC2 인스턴스는 Amazon Linux AMI 2017.09으로, SSM 에이전트가 기본 설치되어 있기 때문에 에이전트를 인스턴스에 설치하는 작업은 생략합니다.
2. 왼쪽 메뉴에서 **Managed Instances** 를 선택합니다. 
   * IAM 역할 생성 및 EC2에 할당하는 작업을 수행하기 전에는 Systems Manager가 관리하는 인스턴스가 아직 조회되지 않음을 확인할 수 있습니다.  
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)
<!--
   * 해당 환경에서 사용되는 인스턴스는 Amazon Linux AMI 2017.09입니다. 이 버전의 [운영체제가 지원하며](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) 사전에 [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html)를 기본으로 설치한 버전입니다.
!-->

#### 2) IAM 역할 생성: AWS Systems Manager가 관리할 인스턴스가 사용할 프로파일을 생성합니다.
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

#### 3) EC2에 IAM 역할 연결
AWS Systems Manager로 관리할 EC2 인스턴스에 연결할 IAM 역할을 생성하여 권한을 부여합니다. 방금 생성한 ManagedInstancesRole을 Systems Manager로 관리하려는 인스턴스에 연결합니다. 인스턴스 이름이 **WellArchitectedLabsStack/ASG**인 2개 인스턴스와 **Bastion Host** 총 3대가 그 대상입니다.
   1. [EC2 Console](https://console.aws.amazon.com/ec2/)로 이동한 후 **Instances**를 클릭합니다.
   2. IAM role를 연결하려는 인스턴스를 클릭한 후. 상단의 **Actions**, **Instance Settings**, 그리고 **Attach/Replace IAM Role**를 클릭합니다. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach.png)
   3. **Attach/Replace IAM Role**의, `ManagedInstancesRole`를 검색한 뒤 리스트의 해당 role을 선택한 후 **Apply**를 누릅니다.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach-select.png)
   1.  **Systems Manager**로 관리하려는 나머지 인스턴스들에도 **ManagedInstancesRole** role을 연결합니다.

#### 4) Managed Instance 재확인
1. [Systems Manager console](https://console.aws.amazon.com/systems-manager/)로 간 다음, 메뉴의 **Managed Instances**를 클릭합니다. 인스턴스가 목록에 나타날 때까지 주기적으로 **Managed Instances**를 선택하십시오. 인스턴스가 **Managed Instances** 목록에서 조회되기까지는 최소 수 분이 소요됩니다. 
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)

2. 최종적으로 Managed Instance에 등록한 인스턴스를 볼 수 있습니다. 
  ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-agent-fin.png)   

{{% notice tip %}}
AWS Systems Manager는 인프라 가시성 및 제어를 위해 여러 기능을 제공하는 만큼, AWS Systems Manager에 접근하는 사용자를 제한하고 사용자 별 권한을 구분할 필요가 있습니다. 다음 문서에서 [IAM 사용자 및 그룹을 생성하고 권한을 부여](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-access-user.html)하는 방법을 알아봅니다. 
{{% /notice %}}



