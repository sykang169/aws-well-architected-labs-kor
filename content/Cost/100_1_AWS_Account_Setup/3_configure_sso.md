---
title: "Single Sign On (SSO) 활성화"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---

### AWS Single Sign-On

---

AWS Single Sign-On(SSO)을 사용하면 여러 AWS 계정 및 비즈니스 애플리케이션에 대한 액세스를 중앙에서 손쉽게 관리하고 사용자에게 Single Sign-On 액세스를 제공하여 할당된 모든 계정 및 애플리케이션을 한 곳에서 액세스하도록 할 수 있습니다. AWS SSO를 사용하면 AWS Organizations의 모든 내 계정에 대한 액세스와 사용자 권한을 중앙에서 손쉽게 관리할 수 있습니다. AWS SSO는 계정에 필요한 모든 권한을 자동으로 구성하고 관리하므로 각 계정에서 추가로 설정할 필요가 없습니다. 일반적인 작업 기능을 기반으로 사용자 권한을 할당하고 특정 보안 요구 사항을 충족하도록 해당 권한을 사용자 지정할 수 있습니다. 또한 AWS SSO는 Salesforce, Box 및 Office 365와 같은 많은 비즈니스 애플리케이션에 대한 통합을 기본적으로 제공합니다.

AWS SSO를 사용하면 AWS SSO의 자격 증명 저장소에서 사용자 자격 증명을 생성 및 관리하거나 Microsoft Active Directory 및 Azure Active Directory(Azure AD) 및 Okta Universal Directory를 비롯한 기존 자격 증명 소스에 쉽게 연결할 수 있습니다.

손쉽게 AWS SSO를 시작할 수 있습니다. AWS SSO 관리 콘솔에서 몇 번의 클릭만으로 AWS SSO를 기존 자격 증명 소스에 연결하고 사용자에게 단일 사용자 포털에서 할당된 AWS Organizations 계정 및 수백 개의 사전 통합된 클라우드 애플리케이션에 대한 액세스 권한을 부여하는 권한을 구성할 수 있습니다.

---

### SSO 설정
{{% notice info %}}
AWS Organization를 생성한 마스터계정으로 진행합니다.
{{% /notice %}}

1. 권한이 있는 IAM사용자로 로그인 한 후, **Find Services**에서 **SSO**를 검색한 다음 **AWS Single Sign-On**를 클릭합니다:
    ![Images/home_sso.png](/Cost/100_1_AWS_Account_Setup/Images/home_sso.png)

1. **Enable AWS SSO**를 클릭합니다:
    ![Images/sso_enable.png](/Cost/100_1_AWS_Account_Setup/Images/sso_enable.png)

1. **Groups**을 선택합니다:
    ![Images/ssodashboard_groups.png](/Cost/100_1_AWS_Account_Setup/Images/ssodashboard_groups.png)

1. **Create group**을 선택합니다:
    ![Images/ssogroups_create.png](/Cost/100_1_AWS_Account_Setup/Images/ssogroups_create.png)

1. 그룹 이름에 `Cost_Optimization`를 입력하고 설명에 `For Cost Optimazion User`를   입력한 후**Create**를 선택합니다:
    ![Images/ssogroup_details.png](/Cost/100_1_AWS_Account_Setup/Images/ssogroup_details.png)

1. **Users**를 클릭합니다:
    ![Images/ssodashboard_users.png](/Cost/100_1_AWS_Account_Setup/Images/ssodashboard_users.png)

1. **Add user**를 클릭합니다:
    ![Images/ssouser_adduser.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_adduser.png)

1. 아래 세부사항들을 입력합니다:
    - **Username**:`CostUser1`
    - **Password**
    - **Email address**
    - **First name** : `Cost`
    - **Last name** : `User1`
    - **Display name** : `Cost User1`
    - 필요에 따라 옵션필드를 구성하고 **Next: Groups**을 선택합니다.: 
    ![Images/ssouser_detail.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_detail.png)

