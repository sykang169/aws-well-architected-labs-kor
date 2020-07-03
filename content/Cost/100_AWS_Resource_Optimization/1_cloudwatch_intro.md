---
title: "Amazon Cloudwatch에 대하여 알아보기"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---

적정 크기 조정을 수행하는 첫 번째 단계는 현재 서비스 사용을 모니터링하고 분석하여 인스턴스 성능 및 사용 패턴에 대한 통찰력을 얻는 것입니다. 충분한 데이터를 수집하려면 최소 2 주 이상 (이상적으로는 1 개월 이상)의 성능을 관찰하여 워크로드와 사용량의 정점을 확인하십시오. 인스턴스 성능을 정의하는 가장 일반적인 지표는 vCPU 사용률, 메모리 사용률, 네트워크 사용률 및 디스크 사용률입니다.

1. Log into your AWS console via SSO, go to the **Amazon CloudWatch** service page:
![Images/CloudWatch01.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch01.png)

2. Select **EC2** under the **Service Dashboard**:
![Images/CloudWatch02.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch02.png)

3. Observe the **Service Dashboard** and all of its different metrics, but focus on **CPU Utilization** and **Network In** and **Out**:
![Images/CloudWatch03.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch03.png)

4. Select one of the **EC2** resources by clicking on the little color icon to the left of the **resource-id** name:
![Images/CloudWatch04.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch04.png)

5. Deselect the **EC2 resource** and now modify the time range on the top right, click **custom** and select the **last 2 weeks**:
![Images/CloudWatch05.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch05.png)

6. Navigate to the **CPU Utilization Average** widget, click the **three dots** and launch the **View in metrics** page. Using the **Graphed metrics** section try to answer the following questions:

- a. What is the instance with the highest CPU Average?
- b. What is the instance with the highest CPU Max?
- c. What is the instance with the lowest CPU Min?

![Images/CloudWatch05.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch06.png)
![Images/CloudWatch05.png](/Cost/100_AWS_Resource_Optimization/Images/CloudWatch07.png)
