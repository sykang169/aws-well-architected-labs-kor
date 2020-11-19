---
title: "재검토"
weight: 80
pre: "<b>8. </b>"
---

지금까지 3티어 웹에 5개의 필라가 제공하는 모범사례들을 적용해보았습니다. 
이제 처음 리뷰를 진행했던 것과 달라진 것들을 살펴보도록 하겠습니다. 

#### 기존환경
![AWS-Code-Cycle](/images/war/awswellarchitected.svg)

#### 적용된 모범사례
각 필라의 HoL을 수행하셨다면 아래와 같은 모범사례를 기존환경에 적용할 수 있습니다.


| 필라| 이름 | 설명|
|:---|:---|:---|
|성능효율성| **CloudWatch**를 사용한 **모니터링** | CloudWatch의 대쉬보드를 사용하여 현재 EC2의 사용량을 측정하고 모니터링합니다. |
|성능효율성| **CloudWatch**를 사용한 **경보** | CloudWatch가 모니터링하는 CPU사용량이 일정이상 올라가면 사용자에게 E-mail을 통한 경보를 보냅니다.| 
|비용최적화| **EC2**의 **Right Sizeing** | 사용하고 있는 EC2의 적정 크기를 찾아내기위해 Cost Explorer의 Recommendation을 활성화합니다. 나의 사용량에 맞는 적절한 EC2를 추천받고 변경합니다.|
|비용최적화| **CloudWatch Agent**의 Memory Metric 수집을 통한 **Right Sizeing** 정확도 향상  | Memory Metric을 추가로 수집하여 Right sizeing의 정확도를 향상시킬 수 있습니다.|
|운영우수성| **System Manager**를 사용한 리소스 중앙관리 | System Mangager의 인벤토리를 통해 생성한 EC2인스턴스의 정보를 수집하고 모니터링, 관리합니다. | 
|운영우수성| **System Manager**를 사용한 패치관리 | System Manager의 패치관리자를 통해 보안 관련 및 업데이트를 인스턴스에 손쉽게 적용하고 자동화합니다. | 
|안정성| **Chaos testing**을 통한 워크로드의 안정성 테스트 | EC2, RDS, AZ를 정지시키는 스크립트를 통해 해당 장애가 발생했을 시 워크로드의 복원력을 검증하고 다양한 장애 시나리오에 시스템이 어떻게 반응하는지 평가합니다. | 


#### 첫번째 Well-Architected Framework Review 이후 환경
![AWS-Code-Cycle](/images/war/awswellarchitected-after2.svg)

이제 적용한 모범사례에 맞춰서 다시 Well-Architected tools의 워크로드 리뷰를 진행하겠습니다.