1. **Cost_Optimization** 그룹을 선택하고 **Add user**를 클릭합니다:
    ![Images/ssouser_group.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_group.png)

1. 사용자는 **Portal URL** 과 **Username**이 포함된 메일을 받았을 것입니다. 해당메일의 **Accept invitation**를 클릭하세요:
    ![Images/ssouser_email.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_email.png)

1. 포탈로 가면, **Password**를 입력할 수 있습니다. 그리고 **Update user**를 클릭하세요:
    ![Images/ssouser_login.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_login.png)

1. **Continue**를 선택합니다.:
    ![Images/ssouser_activate.png](/Cost/100_1_AWS_Account_Setup/Images/ssouser_activate.png)

    {{% notice note %}}
    나머지 단계를 모두 완료하기 전까지 사용자에게는 권한이 부여되지 않습니다.
    {{% /notice %}}

1. **AWS SSO**의  **AWS accounts**를 클릭하고 **Permission sets**를 선택한 후, **Create permission set**을 클릭하세요:
    ![Images/ssoaccount_createpermission.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_createpermission.png)

1. **Create a custom permission set**의 이름에 `Master_CostOptimization` Description에 `Accessto Cost Optimization services in the master account`를 입력하세요. **Session duration**은 4hours, **Create a custom permissions policy**의 체크박스를 체크합니다. 아래 사용자 지정 권한 정책을 복사하여 세부정책 박스에 붙여넣은 다음 **Create**를 클릭합니다.

    {{% notice warning %}}
    **반드시** 보안관련 팀/전문가와 협력하여 조직에 대한 최소 권한으로 인라인 정책을 작성하도록합니다.
    {{% /notice %}}

    {{%expand "클릭하여 사용자 지정 권한 정책 보기" %}}
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "budgets:*",
                        "ce:*",
                        "aws-portal:*Usage",
                        "aws-portal:*PaymentMethods",
                        "aws-portal:*Billing",
                        "cur:DescribeReportDefinitions",
                        "cur:PutReportDefinition",
                        "cur:DeleteReportDefinition",
                        "cur:ModifyReportDefinition",
                        "pricing:DescribeServices",
                        "wellarchitected:*"
                    ],
                    "Resource": "*"
                }
            ]
        }
    {{% /expand%}}

    ![Images/ssopermissionset_create.png](/Cost/100_1_AWS_Account_Setup/Images/ssopermissionset_create.png)

1. 다시 **Create permission set**를 클릭합니다. 이제 멤버의 정책을 만들 것입니다.


1. 이번엔 다른 브라우저 창을 통해 마스터계정의 **CloudFormation**의 **Stack**으로 갑니다. 처음 생성했던 `MasterAccountStack`을 선택합니다.
    ![images/war/master-account-s3.png](/images/war/master-account-s3.png)

1. 상단의 Outputs를 선택하고 S3bucket의 값을 복사하여 어딘가 기록합니다. 
    ![images/war/master-account-s3.png](/images/war/master-account-select.png)


