---
title: "Amazon QuickSight 설정"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>6. </b>"
weight: 6
---

이제 워크로드 계정의 사용자가  분석 및 대시보드를 만들 수 있도록 Amazon QuickSight를 설정할 것입니다.

###  첫 QuickSight 설정

1. **워크로드 계정**의 IAM 사용자로 콘솔에 로그인합니다. 그리고 **Amazon QuickSight** 콘솔로 이동합니다:
![Images/AWSQuicksight1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksight1.png)

2. 이전에 QuickSight의 **Sign up for QuickSight**를 진행했다면, **Setup QuickSight IAM Policy** 으로 바로 건너 뛰어도 됩니다:
![Images/AWSQuicksight2.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksight2.png)

3. **Standard** 에디션을 선택하고 **Continue**를 클릭합니다:
![Images/AWSQuicksight3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksight3.png)

4. CUR 파일이 있는 **region**을 선택합니다. **QuickSight account name**에 계정이름, **Notification email address**에 email을 입력합니다. 그리고  **Amazon Athena** 를 선택한 후 **Choose S3 buckets**을 클릭합니다:
![Images/AWSQuicksight4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksight4.png)

5. **S3 Buckets You Can Access Across AWS**을 클릭하고, 아래 **Use a different bucket**에  **CUR bucket 이름**을 입력합니다, **Add S3 bucket**을 클릭하고 **Finish**를 클릭합니다:
![Images/AWSQuicksights3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksights3.png)

6. **Finish**를 클릭합니다:
![Images/AWSQuicksight80.png](/Cost/100_1_AWS_Account_Setup/Images/AWSQuicksight80.png)

### QuickSight IAM 정책 설정

1. **IAM Dashboard**로 갑니다.

2. **Policies**를 클릭하고 검색창에 `AWSQuickSightS3Policy`를 검색한 뒤, 검색결과 `AWSQuickSightS3Policy` 선택하세요:
![Images/IAMPolicy_editQS.png](/Cost/100_1_AWS_Account_Setup/Images/IAMPolicy_editQS.png)

3. **Edit policy**를 클릭합니다. 그리고 아래와 같이 S3의 Resource에 `arn:aws:s3:::cost*`를 추가합니다.  
![Images/IAMPolicy_editpolicy.png](/Cost/100_1_AWS_Account_Setup/Images/IAMPolicy_editpolicy.png)

4. 이것은 QuickSight가 s3 버킷이 **cost**로 시작한다면 모두 접근이 가능하게되며, 비용최적화 사용자는추가적인 QuickSight권한 없이도 데이터셋을 쉽게 생성할 수 있게됩니다. **Review policy**를 클릭합니다.
![Images/IAMPolicy_editreview.png](/Cost/100_1_AWS_Account_Setup/Images/IAMPolicy_editreview.png)

5. **Save changes**를 클릭합니다:
![Images/IAMPolicy_save.png](/Cost/100_1_AWS_Account_Setup/Images/IAMPolicy_save.png)

{{% notice tip %}}
축하합니다 - 이제 QuickSight를 설정을 완료했습니다. 비용최적화팀은 QuickSight를 자체 관리하고 올바른 버킷 이름으로 S3의 데이터 세트에 액세스 할 수 있습니다.
{{% /notice %}}
