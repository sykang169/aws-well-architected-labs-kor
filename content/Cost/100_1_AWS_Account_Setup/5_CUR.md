---
title: "비용 및 사용 보고서(CUR) 설정"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>5. </b>"
weight: 5
---

## AWS 비용 및 사용 보고서란 무엇입니까?

---

AWS 비용 및 사용 보고서(AWS CUR)에는 사용 가능한 가장 포괄적인 비용 및 사용 데이터 집합이 포함되어 있습니다. 비용 및 사용 보고서를 사용하여 소유한 Amazon Simple Storage Service(Amazon S3) 버킷에 AWS 결제 보고서를 게시할 수 있습니다. 시간이나 월, 제품이나 제품 리소스, 또는 직접 정의한 태그를 기준으로 비용을 구분한 보고서를 받을 수 있습니다. AWS는 이 보고서를 하루에 한 번 CSV(쉼표로 분리된 값) 형식으로 버킷에 업데이트합니다. Microsoft Excel, Apache OpenOffice Calc와 같은 스프레드시트 소프트웨어를 사용하여 보고서를 보거나 애플리케이션에서 Amazon S3 API를 사용하여 액세스할 수 있습니다.

AWS 비용 및 사용 보고서은 AWS 사용량을 추적하고 계정과 관련된 예상 요금을 알려줍니다. 각 보고서에는 AWS 제품, 사용 유형, AWS 계정에서 사용하는 작업에 대해 각각 고유하게 조합된 항목들이 포함되어 있습니다. AWS 비용 및 사용 보고서을 사용자 지정하여 정보를 시간별 또는 일별로 집계할 수 있습니다.

---

비용 및 사용 보고서는 사용 및 청구서에 대한 가장 자세한 정보를 제공합니다. 매일 1 시간마다 자원 당 1 개의 보고서를 제공하도록 구성 할 수 있습니다. 사용량 및 청구 정보에 액세스하고 분석 할 수 있도록 구성해야합니다.

###  비용 및 사용 보고서 설정
여러 비용 및 사용 보고서(CURs)를 사용한다면 1개의 CUR당 하나의 버킷을 사용할 것을 권장드립니다. 단일 버킷에 여러 CUR이 있어야하는 경우 보고서의 경로에 전치사를 사용하여 다른 보고서와 구분할 수 있도록 해야합니다.

{{% notice info %}}
AWS Organization를 생성한 마스터계정으로 진행합니다.
{{% /notice %}}


1. 올바른 권한을 가진 마스터계정의 IAM사용자로 로그인을 한 후, 콘솔의 **Billing**을 검색하여 선택합니다:
![Images/AWSCUR1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCUR1.png)

2. 왼쪽 메뉴의 **Cost & Usage Reports**를 선택합니다:
![Images/AWSCUR2.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCUR2.png)

3. **Create report**를 선택합니다.:
![Images/AWSCUR3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCUR3.png)

4. **Report name** 을 입력하고(`masterCUR`), **Include resource IDs** 와 **Data refresh settings**를 선택합니다. **Next** 버튼을 누릅니다:
![Images/AWSCUR4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCUR4.png)

5. **Configure**를 클릭합니다:
![Images/AWSCURDelivery0.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCURDelivery0.png)

6. 유니크한 버킷이름을 입력하고 리전이 정확한지 확인합니다. 그리고 **Next**를 클릭합니다:
![Images/AWSCURDelivery1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCURDelivery1.png)

7. 정책을 읽어보고 확인하세요. 이것은 해당 버킷에 빌링 보고서를 저장권한을 할당합니다. **I have confirmed that this policy is correct**를 클릭하고 **Save** 클릭하세요:
![Images/AWSCURDelivery3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCURDelivery3.png)

8. 검증과 설정:
- 버킷 요구사항의 **Valid Bucket**이 녹색으로 체크되어있는지 확인하세요(만약 아니라면 버킷 정책을 확인하세요)
- '/' 없이 **Report path prefix**를 입력하세요 (어떤 글자든 상관 없습니다.) 
- **Time Granularity** 가 **Hourly**인지 확인하세요.
- **Report Versioning** 는 **Overwrite existing report**로 설정하세요.
- **Enable report data integration for** 아래 **Amazon Athena**를 선택하고 **Next**클릭합니다:
![Images/AWSCURDelivery4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCURDelivery4.png)

9. 설정을 확인한 후, 스크롤을 내려 **Review and Complete**를 클릭하세요:
![Images/AWSCUR6.png](/Cost/100_1_AWS_Account_Setup/Images/AWSCUR6.png)

비용 및 사용 보고서가 전달되도록 성공적으로 구성했습니다. 첫 번째 보고서를 생성하여 받는데 최대 24 시간이 걸릴 수 있습니다.

{{% notice note %}}
S3 비용을 최소화하기 위해 CUR은 압축됩니다.
{{% /notice %}}


### CUR 버킷 설정
워크로드 계정이 CUR에 액세스 할 수 있도록 CUR버킷을 업데이트합니다.