1. **Create a custom permission set**의 이름에 `Member_CostOptimization` Description에 `Accessto Cost Optimization services in the member account`를 입력하세요. **Session duration**은 4hours, **Create a custom permissions policy**의 체크박스를 체크합니다. 아래 정책을 기본으로 요구사항에 맞게 수정하고, 아래 정책필드의 `(Master CUR bucket)`에 이전에 복사한 S3bucket의 내용을 붙여넣고 `(This Account ID)`를 **워크로드계정**의 12자리 계정 캐노니컬 ID로 변경한 후 정책필드에 아래 내용을 붙여넣습니다. **Create**를 클릭합니다.

    {{% notice warning %}}
    **반드시** 보안관련 팀/전문가와 협력하여 조직에 대한 최소 권한으로 인라인 정책을 작성하도록합니다.
    {{% /notice %}}

    {{%expand "클릭하여 사용자 지정 권한 정책 보기" %}}
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "CostServices",
                    "Effect": "Allow",
                    "Action": [
                        "ce:*",
                        "budgets:*",
                        "aws-portal:*Usage",
                        "aws-portal:*PaymentMethods",
                        "aws-portal:*Billing",
                        "pricing:DescribeServices",
                        "wellarchitected:*"
                    ],
                    "Resource": "*"
                },
                {
                    "Sid": "S3MasterCUR",
                    "Effect": "Allow",
                    "Action": [
                        "s3:GetObject",
                        "s3:ListBucket"
                    ],
                    "Resource": [
                        "arn:aws:s3:::(Master CUR bucket)"
                    ]
                },
            {
                "Sid": "AthenaGlueAndServiceReadAccess",
                "Effect": "Allow",
                "Action": [
                    "athena:*",
                    "glue:*",
                    "iam:ListRoles",
                    "iam:ListPolicies",
                    "s3:GetBucketLocation",
                    "s3:ListAllMyBuckets"
                ],
                "Resource": [
                    "*"
                ]
            },
            {
                "Sid": "QuickSightAccess",
                "Effect": "Allow",
                "Action": [
                    "quicksight:CreateUser",
                    "quicksight:Subscribe"
                ],
                "Resource": "*"
            },
            {
                "Sid": "IAMAccessForGlue",
                "Effect": "Allow",
                "Action": "iam:*",
                "Resource": [
                    "arn:aws:iam::(This Account ID):role/service-role/AWSGlueServiceRole-Cost*",
                    "arn:aws:iam::(This Account ID):policy/service-role/AWSGlueServiceRole-Cost*"
                ]
            },
            {
                "Sid": "S3AccessForAthena",
                "Effect": "Allow",
                "Action": [
                    "s3:GetBucketLocation",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:ListBucketMultipartUploads",
                    "s3:ListMultipartUploadParts",
                    "s3:AbortMultipartUpload",
                    "s3:CreateBucket",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::aws-athena-query-results-*"
                ]
            },
            {
                "Sid": "FullS3AccessForBucketsWithSpecificPrefix",
                "Effect": "Allow",
                "Action": "s3:*",
                "Resource": [
                    "arn:aws:s3:::cost*"
                ]
            }
        ]
        }
    {{% /expand%}}

    ![Images/ssopermissionset_member_create.png](/Cost/100_1_AWS_Account_Setup/Images/ssopermissionset_member_create.png)

1. **AWS organization**을 클릭하고, **마스터계정**을 선택한 다음, **Assign users**를 선택합니다:
    ![Images/ssoaccount_organizationusers.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_organizationusers.png)

1. **Groups**을 선택하고, **Cost_Optimization** 그룹을 클릭한 후, **Next: Permission sets**를 클릭합니다:
    ![Images/ssoaccount_groups.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_groups.png)

1. Permission set의 **Master_CostOptimization**을 체크한 후, **Finish**를 클릭합니다:
    ![Images/ssoaccount_grouppermission.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_grouppermission.png)

1. **Proceed to AWS accounts**클릭합니다:
    ![Images/ssoaccount_success.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_success.png)

1. 워크로드 계정을 맴버로 셋팅합니다. **Memeber account**를 선택하고, **Assign users**를 클릭합니다.

1. **Groups**을 선택하고, **Cost_Optimization** 그룹을 선택한 후, **Next: Permission sets**를 클릭합니다:
    ![Images/ssoaccount_groups.png](/Cost/100_1_AWS_Account_Setup/Images/ssoaccount_groups.png)

1. Permission set의 **Member_CostOptimization**를 선택하고, **Finish**를 클릭합니다.

1. **Proceed to AWS accounts**를 클릭합니다.


{{% notice tip %}}
이제 비용 최적화 사용자, 그룹 및 권한을 설정했습니다.
{{% /notice %}}







