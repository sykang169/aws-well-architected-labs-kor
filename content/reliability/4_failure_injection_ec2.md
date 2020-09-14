---
title: "EC2 장애 주입을 사용하여 안정성 테스트"
menutitle: "EC2 장애 주입"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>4. </b>"
weight: 4
---

### 4.1 EC2 장애 주입

1. EC2 콘솔로 이동하고 왼쪽 창에서 **Instances**를 클릭합니다: <http://console.aws.amazon.com/ec2>.

1.  WellArchitectedLabsStack/ASG로 시작하는 이름을 가진 2개의 EC2 인스턴스가 있습니다:
      1. 각각 고유 한 *Instance ID*가 있습니다.
      1. 각 가용 영역 당 하나의 인스턴스가 있습니다.
      1. 모든 인스턴스가 정상입니다.

    ![EC2ShuttingDown](/images/reliability/reliability-ec2-normal.png)

1. 변화를 관찰하기 위해 **Target Groups** 와 **Auto Scaling Groups** 를 별도의 탭에 오픈합니다.

    ![NavToTargetGroupAndScalingGroup](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/NavToTargetGroupAndScalingGroup.png)

1. EC2 인스턴스 중 하나에 장애가 발생시키려면 Cloud9의 터미널에서 VPC ID를 사용하여 아래 스크립트를 실행시킵니다. \<vpc-id\>는 이전에 기록한 VPC ID로 대체합니다.
```bash
./fail_instance.sh <vpc-id>
```
1. EC2 인스턴스의 ID에 대한 참조와 성공 표시기가 포함됩니다. 다음은 Bash 명령의 출력입니다. 해당 인스턴스는 강제로 `CurrentState`가 `shutting-down`이 됩니다.

        $ ./fail_instance.sh vpc-04f8541d10ed81c80
        Terminating i-0710435abc631eab3
        {
            "TerminatingInstances": [
                {
                    "CurrentState": {
                        "Code": 32,
                        "Name": "shutting-down"
                    },
                    "InstanceId": "i-0710435abc631eab3",
                    "PreviousState": {
                        "Code": 16,
                        "Name": "running"
                    }
                }
            ]
        }

