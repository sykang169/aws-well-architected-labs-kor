---
title: "사용자 대시보드 설정"
weight: 312
pre: "<b>2. </b>"
---

### CloudWatch 사용자 대시보드 만들기
---
CloudFormation에서 생성한 WellArchitectedFrameworkLabsStack에서 생성된 인스턴스의 CPU사용량과 갯수를 측정 할 것입니다. 

1. 먼저 WellArchitectedFrameworkLabsStack의 Auto scaling group이 생성한 인스턴스의 CPU Utilization을 가져오기 위해 Auto scaling group의 이름이 필요하며 Load Balancer에 연결된 EC2의 갯수를 확인하기 위해선 Application Load Balancer의 이름이 필요합니다.

    CloudFormation 콘솔로 가기 : https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2

1. Output의 `ASGName`은 Auto scaling group의 이름입니다. `ALBName`는 Application Load Balancer의 이름입니다. 
    CloudFormation 콘솔에서 `MasterAccountStack`을 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-stack.png#medium)

    상단 탭의 Output을 선택한 후 `ASGName`과 `ALBName`의 값을 복사한 후 어딘가 적어놓습니다.   
    ![CloudwatchDashboard](/images/war/cloudwatch-stack-output.png#medium)

    이제 CloudWatch에서 대시보드를 생성할 것입니다.
    CloudWatch 콜솔로 가기 : https://us-west-2.console.aws.amazon.com/cloudwatch/home?region=us-west-2

1. 오른쪽 상단의 **Dashboards**를 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-dashboard.png#medium)

1. **Create Dashboard** 버튼을 클릭합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-createdashboard.png#medium)
 
1. Create new dashboard창의 dashboard name에 `warworkshop-default`를 입력하고 **Create dashboard**버튼을 클릭하여 기본 대쉬보드를 생성합니다.
    ![CloudwatchDashboard](/images/war/cloudwatch-create-fin.png#medium)

1. 이제 생성한 대시보드에서 EC2의 CPU사용울을 볼 수 있는 위젯을 추가할 것입니다. 시간의 흐름에 따른 CPU 사용율를 알아보기 쉽도록 라인형 그래프를 선택하고 **Configure**를 클릭합니다.
    ![CloudwatchDashboard](/images/war/cloudwatch-detail.png#medium)

1. All metrics의 검색창에 이전에 복사해 놓은 Output의 ASGName의 값을 붙여넣습니다. 그리고 엔터를 누른 후 **EC2 > By Auto Scaling Group**를 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-metric.png#medium)

1. 측정가능한 여러 Metric값이 나옵니다. 추후 필요한 값이 있다면 선택하셔서 확인하실 수 있습니다. 지금은 중 Metric Name이 **CPUUtilization**를 것을 선택합니다. 그리고 **Create Widget**버튼을 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-cpuutilization.png#medium)

1. 대시보드 창에 CPUUtilization이 추가된것을 볼 수 있습니다. 이제 EC2의 instance 갯수를 확인하기위한 위젯을 추가해보도록 하겠습니다. 상단의 Add widget버튼을 클릭합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-widget.png#medium)

1. EC2 instance의 갯수를 죽각적으로 알아보기 쉽도록 **Number** 타입를 사용하도록 하겠습니다. **Number** 타입을 선택한 후 Configure 버튼을 클릭합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-metric-widget-select.png#medium)

1. All metrics의 검색창에 이전에 복사해 놓은 Output의 ALBName 값을 붙여넣습니다. 그리고 엔터를 누른 후 Application Load Balancer 별, Target Group단위의 값을 측정하기 위해 **ApplicationELB > Per AppELB, per TG Metrics**를 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-alb.png#medium)

1. 다양한 메트릭들이 나옵니다. 이 중 `HealthyHostCount` 값을 선택한 후 하단의 **Create widget**을 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-healthy.png#medium)

1. 이제 CPUUtilization과 Target Group에 생성된 Instance의 갯수를 확인할 수 있는 대시보드 생성이 완료 되었습니다. 현재는 매우 낮은 CPU사용율과 2개의 인스턴스가 띄워져 있는 것을 확인할 수 있습니다. 상단의 Save dashboard를 눌러 대시보드를 저장합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-widget-fin.png#medium)


[이제 CPU사용율의 변화를 사용자가 즉시 알 수 있도록 Cloudwatch 경보를 생성하겠습니다.](/performanceefficiency/cloudwatcheventemail)
 
