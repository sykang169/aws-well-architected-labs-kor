---
title: "워크로드 생성"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---



1. AWS 콘솔에 로그인 한 후 서비스 검색창에 Well-Architected Tools을 입력합니다. 
    링크를 통해 바로갈 수 있습니다. : [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).

    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT0.png)

    Well-Architected 리뷰는 [워크로드](https://wa.aws.amazon.com/wat.concept.workload.en.html)단위로 생성합니다(워크로드는 비지니스 가치를 제공하는 단위로 식별됩니다.). 

1. 랜딩페이지 회면의 **Define Workload** 버튼을 클릭합니다.:
    ![ClickWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT1.png)

1. 만약 이미 생성한 워크로드가 있다면, 워크로드 리스트가 나올 것입니다. 동일하게 이 화면에서도 **Define Workload** 버튼을 클릭합니다.
    ![ClickWorkload2](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT2.png)

1. 워크로드 정의 인터페이스에서 필요한 정보를 입력하세요:
    - Name: `Workload for AWS Workshop`  
    - Description: `wellarchitectedlabs workshop`  
    - Environment: Select **Pre-production**  
    - Review owner: 워크로드 담당자의 이름 또는 email주소
    - Account ID: \<AWS ACCOUNT_NUMBER\>
    - Regions: AWS Regions 선택, **(Seoul)/ap-northeast-2**  
    ![EnterWorkloadDetails](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload.png)
  
    - Industry Type: `InfoTech`(옵션) 
    - Industry: `Internet`(옵션)  
    ![DefineWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload2.png)
    입력이 완료됬으면 **Next** 버튼을 클릭합니다:

1. **Apply lenses** 탭에서  **AWS Well-Architected Framework** 체크박스를 클릭합니다. **AWS Well-Architected Framework** 사용하면 정식으로 AWS 모범 사례와 고객의 워크로드를 비교하고 개선에 대한 지침을 얻을 수 있습니다.또한 특정한 워크로드에 조언을 더 많이 제공하기 위해 워크로드에 맞는 다른 Lense를 선택하실 수도 있습니다.:
    ![DefineWorkload](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-workload3.png)
    **Define workload**를 클릭합니다.
