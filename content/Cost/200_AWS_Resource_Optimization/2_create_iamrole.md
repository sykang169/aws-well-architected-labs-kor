---
title: "AMAZON CLOUDWATCH AGENT가 사용할 IAM 역할 만들기"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---

AAWS 리소스를 사용하려면 권한이 필요합니다. 이제 에이전트가 CloudWatch에 지표를 작성하는 데 필요한 권한을 부여하기 위해 IAM 역할을 생성합니다. Amazon은 해당 용도로만 사용 할 수 있는 *CloudWatchAgentServerPolicy* 및 *CloudWatchAgentAdminPolicy*라는 두 개의 기본 정책을 만들었습니다.


1. **AWS Management Console**로 로그인 한 다음 **IAM console**로 들어갑니다.
![Images/IAMrole01.png](/cost/200_aws_resource_optimization/Images/IAMrole01.png)

2. 왼쪽 메뉴페이지에서 **Roles**을 선택하고 **Create role**을 클릭합니다.
![Images/IAMrole02.png](/cost/200_aws_resource_optimization/Images/IAMrole02.png)

3. **Choose a use case** 아래, **EC2**를 클릭합니다(EC2가 AWS Services를 호출하는 것을 허락). 그리고 **Next: Permissions**를 클릭합니다.
![Images/IAMrole03.png](/cost/200_aws_resource_optimization/Images/IAMrole03.png)

4. 정책목록 중, `CloudWatchAgentServerPolicy`의 체크박스를 선택합니다. 검색창에 이름을 넣어서 검색하면 찾기 쉽습니다. **Next: Tags**를 클릭합니다:
4. ![Images/IAMrole04.png](/cost/200_aws_resource_optimization/Images/IAMrole04.png)

5. 태그(옵션)를 추가합니다. **Next: Review**클릭합니다.
![Images/IAMrole05.png](/cost/200_aws_resource_optimization/Images/IAMrole05.png)

6. **Policies**에 **CloudWatchAgentServerPolicy**가 있는지를 확인합니다. 그리고 role name에 `CloudWatchAgentServerRole`을 넣습니다. 필요하다면 description을 입력합니다. **Create role**을 클릭합니다.
![Images/IAMrole06.png](/cost/200_aws_resource_optimization/Images/IAMrole06.png)

role이 생성되었습니다.
