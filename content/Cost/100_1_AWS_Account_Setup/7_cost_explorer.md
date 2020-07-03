---
title: "AWS Cost Explorer 활성화"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>7. </b>"
weight: 7
---


AWS Cost Explorer는 시간에 따른 AWS 비용 및 사용량을 시각화, 분석 및 관리 할 수 있습니다. 이것은 계쩡에서 활성화 해야 사용 할 수 있습니다. 일단 활성화되면 모든 계정에 대해 활성화되고 IAM 정책을 통해 제어됩니다. 비용 탐색기의 기본 구성은 무료이지만 시간 단위로 사용하도록 설정하면 추가 비용이 발생합니다.- [AWS Cost Management Pricing](https://aws.amazon.com/aws-cost-management/pricing/).

1. 권한을 가진 IAM 사용자를 콘솔에 로그인하고 **Billing** 으로 갑니다:
![Images/AWSExplorer0.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer0.png)

2. 왼쪽 메뉴에서 **Cost Explorer**를 선택합니다:
![Images/AWSExplorer1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer1.png)

3. **Enable Cost Explorer**를 클릭합니다:
![Images/AWSExplorer2.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer2.png)

4. You will receive notification that Cost Explorer has been enabled, and data will be populated:
4. 이제 Cost Explorer가 활성화됬다는 공지를 받을 것입니다. 그리고 데이터가 나타납니다.
![Images/AWSExplorer3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer3.png)

5. 24시간 뒤 **Cost Explorer**롤 갑니다:
![Images/AWSExplorer4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer4.png)

6. 오른쪽 상단의 **Settings**를 클릭합니다:
![Images/AWSExplorer5.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer5.png)

7. **Hourly and Resource Level Data**를 선택하고, **Save**를 클릭합니다:
![Images/AWSExplorer6.png](/Cost/100_1_AWS_Account_Setup/Images/AWSExplorer6.png)

{{% notice note %}}
실행하는 리소스 수에 따라 비용이 발생합니다.
{{% /notice %}}

