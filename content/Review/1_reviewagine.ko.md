---
title: "AWS Well-Architected Tool을 통한 재검토"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1

---

{{% notice tip %}}
모범사례를 적용한 필라를 기준으로 다시 평가합니다.
{{% /notice %}}

1. AWS 콘솔에 로그인 한 후 서비스 검색창에 Well-Architected Tools을 입력합니다. 
    링크를 통해 바로갈 수 있습니다. : [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).

    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT0.png)


1. 이전에 생성한 workload인 **Workload for AWS Workshop**에서 **AWS Well-Architected Framework**를 클릭합니다. 그리고 각 필러를 클릭하여 적용한 모범사례에 해당하는 질문을 체크합니다.
 
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-review.png)


1. **운영우수성**을 예로 들겠습니다. 하단의 **Operational Excellence**를 선택합니다.
    링크를 통해 바로갈 수 있습니다. : [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational.png)


1. 우리는 **운영우수성**에서 **Systems Manager**의 인벤토리와 상태관리자를 사용하여 인스턴스와 인스턴스에 설치된 소프트웨어 정보를 수집하여 **시스템 구성**과 **애플리케이션 자산**을 관리하고 모니터링 하였습니다. 또한 세부정보를 구성하여 규정 준수 상태에 대한 가시성을 확보하였습니다. 또한 패치관리자를 통해 EC2 인스턴스 전체에 자동으로 **운영체제 및 소프트웨어 패치**를 선택 배포하도록 구성하였습니다. 이러한 작업들은 프로덕션환경에 배포된 인스턴스를 모니터링하고 결함을 줄이고 패치와 구성사항을 자동화하는데 매우 큰 도움을 줍니다. 

    해당 작업에 해당하는 질문 **OPS 5. 귀사는 어떻게 결함을 줄이고 수정 작업을 쉽게 수행하고 프로덕션으로 이어지는 흐름을 개선하십니까?** 클릭합니다. 
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational2.png)

1. **None of these**의 체크를 해제하고 **구성 관리 시스템 사용**과 **패치 관리 수행**를 클릭합니다. 해당질문의 **정보**를 클릭하여 자세한 내용을 확인할 수도 있습니다.
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational3.png)
    아직 개선해야할 점이 더 많습니다. 11개의 질문중 2개밖에 선택하지 못했습니다. 더 많은 질문을 선택할 수 있어야 위험요소를 줄일 수 있습니다. 스크롤을 아래로 내리면 우리가 적용 할 수 있는 다양한 개선사항들을 볼 수 있습니다.
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational4.png)

1. 확인이 끝나면 상단의 **Save and exit**를 클릭합니다.

1. 이런식으로 다른 필라도 질문을 재검토합니다. AWS Well-Architected Framework의 위험사항을 줄이기 위해선 다양한 모범사례를 적용하고 리뷰를 반복적으로 수행해야합니다. 실제 워크로드에선 **주기적으로 리뷰**를 진행하세요. 아키텍쳐의 위험요소를 제거하고 확장가능하고 안전한 아키텍쳐를 만들 수 있습니다. 필요한 경우 파트너 또는 SA와 함께 리뷰를 진행하실 수도 있습니다.

1. [https://wellarchitectedlabs.com/](https://wellarchitectedlabs.com/)에서 더 많은 정보를 얻을 수 있습니다. 