1. *미리띄워놓은 EC2 Instances 콘솔*에서 인스턴스가 어떤 상태인지 확인해보겠습니다(또는 [새로운 콘솔 열기](http://console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:))

      * 새로 고침하세요.(참고 : 일반적으로 브라우저를 새로 고치는 것보다 콘솔에서 새로 고침 단추를 사용하는 것이 더 효율적입니다.)

           ![RefreshButton](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/RefreshButton.png)
    
      * 스크립트에서 보고한 인스턴스의 상태를 관찰하십시오. 아래 화면과 같이 인스턴스는 _shutting down_ 되고 궁극적으로 _terminated_ 로 전환됩니다.

        ![EC2ShuttingDown](/images/reliability/reliability-ec2-shuttingdown.png)

### 4.2 EC2 인스턴스 실패에 대한 시스템 응답

서비스가 어떻게 반응하는지보십시오. AWS시스템이 서비스 가용성을 유지하는데 어떻게 도움이되는지 확인하십시오. 비가용성이 있는지 테스트하고 그렇다면 얼마나 오래 사용할 수 있는지 테스트하십시오.

#### 4.2.1 시스템 가용성

서비스 웹 사이트를 여러 번 새로 고칩니다: 웹사이트의 주소는 실습환경셋업에서 생성한 CloudFormation의 `MasterAccount` Stack의 Outputs에서 ALBDNS를 사용하세요.

* 웹 사이트 사용 가능한지 확인. 
* 나머지 EC2 인스턴스가 모든 요청을 처리합니다.
{{% notice info %}}
BastionHost가 떨어질 수도 있습니다. 카오스엔지니어링에서는 이러한 경우도 고려해야하지만 아래 실습내용은 EC2를 다루고 있습니다. 다시 Cloud9에서 다시 명령어를 실행하세요. 
{{% /notice %}}

#### 4.2.2 로드벨런싱

로드 밸런싱은 서비스 요청이 실패한 EC2 인스턴스와 같은 비정상 리소스로 라우팅되지 않도록합니다.

1. 미리 띄워놓은 **Target Groups**으로 이동합니다(또는 새로운 창을 띄우기위해 [이곳을 클릭하세요](http://console.aws.amazon.com/ec2/v2/home?region=us-east-2#TargetGroups:))
     *  **Target Groups**이 여러개인 경우 이름이 Maste-LB로 시작하는 **Load Balancer**가 있는 그룹을 선택하십시오.

1. **Targets** 탭을 클릭하고 다음을 확인하세요.:
      * 그룹의 인스턴스 상태입니다. 로드 밸런서는 정상 인스턴스로만 트래픽을 보냅니다.
      * Auto Scaling이 새 인스턴스를 시작하면 자동으로 **Load Balancer Target Groups**에 추가됩니다.
      * 비정상 인스턴스 인스턴스가 생겼다면 리스트에 새로 추가 된 인스턴스가 생깁니다. 로드 밸런서는 인스턴스 초기화가 완료 될 때까지 트래픽을 전송하지 않습니다. 궁극적으로 정상 상태로 전환 된 다음 트래픽 수신을 시작합니다.
      * 새 인스턴스는 실패한 인스턴스와 동일한 가용 영역에서 시작됩니다. Amazon EC2 Auto Scaling은 사용자가 지정한 모든 가용 영역에서 자동으로 균형을 유지합니다.
        ![TargetGroups](/images/reliability/reliability-ec2-targetgroup.png)    
      

1. 동일한 콘솔에서 이제 **Monitoring** 탭을 클릭하고 **Unhealthy hosts** 및 **Healthy hosts**와 같은 메트릭을 봅니다.
      ![TargetGroupsMonitoring](/images/reliability/reliability-ec2-montoring.png)   
#### 4.2.3 Auto scaling

Autos scaling 은 고객 요구를 충족하는 데 필요한 용량을 확보합니다. 이 서비스의 Auto Scaling은 최소 2 개의 EC2 인스턴스가 실행되도록 하는 간단한 구성입니다. AWS를 사용하면 CPU 또는 네트워크 부하에 대한 더 복잡한 구성도 가능합니다.

1. 이전에 띄워놓은 **Auto Scaling Groups** 콘솔로 갑니다.(또는 [새 콘솔을 띄웁니다.](http://console.aws.amazon.com/ec2/autoscaling/home?region=us-east-2#AutoScalingGroups:))
      * Auto Scaling 그룹이 여러개인 경우 이름이 **MasterAccount-ASG**로 시작하는 그룹을 선택하십시오.

1. **Activity**탭을 클릭하고 스크롤을 내리면 **Activity history**를 볼 수 있습니다:
      * 인스턴스들의 변화 상태와 시간을 확인할 수 있습니다.
          ![AutoScalingGroup](/images/reliability/reliability-ec2-asg.png)   


_Draining_ 을 사용하면 인스턴스에 대한 기존의 진행중인 요청을 완료 할 수 있지만 인스턴스에 새 요청을 보내지 않습니다. [자세히 알아보기](https://aws.amazon.com/blogs/aws/elb-connection-draining-remove-instances-from-service-with-care/).

* __Learn more__: 실습 후 [Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html)그룹에서 **Auto Scaling** 그룹이 설정되고 인스턴스를 배포하는 방법에 대해 자세히 알아보고싶으면 [Dynamic Scaling for Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html)에서 수요에 응답하는 Auto Scaling 설정에 대한 자세한 내용을 참조하십시오.

#### 4.2.4 EC2 장애 주입 - 결론

여러 서버와 Elastic Load Balancing을 배포하면 사용자 트래픽이 정상 서버로 자동 라우팅되므로 가용성 중단없이 서비스가 서버 손실을 겪을 수 있습니다. Amazon Auto Scaling은 고 가용성을 유지하기 위해 비정상 호스트를 제거하고 정상 호스트로 교체합니다.