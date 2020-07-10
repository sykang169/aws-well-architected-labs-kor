---
title: "IAM access 설정"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---

{{% notice info %}}
**참고** :이 작업을 수행하려면 루트 계정 자격 증명을 사용하여 마스터 계정에 로그인해야합니다.
{{% /notice %}}

루트 자격 증명을 사용하지 않고 청구 정보에 접근하려면 IAM 액세스를 활성화해야합니다. 이를 통해 루트가 아닌 다른 사용자가 마스터 계정의 청구 정보에 액세스 할 수 있습니다. 이 접근 방식은 각 사용자에게 개별 로그인 정보를 제공하며 각 사용자에게 계정 작업에 필요한 권한만 부여 할 수 있습니다. 예를 들어 재무 팀에 청구 정보에만 액세스 권한을 부여하고 계정의 다른 리소스는 접근 할 수 없도록 할 수 있습니다.

1. 마스터계정의 루트사용자로 로그인하고 오른쪽 상단의 계정이름을 클릭한 다음 메뉴에서 **My Account** 클릭하세요.:
![Images/AWSAcct4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSAcct4.png)

2. **IAM User and Role Access to Billing Information**까지 아래로 스크롤 한 다음 **Edit**을 클릭합니다.
![Images/AWSAcct5.png](/Cost/100_1_AWS_Account_Setup/Images/AWSAcct5.png)

3. **Activate IAM Access**를 선택한 다음 **Update**를 클릭하세요. 
![Images/AWSAcct6.png](/Cost/100_1_AWS_Account_Setup/Images/AWSAcct6.png)

4. **IAM user/role access to billing information is activated** 활성화되어있는지 확인하세요. :
![Images/AWSAcct7.png](/Cost/100_1_AWS_Account_Setup/Images/AWSAcct7.png)

이제 루트가 아닌 사용자에게 IAM 정책을 통해 청구 정보에 대한 액세스를 제공 할 수 있습니다.


{{% notice note %}}
**NOTE:** 계속 진행하기 전에 루트사용자를 로그아웃하세요.
{{% /notice%}}