1. S3콘솔로가서, **CUR Bucket**을 선택하고, **Permissions**을 선택합니다.:
![Images/s3cur_permissions.png](/Cost/100_1_AWS_Account_Setup/Images/s3cur_permissions.png)

2. **Bucket Policy**을 클릭합니다:
![Images/s3cur_bucketpolicy.png](/Cost/100_1_AWS_Account_Setup/Images/s3cur_bucketpolicy.png)

3. 워크로드 계정의 S3 읽기 권한을 추가하기위해 아래와 같은 정책을 현재 버킷에 추가 할 것입니다. 버킷정책의 **(sub account ID)** 와 **(CUR bucket)** 을 수정한 뒤 버킷정책을 업데이트합니다.

        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::(sub account ID):root"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::(CUR bucket)"
        },
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::(sub account ID):root"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::(CUR bucket)/*"
        }


{{%expand "클릭하여 완성된 정책 예제 보기" %}}
    {
        "Version": "2008-10-17",
        "Id": "123",
        "Statement": [
            {
                "Sid": "Stmt1335892150622",
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::386209384616:root"
                },
                "Action": [
                    "s3:GetBucketAcl",
                    "s3:GetBucketPolicy"
                ],
                "Resource": "arn:aws:s3:::(CUR Bucket)"
            },
            {
                "Sid": "Stmt1335892526596",
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::386209384616:root"
                },
                "Action": "s3:PutObject",
                "Resource": "arn:aws:s3:::(CUR Bucket)/*"
            },
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::(Sub Account ID):root"
                },
                "Action": "s3:ListBucket",
                "Resource": "arn:aws:s3:::(CUR Bucket)"
            },
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::(Sub Account ID):root"
                },
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::(CUR Bucket)/*"
            }
        ]
    }

{{% /expand%}}





### S3 오브젝트 ACL의 덮어쓰기 설정
이제 새로 제공되는 CUR 파일에서 ACL을 다시 작성하도록 Lambda 함수를 설정할 것입니다. 이것은 CUR파일의 읽기 권한이 버킷소유자(마스터계정)의 접근권한으로만 제공되므로 하위 계정이 CUR파일을 읽을 수 있도록하는 데 필요합니다.

1. IAM 대시보드로 갑니다.

2. **Policies**를 선택한 후, **Create policy**를 클릭합니다:
![Images/IAMPolicy_Createpolicy.png](/Cost/100_1_AWS_Account_Setup/Images/IAMPolicy_Createpolicy.png)

3. **JSON**을 클릭합니다. 아래와 같이 정책을 수정합니다. - **(bucket name)** 은 CUR버킷으로 수정하고, **Review policy**를 클릭합니다:

       {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "s3:PutObjectVersionAcl",
                       "s3:PutObjectAcl"
                   ],
                   "Resource": "arn:aws:s3:::(bucket name)/*"
               }
           ]
       }

![Images/splitsharecur1.png](/Cost/100_1_AWS_Account_Setup/Images/splitsharecur1.png)

4. 이름에 `Lambda_S3Linked_PutACL`을 입력하고 **Description**에 `Policy to allow Lambda to re-write CUR ACLs in S3`를 입력한 후 **Create policy**를 클릭합니다:
![Images/IAM_PolicyCreate.png](/Cost/100_1_AWS_Account_Setup/Images/IAM_PolicyCreate.png)

5. **Roles**을 클릭하고, **Create role**을 클릭합니다:
![Images/IAMRole_Create.png](/Cost/100_1_AWS_Account_Setup/Images/IAMRole_Create.png)

6. use case에서 **Lambda**를 선택한 후, **Next: Permissions**를 클릭합니다:
![Images/IAM_LambdaPermissions.png](/Cost/100_1_AWS_Account_Setup/Images/IAM_LambdaPermissions.png)

7. **Lambda_S3Linked_PutACL** 정책을 검색하고, 체크한 뒤 **Next: Tags**를 클릭합니다:
![Images/IAM_PolicyTags.png](/Cost/100_1_AWS_Account_Setup/Images/IAM_PolicyTags.png)

8. **Next: Review**를 클릭합니다.

9. **Role name**에 `Lambda_Put_Linked_S3ACL`, **Role description**에 `Allows lambda function to call AwS services on your behalf`를 입련한 다음 **Create role**을 클릭합니다:
![Images/IAM_RoleCreate.png](/Cost/100_1_AWS_Account_Setup/Images/IAM_RoleCreate.png)

10. **Lambda**의 서비스 대시보드로 간 다음 **Create function**을 클릭합니다\:
![Images/Lambda_home.png](/Cost/100_1_AWS_Account_Setup/Images/Lambda_home.png)

11. **Author from scratch** 를 선택한 후, **function name** 에 `S3LinkedPutACL`를 입력하고, 런타임은 **Node.js 12.x**, **Execution role**은 `Use an existing role`을 선택합니다. 그리고 **Existing role**은 `Lambda_Put_Linked_S3ACL`을 선택한 다음**Create function**을 클릭합니다:
![Images/Lambda_functionscratch.png](/Cost/100_1_AWS_Account_Setup/Images/Lambda_functionscratch.png)

12. 다음의 람다 코드를 붙여넣습니다. 아래 값들은 수정하여 붙여넣습니다:
 
 - **Master Account Name**: 마스터 오너 계정의 이름 - email에서 @뒷부분을 제외한 아이디를 적습니다.이 계정은 FULL_CONTROL 권한을 얻습니다.
 - **Master Canonical ID**: 마스터 오너의 canonical ID, 12자리 숫자로된 아이디를 말합니다. 아이디를 확인하는 방법은 이곳 https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html에 있습니다.
 - **Linked Account Name**: 워크로드 계정 아이디 - email에서 @뒷부분을 제외한 아이디를 적습니다.이 계정은 READ 권한을 얻습니다.
 - **Linked Account Canonical ID**: 워크로드 계정의 canonical ID


{{%expand "클릭 확장하여 람다 코드 전체보기" %}}

    const AWS = require('aws-sdk');
    const util = require('util');

    // Main Loop
    exports.handler = function(event, context, callback) {
    
        // If its an object delete, do nothing
        if (event.RequestType === 'Delete') {
        }
        else // Its an object put
        {
            // Get the source bucket from the S3 event
            var srcBucket = event.Records[0].s3.bucket.name;
        
            // Object key may have spaces or unicode non-ASCII characters, decode it
            var srcKey = decodeURIComponent(event.Records[0].s3.object.key.replace(/\+/g, " "));  

            // Gets the top level folder, which is the key for the permissions array        
            var folderID = srcKey.split("/")[0];

            // Define the object permissions, using the permissions array
            var params =
            {
                Bucket: srcBucket,
                Key: srcKey,
                AccessControlPolicy:
                {
                    'Owner':
                    {
                        'DisplayName': 'aws-billpresentation+artifact-storage',
                        'ID': '72b999b38bdff6b040374efc3086ba5a0a87c0c07e1eda14fe56fadb2b4a6ef0'
                    },
                    'Grants': 
                    [
                        {
                            'Grantee': 
                            {
                                'Type': 'CanonicalUser',
                                'DisplayName': '(master account name)',
                                'ID': '(master canonical id)'
                            },
                            'Permission': 'FULL_CONTROL'
                        },
                        {
                            'Grantee': {
                                'Type': 'CanonicalUser',
                                'DisplayName': '(linked account name)',
                                'ID': '(linked canonical id)'
                                },
                            'Permission': 'READ'
                        },
                    ]
                }
            };

            // get reference to S3 client 
            var s3 = new AWS.S3();

            // Put the ACL on the object
            s3.putObjectAcl(params, function(err, data) {
                if (err) console.log(err, err.stack); // an error occurred
                else     console.log(data);           // successful response
            });
        }
    };

{{% /expand%}}

13. **Save**버튼을 클릭합니다:
![Images/Lambda_functionsave.png](/Cost/100_1_AWS_Account_Setup/Images/Lambda_functionsave.png)

14. **S3 service dashboard**로 가서, 당신의 **CUR** 버킷을 클릭한 후 **Properties**클릭하세요:
![Images/s3cur_bucketproperties.png](/Cost/100_1_AWS_Account_Setup/Images/s3cur_bucketproperties.png)

15. **Events**를 선택하고, **Add notification**을 클릭합니다:
![Images/s3cur_event.png](/Cost/100_1_AWS_Account_Setup/Images/s3cur_event.png)

16. 이름에 `S3PutACL`을 입력하고 **All object create events**를 선택합니다, **Send to**에 `Lambda Function`를 선택하고, **Lambda function**은 `S3LinkedPutACL`를 선택한 후 **Save**를 누릅니다:
![Images/s3_event.png](/Cost/100_1_AWS_Account_Setup/Images/s3_event.png)

17. AWS가 다음 CUR 파일을 제공 할 때까지(최대 24시간)기다려야합니다. 최신 CUR파일로 이동하여 권한을 확인하면 원본소유자(AWS), 전체 권한이있는 마스터계정 (원본 별) 및 연결 된 비용최적화팀 계정이 읽기권한으로 표시됩니다.
![Images/s3_newCUR.png](/Cost/100_1_AWS_Account_Setup/Images/s3_newCUR.png)


### 이미 존재하는 CURs 업데이트
업데이트 할 권한이 필요한 다른 보고서의 기존 CUR이있는 경우 다음 CLI를 사용하여 개체와 권한을 직접 복사 하여 업데이트합니다.

    aws s3 cp --recursive s3://(CUR bucket) s3://(CUR bucket) --grants read=id=(sub account canonical ID) full=id=(master account canonical ID) --storage-class STANDARD


{{% notice tip %}}
축하합니다. 이제 워크로드 계정에서 CUR을 제공하고 액세스 할 수 있습니다.
{{% /notice %}}
