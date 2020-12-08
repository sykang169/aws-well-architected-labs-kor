---
title: "리뷰 진행"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 2
---

1. 워크로드에 대한 세부 사항 페이지에서 **Start review** 버튼을 클릭합니다. 그리고 AWS Well-Architected Framework를 선택합니다. 
    ![StartingReview](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-review.png)  

1. **Operational Excellence**  질문의 왼쪽에 **삼각형버튼**을 클릭하여 질문창을 축소하면 다른 Pillar의 질문들도 확인할 수 있습니다. 물론 순차적으로 진행하면 자연스럽게 다음단계로 이동합니다.
    ![CollapseOE](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT6.png)

1. 예를들어 **안정성**의 리뷰를 진행하도록 하겠습니다. 안정성 메뉴의 삼각형을 클릭하면 세부적인 질문을 확인하실 수 있습니다.
    ![ExpandReliability](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT7.png)

1. 첫번째 질문입니다: **REL 1. 계정에 대한 AWS 서비스 한도를 어떻게 관리하고 있습니까?**
    ![SelectREL1](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT8.png)

1. 현재 배포된 아키텍쳐를 생각하며 **REL 1** 에서 **REL 9** 질문에 답해보십시오. **정보** 링크를 클릭하여 질문의 의미를 이해할 수 있으며, **관련 비디오**를 시청하여 더 많은 컨텍스트를 얻을 수도 있습니다. 만약 해당 질문이 워크로드에 적용되지 않는다면 **질문이 워크로드에 적용되지 않음** 버튼을 활성화하여 질문을 건너 뛸 수도 있습니다. 
    ![InfoAndVideo](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT9.png)

1. 만약 워크로드에 해당 질문을 적용할 수 있으나 세부사항에 해당되는 내용이 없다면 맨 아래 **해당사항없음**을 선택해주세요. 질문의 옆에 **Done**이 표시되면 해당 질문에 대한 대답이 완료 된 것입니다.
    ![InfoAndVideo](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-review2.png)


1. 기본적으로 배포된 환경은 아무것도 고려되지 않았기 때문에 별로 체크할 것이 없을 것입니다. 원랜 질문지를 읽고 자신의 아키텍처의 상태에대해 대답해야하지만, 오늘의 실습을 진행하기위해 모든 질문에 **해당사항없음**을 선택하고 넘어가세요. 질문의 대답을 완료하고 답변 하단의 **Next** 버튼을 클릭합니다. :
![SelectNext](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT10.png)

1. 마지막 질문에 도달하면 **Save and Exit:** 를 클릭합니다.
![SelectSave](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT11.png)

1. 모든 질문에 **해당사항없음**을 선택했다면 아래와 같은 리스크가 생성되었을 것입니다.
![SelectSave](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/watools-review3.png)
