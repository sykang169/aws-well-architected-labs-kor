---
title: "AZ 장애 주입을 사용하여 안정성 테스트"
menutitle: "AZ 장애 주입"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>4. </b>"
weight: 4
---

### 6.1 AZ 장애 주입

이 장애 주입은 서비스에서 사용하는 두가지 AWS 가용영역(AZ)중 하나가 문제가 생겼을 경우를 시뮬레이션합니다. AWS 가용영역은 고 가용성 애플리케이션을 구축하는 데 도움이되는 강력한 도구입니다. 애플리케이션이 AZ로 분할되면 기업은 낙뢰, 토네이도, 지진 등과 같은 문제로부터 격리되고 보호됩니다.

1. AWS Console <http://console.aws.amazon.com/rds>의 RDS 대쉬보드에서 _primary_ DB 인스턴스가 어느 가용 영역에 있는지 확인하세요.
      * 이전에 **RDS 장애주입 테스트**를 실행 한 경우 콘솔에 _primary_ 및 _standby_ 인스턴스의 AZ가 스왑 된 것으로 표시 될 때까지 기다려야합니다.
      * A good way to run the AZ failure injection is first in an AZ _other_ than this - we'll call this **Scenario 1**
      * AZ 장애 주입을 실행하는 좋은 방법은 다른 AZ에서 먼저 실행하는 것입니다. 이 시나리오를 **시나리오 1**이라고합니다.
      * 그런 다음 AWS RDS 기본 DB 인스턴스와 동일한 AZ에서 다시 시도합니다.이 시나리오를 **시나리오 2**라고합니다.
      * 이러한 방식으로 3 개의 AZ 중 2 개를 제거하는 것은 가능성이 낮은 사용 사례이지만 극한 상황에서도 AWS 시스템이 서비스 무결성을 유지하기 위해 어떻게 작동하는지 보여줍니다.
      * 그리고 이러한 방식으로 실행하면 두 가지 다른 시나리오에서 영향과 대응을 알 수 있습니다.
1. AZ의 실패를 시뮬레이션하려면 서비스에서 사용하는 가용 영역 (`ap-northeast-2a`, `ap-northeast-2b` 또는 `ap-northeast-2c`) 중 하나를 `<az>`로 선택합니다.
      * **시나리오 1**의 경우 RDS DB 인스턴스에 대해 기본도 보조도 아닌 AZ를 선택합니다. 다음 RDS 콘솔이 주어지면 `ap-northeast-2c`를 선택합니다.
      * **시나리오 2**의 경우 RDS DB 인스턴스의 기본 AZ를 선택합니다. 다음 RDS 콘솔이 주어지면 `ap-northeast-2b`를 선택합니다.
      ![DBConfigurationShort](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/DBConfigurationShort.png)

1. 아래 명령어를 입력합니다. VPC ID는 이전에 기록한 `<vpc-id>`를 사용합니다.

```bash
./failover_az.sh <az> <vpc-id>
```

1. RDS 장애 조치가 시작되었는지 확인합니다.(AWS RDS _primary_ DB 인스턴스가 포함 된 AZ를 선택한 경우).

### 6.2 AZ 장애에 대한 시스템 응답

서비스가 어떻게 반응하는지보십시오. AWS 시스템이 서비스 가용성을 유지하는 데 어떻게 도움이되는지 확인하십시오. 비가용성이 있는지 테스트하고 그렇다면 얼마나 오래 사용할 수 있는지 테스트하십시오.

#### 6.2.1 시스템 가용성

서비스 웹 사이트를 여러 번 새로 고칩니다.

* **시나리오 1** : AWS RDS 기본 DB 인스턴스가 포함되지 않은 AZ를 선택한 경우 중단없는 가용성이 표시되어야합니다.
* **시나리오 2**: AWS RDS 기본 DB 인스턴스가 포함 된 AZ를 선택한 경우 RDS 장애 주입 테스트에서 확인한 것과 유사한 가용성 손실이 발생합니다.

#### 6.2.2 시나리오 1 - 로드 밸런서 및 웹 서버 계층

이 시나리오는 아키텍처에서 AZ 당 하나의 EC2 서버 만 있기 때문에 EC2 장애 주입 테스트와 유사합니다. 해당 테스트와 동일한 대쉬보드와 화면을 관찰해보세요.

* [EC2 Instances](http://console.aws.amazon.com/ec2/v2/home?region=ap-northeast-2#Instances:)
* Load Balancer [Target group](http://console.aws.amazon.com/ec2/v2/home?region=ap-northeast-2#TargetGroups:)
* [Auto Scaling Groups](http://console.aws.amazon.com/ec2/autoscaling/home?region=ap-northeast-2#AutoScalingGroups:)

관찰하게 될 EC2 장애 주입과의 차이점은 Auto Scaling이 나머지 AZ에서 요청 된 2 개의 EC2 인스턴스의 균형을 맞추려고 시도 할 때 이미 EC2 인스턴스가있는 AZ에서 교체 EC2 인스턴스를 가져온다는 것입니다.

#### 6.2.3 시나리오 2 - 로드밸런서, 웹 서버와 데이터 계층

이 시나리오는 EC2 장애주입과 RDS 장애 주입조합의 유사합니다. EC2 관련 화면 외에도 [Amazon RDS console](http://console.aws.amazon.com/rds)을보고 DB 화면으로 이동하여 다음 탭을 확인합니다.

* Configuration
* Monitoring
* Logs & Events

#### 6.2.4 AZ 장애 주입 - 결론

**시나리오 1**과 EC2 장애 테스트, 그리고 **시나리오 2**와 RDS 장애 테스트 간의 유사성은 AZ 장애가 시스템에 미치는 영향을 잘 보여줍니다. 해당 AZ의 리소스는 가용성이 없거나 제한됩니다. 그러나 가용 영역 간의 강력한 파티셔닝 및 격리를 통해 다른 AZ의 리소스는 필요한 기능을 계속해서 서비스에 제공합니다. **시나리오 1**은 하나의 AZ에서로드 밸런서 및 웹 서버 기능의 손실만 초래하는 반면 **시나리오 2**는 데이터 계층의 손실을 추가합니다. 시스템의 모든 계층이 여러 AZ에 있도록함으로써 장애에 대해 복원력이있는 분할 된 아키텍처를 생성합니다.

#### 6.2.5 AZ 장애 복구

이 단계는 선택 사항입니다. AZ를 다시 정상으로 돌리려면 아래 내용을 수행하세요.

1. [Auto Scaling Group console](http://console.aws.amazon.com/ec2/autoscaling/home?region=ap-northeast-2#AutoScalingGroups:)으로 갑니다.
1. **MasterAccount-ASG**로 시작하는 Auto Scaling Group를 선택합니다.
1. Actions >> Edit
1. **Subnet**에 **WellArchitectedLabsStack/VPC/PrivateSubnet**중 없는 것을 추가합니다.(총 2개, PrivateSubnet1, PrivateSubnet2 ) 그리고 **Save**을 누릅니다.
1. [Network ACL console](https://ap-northeast-2.console.aws.amazon.com/vpc/home?region=ap-northeast-2#acls:)로 갑니다.
1. **WellArchitectedLabsStack/VPC**의 NACL을 살펴봅니다.
1.  **Default**가 아닌 값을 찾습니다.
      1. NACL을 선택합니다.
      1. **Actions** >> **Edit subnet associations**
      1. 모든 선택을 해제하고 **Edit**를 클릭합니다.
      1. **Actions** >> **Delete network ACL**

* Auto Scaling이 가용성 영역에서 EC2 서비스를 재배포하는 방법을 확인합니다.