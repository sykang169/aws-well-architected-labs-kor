---
title: "장애 주입 준비"
menutitle: "장애 주입 준비"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

**장애 주입** (**chaos testing**라고도 함)은 워크로드의 복원력을 검증하고 이해하는 효과적이고 필수적인 방법이며 [AWS Well-Architected Reliability Pillar](https://aws.amazon.com/architecture/well-architected/)의 권장 사례입니다. 여기에서 다양한 장애 시나리오를 시작하고 시스템이 어떻게 반응하는지 평가합니다.

### 준비

테스트 하기 전에 다음을 준비하세요. 

1. **서울**리전에서 진행됩니다.
      * AWS 콘솔을 사용하여 테스트의 영향을 평가할 것입니다.
      * 이 실습 전체에서 귀하가 **서울** 지역에 있는지 확인하십시오.

1. VPC ID 가져오기
      * VPC (Amazon Virtual Private Cloud)는 서비스에 대한 리소스를 배포 한 AWS 클라우드의 논리적으로 격리 된 섹션입니다.
      * 테스트를 위해서는 VPC의 **VPC ID**를 알아야합니다.
      * VPC 관리 콘솔로 이동합니다.: <https://console.aws.amazon.com/vpc>
      * 왼쪽 패널에서 **Your VPCs**를 클릭합니다.
      * 1 - VPC리스트 중 **WellArchitectedLabsStack/VPC**체크박스를 클릭합니다.
      * 2 - **VPC ID**를 복사합니다.

      ![setvpc](/images/reliability/reliability-vpc.png)      

     * 저장한 VPC-ID는 이후 나올 실습중 `<vpc-id>` 명령에 복사하여 사용하시면 됩니다.

1. 장애 주입에 사용될 스크립트를 Cloud9으로 옮기겠습니다. 아래파일을 다운받습니다.         
      * [fail_az.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/fail_az.sh)
      * [fail_instance.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/fail_instance.sh)
      * [failover_rds.sh](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Code/FailureSimulations/bash/failover_rds.sh)
1. 이제 Cloud9을 실행시킵니다([AWS Cloud9 Console로 가기](https://ap-northeast-2.console.aws.amazon.com/cloud9/home?region=ap-northeast-2#)). 콘솔로 이동하여 실습환경셋업에서 생성한 `WellArchitectedWorkshop's Cloud9`을 선택합니다.
      ![](/images/reliability/reliability-cloud9-start.png)      
1. 다운로드 받은 세 파일을 Cloud9에 업로드합니다. 상단의 메뉴에서 **File** -> **Upload Local Files**...을 클릭하고 업로드할 파일을 선택합니다.
      ![](/images/reliability/reliability-cloud9-upload.png)      



1. 업로드가 완료되면 업로드된 파일을 Cloud9에서 확인할 수 있습니다. 
      ![](/images/reliability/reliability-cloud9-fin.png)      

1. 파일에 실행권한을 부여합니다. CLoud9의 터미널에 아래와 같이 입력합니다. 
```bash
  sudo chmod 755 ./fail_instance.sh
  sudo chmod 755 ./fail_az.sh
  sudo chmod 755 ./failover_rds.sh
```

1. 아재 Cloud9에서 Json을 다루기위해 `jq`가 설치되어 있는지 확인합니다.(1.4이상의 버전이 필요)

```bash
  $ jq --version
  jq-1.5-1-a5b5cbe
```

1. 만약 설치되어있지 않다면 CLoud9의 터미널에 아래와 같이 입력합니다.
```bash
sudo yum install jq -y
```

1. 다시 jq --version 을 입력하여 위와 같이 나오면 준비 완료입니다. 


    | |
    |:---:|
    |**Availability Zones** (**AZ**s)은 리전 내의 격리 된 리소스 집합으로, 각각 별도의 시설에있는 중복 전원, 네트워킹 및 연결 기능이 있습니다. 각 가용 영역은 격리되어 있지만 한 리전의 가용 영역은 지연 시간이 짧은 링크를 통해 연결됩니다. AWS는 높은 복원성을 위해 각 AWS 리전 내의 여러 가용 영역에 인스턴스를 배치하고 데이터를 저장할 수있는 유연성을 제공합니다.|
    |*__Learn more__: 실습 후 지역 및 가용성 영역에 대한 [백서를 참조하십시오.](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/global-infrastructure.html) on regions and availability zones*|
