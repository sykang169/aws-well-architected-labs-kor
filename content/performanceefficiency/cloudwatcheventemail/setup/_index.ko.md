---
title: "사용자 경보 설정"
weight: 321
pre: "<b>1. </b>"
---

### CloudWatch 경보, 경보 생성을
---
CloudFormation에서 생성한 WellArchitectedFrameworkLabsStack에서 생성된 인스턴스의 CPU사용량과 갯수를 측정 할 것입니다.
 
CloudWatch 콘솔 가기 : https://console.aws.amazon.com/cloudwatch/ 

1. 왼쪽 탐생착에서 경보와 경보 생성을 선택합니다. 
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm.png#medium)

1. 그래프의 지표 선택을 선택합니다.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-metric.png#medium)

1. EC2별 CPU사용율을 선택하기위해 검색창에 이전에 복사한 ASGName를 입력한 후 검색하고 `EC2 > By Auto Scaling group`를 선택합니다.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-asg.png#medium)

1. Metric이 **CPUUtilization**인 항목을 찾아 체크박스를 체크한 후 **Select Metric**버튼을 누릅니다.     
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-cpu.png#medium)

1. **지표 및 조건 지정** 설정을 진행하겠습니다. **지표**는 백분율을 이용하여 CPU가 90%이상 사용될 경우 경보를 생성할 예정입니다. 그래프의 **통계** 항목을 **p90**으로 변경합니다. 실제 사용하실 경우 다양항 측정기준이 있으니 원하시는 항목을 선택하시면 됩니다. **기간**은 **1분**을 선택합니다. 1분마다 항목을 업데이트합니다.
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-setting.png#medium)

1.  **조건**의 입계값 유형은 **정적**으로, **보다 큼**를 선택 한 후 **...보다**에 95를 입력합니다. CPU사용율의 백분율이 95%이상 올라갈 경우 경보이 생성됩니다.
    ![CloudwatchAlarm](/images/war/cloudwatch-percent.png#medium)

1. 이제 하단의 **다음**을 선택합니다.

1. 이제 작업구성입니다. 기존에 생성되어있는 SNS topic을 연결할 수도 있습니다. 여기선 새로운 SNS topic을 생성하겠습니다. **경보 상태 트리거**의 **경보 상태**를 선택하고 **SNS 주제 선택**에서 **새 주제 생성**라디오 박스를 선택합니다. 그리고 **새 주제 생성**에 `Default_CloudWatch_Alarms_Topic`, **Email Endpoint**에 본인의 Email을 입력한 후 **Create topic** 버튼을 클릭합니다. 
    ![CloudwatchAlarm](/images/war/cloudwatch-create-topic.png#medium)
1. **다음** 버튼을 클릭합니다.
1. 마지막 이름 및 설명 추가에 아래와 같이 입력합니다.
    - **Alarm name** : `CloudWatch-CPU-Alarm`
    - **Alarm description - optional** : `for WAR workshop`
    ![CloudwatchAlarm](/images/war/cloudwatch-alarm-fin.png#medium)

1. ***경보생성 버튼**을 눌러 생성을 완료합니다. 
1. 이제 기본적인 셋팅이 완료되었습니다. 

[이제 EC2 Instance의 CPU사용율이 올라가면 어떤 변화가 있는지 확인해 보겠습니다.](/performanceefficiency/cloudwatcheventemail/snstopic)
 
