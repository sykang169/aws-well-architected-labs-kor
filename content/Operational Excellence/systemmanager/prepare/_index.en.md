---
title: "Prepare"
chapter: false
pre: "<b>1. </b>"
weight: 51
---


{{% notice note %}}
you need to create a VPC endpoint for AWS Systems Manager, create an IAM role, and assign it to EC2.
{{% /notice%}}


### 1. Generate VPC Endpoint
In the lab environment, EC2 is located in the private subnet. In this lab, we will configure AWS Systems Manager to connect privately through a [VPC endpoint](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-endpoints.html) without public IP.

1. Go to the AWS console, Search VPC or click this link:[VPC](https://console.aws.amazon.com/vpc). And click **endpoint** on left top. Click **Create endpoint** button.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-create.png)
1. in **Service category**, click **AWS Service** and search **EC2** in **Service Name** search bar. Select `com.amazonaws.<region>.ec2` and scroll down, click **Create endpoint** button.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-endpoint-select.png)
2. Select **VPC**. Search and click `WellArchitectedLabsStack/VPC` which generate lab setup. **Subnets** select checkbox `ap-northeast-2b` and `ap-northeast-2b`, check all **PrivateSubnet** each AZ.
   ![/images/war-operationalexcellence/ssm-agent-vpc.png](/images/war-operationalexcellence/ssm-agent-vpc.png)
3. Select **Security Group**. Select **Description** value is `WellArchitectedLabsStack/ASG/InstanceSecurityGroup` which for EC2 instance. 
   ![/images/war-operationalexcellence/ssm-agent-sg.png](/images/war-operationalexcellence/ssm-agent-sg.png)
4. Same way search **SSM**, Select `com.amazonaws.< region >.ssm`. 
5. The final created endpoint should have at least 2 endpoints, ec2 and ssm, as shown below.
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
1. Open to the [Systems Manager Console](https://console.aws.amazon.com/systems-manager/). For reference, the EC2 instance for the practice is Amazon Linux AMI 2017.09, and since SSM agent is installed by default, installing the agent on the instance is omitted.
2. Left menu, Click **Managed Instances**.
   * Before you create an IAM role and assign it to EC2, you can see that the instances managed by Systems Manager are not yet looked up. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)
<!--
   * 해당 환경에서 사용되는 인스턴스는 Amazon Linux AMI 2017.09입니다. 이 버전의 [운영체제가 지원하며](https://docs.aws.amazon.com/systems-manager/latest/userguide/patch-manager-supported-oses.html) 사전에 [SSM Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html)를 기본으로 설치한 버전입니다.
!-->

#### 2) Create an IAM role: AWS Systems Manager creates a profile to be used by instances to be managed
   1. Go to [IAM console](https://console.aws.amazon.com/iam/).
   2. In left menu, click **Roles**.
   3. Click **Create role**.
   4. Section in **Select type of trusted entity**, Click **AWS service**.
   5. And Section **Choose the service that will use this role**, Click **EC2**(EC2 Allows EC2 instances to call AWS services on your behalf). And Click **Next Permission** Button.
   ![/images/war-operationalexcellence/ssm-agent.png](/images/war-operationalexcellence/ssm-agent.png)

  
1. under **Attached permissions policy** , search `AmazonEC2RoleforSSM` and select. and click **Next: Tags**.
 ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2.png)

1. Click **Next Review** button.

  
1. **Review** Selection:
   1. type **Role name**: `ManagedInstancesRole`.
   1. if you need type **Role description**.
   1. Click **Create role**.

#### 3) Attach IAM to EC2
Creating an IAM role to attach to the EC2 instance that you want to manage with AWS Systems Manager. Attach the ManagedInstancesRole you just created to the instance you want to manage with Systems Manager. Target is 2 EC2 instance whitch name **WellArchitectedLabsStack/ASG**, one **Bastion Host**.
   1. Go to [EC2 Console](https://console.aws.amazon.com/ec2/), Click **Instances**.
   2. Click instance to attach IAM role, Click top menu button **Actions**, **Instance Settings**, and **Attach/Replace IAM Role**. 
    ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach.png)
   3. Search `ManagedInstancesRole` of **Attach/Replace IAM Role**, select role and click **Apply**.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-ec2-attach-select.png)
   1.  Attach **ManagedInstancesRole** role to other instance which managed from **Systems Manager**.

#### 4) Managed Instance reconfirm
1. Go to [Systems Manager console](https://console.aws.amazon.com/systems-manager/), click **Managed Instances** in menu. Select **Managed Instances** periodically until the instance appears in the list. It may take a few minutes for the instance to appear in the **Managed Instances** list.
   ![/images/war-operationalexcellence/ssm-iam-ec2.png](/images/war-operationalexcellence/ssm-iam-managed-instance.png)

2. Finally, you can see the instances registered with the Managed Instance.
  ![/images/war-operationalexcellence/ssm-agent-fin.png](/images/war-operationalexcellence/ssm-agent-fin.png)   

 

