---
title: "이메일 확인 및 전화번호 등록"
weight: 322
pre: "<b>2. </b>"
---

### SNS e-mail Confirm
---
SNS topic에서 연결한 email은 해당 계정에서 재승인을 해야 올바른 경고를 받을 수 있습니다. 이전 sns 셋팅할 때 입력한 email의 받은 편지함에서 `ÀWS Notification`이 보낸 메일을 찾으세요. 
   ![CloudwatchAlarm](/images/war/cloudwatch-confirm.png#medium)

그리고 **Confirm subription**을 누르세요. 아래와 같은 화면이 나타나면서 구독이 완료됩니다. 
   ![CloudwatchAlarm](/images/war/cloudwatch-confirm-fin.png#medium)

이제 추가로 알람 발생시 휴대폰 문자를 보낼 수 있도록 SNS topic에 휴대폰 번호를 추가해보겠습니다. 

Amazon SNS 콘솔 가기 : https://console.aws.amazon.com/sns/ 

1. 왼쪽 메뉴의 Topics을 선택합니다.  
    ![CloudwatchAlarm](/images/war/sns-topics.png)

1. 경보를 생성하면서 같이만든 SNS topic인 `Default_CloudWatchAlarms_Topic`을 선택합니다.
    ![CloudwatchAlarm](/images/war/sns-topics-select.png#medium)

1. 스크롤을 내리면 **구독**을 보면 알람을 생성할 때 등록한 email을 볼 수 있습니다. 이곳에서 **구독 생성**을 선택해 새로운 구독자를 추가할 수 있습니다. 
    ![CloudwatchAlarm](/images/war/sns-topics-create-sub.png#medium)

1. 구독생성의 **Protocol**을 SMS로 선택합니다. (이곳에서 다양한 프로토콜을 사용 할 수 있습니다.) 그리고 Endpoint에 본인의 휴대폰 번호를 입력합니다. (ex+821012345678) 그리고 하단의 구독 생성버튼을 클릭합니다. 
    ![CloudwatchAlarm](/images/war/sns-topics-create-sub-fin.png#medium)

1. 경보 알람에 나의 휴대폰 번호 등록도 완료하였습니다. 이전의 Topics메뉴에서 `Default_CloudWatchAlarms_Topic`를 선택하면 해당 토픽과 연결된 email과 휴대폰 정보를 볼 수 있습니다. 

[이제 EC2 Instance의 CPU사용율이 올라가면 어떤 변화가 있는지 확인해 보겠습니다.](/ko/performanceefficiency/cloudwatcheventemail/ec2)
 
