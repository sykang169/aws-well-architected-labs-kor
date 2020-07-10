---
title: "EC2인스턴스에 CloudWatch IAM role 연결하기"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

1. 이제 이전 스텝에서 생성한 IAM Role created 기존의 EC2인스턴스와 연결할 것입니다. **Amazon EC2 Dashboard** 로 가겠습니다..
![Images/MemInstall01.png](/cost/200_aws_resource_optimization/Images/MemInstall01.png)

2. 왼쪽 메뉴에서 **Instances**를 클릭하세요.
![Images/MemInstall02.png](/cost/200_aws_resource_optimization/Images/MemInstall02.png)

4. 검색창에 `WellArchitectedLabsStack`을 입력하여 오토스캐일링 그룹이 자동으로 생성한 2개의 인스턴스를 찾습니다. 그리고 하나를 선택한수 상단의 **Action**버튼을 클릭합니다. 그리고 **Instance Settings** -> **Attach/Replace IAM Role** 을 아래 그림과 같이 순서대로 클릭합니다.
![/images/war-cost/2cost-cloudwatch-agent.png](/images/war-cost/cost-cloudwatch-agent2.png)

5. IAM role의 드랍 박스 버튼을 클릭하여 이전에 생성한 `CloudWatchAgentServerRole` 역할을 검색 한 후 선택하고 **Apply**를 클릭합니다..
![Images/MemInstall04.png](/cost/200_aws_resource_optimization/Images/MemInstall04.png)

6. 이제 EC2인스턴스에 *CloudWatchAgentServerRole*이 성공적으로 연결되었습니다.
![Images/MemInstall05.png](/cost/200_aws_resource_optimization/Images/MemInstall05.png)

7. 인스턴스를 클릭하면 연결된 IAM role을 확인 하실 수 있습니다.
![/images/war-cost/cost-cloudwatch-agent.png](/images/war-cost/cost-cloudwatch-agent-check.png)

