---
title: "계정 구조 만들기"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---


### AWS Organizations

---

AWS Organizations는 AWS의 워크로드가 증가하고 확장됨에 따라 환경을 중앙에서 관리하는 데 도움이 됩니다. 성장하는 스타트업이든, 대기업이든 관계없이 AWS Organizations를 활용하면 결제를 관리하고, 액세스, 규정 준수 및 보안을 제어하고, AWS 계정에서 리소스를 공유하는 일을 모두 중앙에서 손쉽게 처리할 수 있습니다.

AWS Organizations를 사용하면 계정 생성을 자동화하고, 비즈니스 요구를 반영하도록 계정 그룹을 생성하고, 거버넌스를 위해 이러한 그룹에 정책을 적용할 수 있습니다. 또한 모든 AWS 계정에 대해 단일 결제 방법을 설정하여 결제 과정을 간소화할 수도 있습니다. 다른 AWS 서비스와 통합할 경우 AWS Organizations를 사용하여 조직의 계정 전반에 걸쳐 중앙 구성 및 리소스 공유를 정의할 수 있습니다. AWS Organizations는 모든 AWS 고객이 추가 비용 없이 사용할 수 있습니다.

---

{{% notice warning %}}
만약 조직 및 통합 결제가 설정되어있다면 과정을 수행하지 마세요.
{{% /notice %}}

AWS Organization을 생성하고 둘 이상의 계정을 마스터계정에 가입시킵니다. 조직에서는 여러 AWS 계정을 효율적이고 일관되게 중앙에서 관리 할 수 있습니다. 제한된 청구작업을 위해 제한된 보안 및 관리권한을 가지는 마스터계정을 갖는 것이 좋습니다. 비용최적화팀 또는 다른기능을 위한 전용 AWS계정과 워크로드 리소스를 위한 다른계정을 생성하세요.

organizations가 필요합니다.: CreateOrganization 액세스 및 2 개 이상의 AWS 계정이 필요합니다. 멤버계정을 마스터계정에 가입 시키면 해당 멤버계정에 대한 모든 결제정보가 마스터계정에 포함됩니다. 멤버계정에는 더 이상 청구정보, 이전 청구정보를 볼 수 없습니다. 계정을 마스터계정에 가입시키기 전에 보고서 또는 데이터를 백업하거나 내보내십시오.

### AWS Organizations 생성
{{% notice warning %}}
마스터계정으로 AWS Organization을 생성합니다.
{{% /notice %}}

1. 필요한 권한이 있는 IAM User로 콘솔에 로그인한 뒤, 상단의 **Find Services** 에 *AWS Organizations* 을 검색하고 **AWS Organizations**를 선택합니다.:
![Images/AWSOrg1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg1.png)

2. **Create organization**를 클릭합니다.:
![Images/AWSOrg2.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg2.png)

3. 모든 기능을 가진 조직을 만들기위해 **Create organization**를 선택합니다.
![Images/AWSOrg3.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg3.png)

4. 확인 메일을 받을 것입니다. 당신의 계정에서 **Verify your email address** 를 클릭하세요.:
![Images/AWSOrg4.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg4.png)

5. 당신의 조직 콘솔에서 확인 메세지를 볼 수 있습니다.:
![Images/AWSOrg5.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg5.png)

이제 다른 계정을 조직에 포함시킬 수 있습니다. 

### 멤버계정 가입
이제 다른 계정을 당신의 조직에 가입시킬 수 있습니다. 비용최적화 작업을 수행하는 데 사용될 계정뿐만 아니라 워크로드의 리소스를 실행하는 데 사용되는 다른 구성원들의 계정을 만들고 가입해야합니다.

1. AWS Organizations 콘솔에서 **Add account**를 클릭합니다:
![Images/AWSOrg6.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg6.png)

2. **Invite account**를 클릭합니다.:
![Images/AWSOrg7.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg7.png)

3. 워크로드 계정의 **Email or account ID**를 입력하고, **Notes**에 필요한 정보를 입력합니다. 하단의 **Invite**를 클릭합니다:
![Images/AWSOrg8.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg8.png)

4. 요청이 열려있는것을 확인할 수 있습니다. :
![Images/AWSOrg9.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg9.png)

5. 이제 **멤버계정** (워크로드계정)으로 로그인한 후, **AWS Organizations**으로 갑니다:
![Images/AWSOrg1.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg1.png)

6. 메뉴에서 초대가 온것을 확인할 수 있습니다. **Invitations**을 클릭합니다:
![Images/AWSOrg10.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg10.png)

7. 요청 세부사항(검은 블록 부분)을 확인한 후 **Accept**를 클릭합니다:
![Images/AWSOrg11.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg11.png)

8. Organization ID (검은 블록 부분)를 확인하고, **Confirm**를 클릭합니다:
![Images/AWSOrg12.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg12.png)

9. 멤버계정(워크로드계정)이 당신의 조직에 포함된 것을 확인할 수 있습니다. 
![Images/AWSOrg13.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg13.png)

10. 멤버계정(워크로드계정)에 조직가입 성공메일이 보내진 것을 확인할 수 있습니다.:
![Images/AWSOrg14.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg14.png)

11. 마스터계정도 새로운 멤버계정이 가입된 것을 메일로 확인할 수 있습니다:
![Images/AWSOrg15.png](/Cost/100_1_AWS_Account_Setup/Images/AWSOrg15.png)

다른계정도 위 내용을 반복하여 조직에 포함시켜주세요.

### 서비스 제어 정책 활성화
서비스 제어정첵을 활성화 할 수 있습니다. 중앙에서 사용가능한 최대권한을 조절할 수 있습니다. - 비용관리 및 조직 전체의 태그 표준화를 위한 정책들이 도움이 됩니다. 

1. **마스터계정**으로 로그인 한 뒤 AWS Organizations console에서 **Policies**를 선택합니다:
![Images/Organizations_Policies.png](/Cost/100_1_AWS_Account_Setup/Images/Organizations_Policies.png)

2. 기본적으로 두 정책은 모두 비활성화되어 있습니다. **Service control policies**를 클릭하세요.:
![Images/OrganizationsPolicies_SCPenable.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_SCPenable.png)

3. **Enable service control policies**를 클릭하세요:
![Images/OrganizationsPolicies_SCPenable2.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_SCPenable2.png)

4. **Service control policies are enabled**을 볼 수 있습니다. **Policies**를 클릭하세요:
![Images/OrganizationsPolicies_SCPenable3.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_SCPenable3.png)

5. 태그 정책을 활성화 할 것입니다. **Tag policies**를 클릭하세요:
![Images/OrganizationsPolicies_Tagenable.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_Tagenable.png)

6. **Enable tag policies**를 선택합니다:
![Images/OrganizationsPolicies_Tagenable2.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_Tagenable2.png)

7. **Tag policies are enabled**를 볼 수 있습니다. **Policies**를 클릭하세요:
![Images/OrganizationsPolicies_Tagenable3.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_Tagenable3.png)

8. 이제 서비스제어정책과 태그정책이 활성화 되어있는 것을 볼 수 있습니다:
![Images/OrganizationsPolicies_complete.png](/Cost/100_1_AWS_Account_Setup/Images/OrganizationsPolicies_complete.png)


