---
title: "Amazon Cloudwatch에 대하여 알아보기"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---

{{% notice warning %}}
이 실습은 실제 사용 계정에서 진행 해보세요. 현재 Lab환경으로는 수행하실 수 없습니다.
{{% /notice %}}

적정 크기 조정을 수행하는 첫 번째 단계는 현재 서비스 사용을 모니터링하고 분석하여 인스턴스 성능 및 사용 패턴에 대한 통찰력을 얻는 것입니다. 충분한 데이터를 수집하려면 최소 2 주 이상 (이상적으로는 1 개월 이상)의 성능을 관찰하여 워크로드와 사용량의 정점을 확인하십시오. 인스턴스 성능을 정의하는 가장 일반적인 지표는 vCPU 사용률, 메모리 사용률, 네트워크 사용률 및 디스크 사용률입니다.

1. Log into your AWS console via SSO, go to the **Amazon CloudWatch** service page:
![Images/CloudWatch01.png](/cost/100_aws_resource_optimization/Images/CloudWatch01.png)

2. **EC2**의 **Service Dashboard**를 클릭합니다:
![Images/CloudWatch02.png](/cost/100_aws_resource_optimization/Images/CloudWatch02.png)

3. **Service Dashboard** 및 모든 다른 지표를 관찰하지만 CPU 사용률 및 네트워크 입출력에 중점을 둡니다.:
![Images/CloudWatch03.png](/cost/100_aws_resource_optimization/Images/CloudWatch03.png)

4. **resource-id**가 쓰여있는 왼쪽의 작은 아이콘을 클릭하여 EC2 자원 중 하나를 선택하십시오.:
![Images/CloudWatch04.png](/cost/100_aws_resource_optimization/Images/CloudWatch04.png)

5. EC2 리소스를 선택 해제하고 오른쪽 상단의 시간 범위를 수정합니다. custom을 클릭 한 후 **2주**를 범위로 잡습니다.:
![Images/CloudWatch05.png](/cost/100_aws_resource_optimization/Images/CloudWatch05.png)

6. Navigate to the **CPU Utilization Average** widget, click the **three dots** and launch the **View in metrics** page. Using the **Graphed metrics** section try to answer the following questions:

6. **CPU Utilization Average** 위젯으로 이동하여 3 개의 점을 클릭하고 지표 보기 페이지를 시작하십시오. 그래프 측정 항목 섹션을 사용하여 다음 질문에 답하십시오.

- a. CPU 사용율 평균이 가장 높은 인스턴스는 무엇입니까?
- b. CPU 사용율 최대값이 가장 높은 인스턴스는 무엇입니까?
- c. CPU 사용율 최소값이 가장 낮은 인스턴스는 무엇입니까?

![Images/CloudWatch05.png](/cost/100_aws_resource_optimization/Images/CloudWatch06.png)
![Images/CloudWatch05.png](/cost/100_aws_resource_optimization/Images/CloudWatch07.png)
