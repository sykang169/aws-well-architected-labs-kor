---
title: "업데이트 된 Amazon EC2 리소스 최적화 권장 사항"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>5. </b>"
weight: 5
---

{{% notice info %}}
이 단계를 완료하려면 Amazon EC2 리소스 최적화를 활성화해야합니다. AWS Cost Explorer, 권장 사항 (왼쪽 리스트) 섹션으로 이동하면됩니다.
{{% /notice %}}

{{% notice info %}}
인스턴스에 CloudWatch 에이전트를 방금 설치 한 경우 Amazon EC2 Resource Optimization에서 업데이트 된 권장 사항을 제공하는 데 며칠이 걸릴 수 있으므로 첫 번째 확인 중에 메모리 데이터가 표시되지 않더라도 걱정하지 마십시오.
{{% /notice %}}


CloudWatch에 메모리 데이터를 사용자 지정지표로 사용 했으므로 Amazon EC2 리소스 최적화 권장사항에 어떤 영향을 미치는지 확인하겠습니다.

Amazon EC2 Resource Optimization은 추가 비용없이 AWS 비용 탐색기에서 적정크기 조정 권장사항을 제공합니다. 이러한 권장 사항은 계정, 리전 및 태그에서 유휴상태이거나 사용률이 낮은 인스턴스를 식별합니다. 이러한 권장사항을 생성하기 위해 AWS는 과거 EC2 리소스 사용량(Amazon CloudWatch를 사용, 최근 14 일)과 기존 예약자원의 기록을 분석하여 비용 절감기회를 식별합니다. 권장되는 조치에는 두 가지 유형이 있습니다. 인스턴스가 유휴상태(최대 CPU 사용률이 1%이하)인 경우 **종료**하거나 인스턴스 사용률이 낮을 경우 (최대 CPU 사용률이 1 %-40 %)**다운사이즈**를 권장합니다.
 
기본적으로 Amazon EC2 리소스 최적화는 권장사항을 제공하기 위해 메모리 데이터 포인트가 필요하지 않지만, 해당정보가 사용 가능한 경우 현재 최대 CPU 및 MEM사용률이 1% 에서 40% 사이 인 인스턴스에 대한 다운사이즈 권장사항 업데이트를 고려해야합니다. 다음 단계를 통해 이를 확인하십시오.

1. **AWS Cost Explorer** 로 갑니다.
![Images/ResourceOpt01.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt01.png)

2. 왼쪽 메뉴의 **Recommendations** 를 선택합니다.
![Images/ResourceOpt2.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt02.png)





3. **Amazon EC2 Resource Optimization Recommendations**의 **View All**을 클릭합니다.
![Images/ResourceOpt3.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt03.png)

Amazon EC2 리소스 최적화를 활성화하지 않은 경우, 활성화 한 시점부터 첫 번째 권장사항을 생성하는 데 최대 24시간이 걸릴 수 있습니다. 일반 또는 마스터(지불)계정만 사용 가능하며, 마스터(지불)계정이 설정 페이지(오른쪽 위)에서 특별히 금지하지 않는 한 기본적으로 연결된 계정과 마스터(지불)계정 모두 권한부여 권장사항에 접근 할 수 있습니다.

![Images/ResourceOpt4.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt04.png)

4. Amazon EC2 리소스 최적화 권장사항을 활성화했다면, 권장사항(있는 경우)을 제공하는 화면이 표시됩니다. 자원 최적화 권장사항을 보려면 클릭하십시오.

![Images/ResourceOpt5.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt05.png)

- **Optimization opportunities** – 사용가능한 권장사항
- **Estimated monthly savings** – 제공된 각 권장사항과 관련된 예상 월별 절감액의 합계
- **Estimated savings (%)** – 권장사항의 인스턴스와 Amazon EC2 비용(온디맨드)과 비교하여 나타나는 절감액


작업 유형별(유휴 및 낮은 사용율), 연결된계정, 지역 및 태그별로 권장 사항을 필터링 할 수도 있습니다.

5. Amazon EC2 리소스 최적화 권장 사항 이해.

In the example below we have a recommendation to downsize the **t2.micro** (1vCPU *for a 2h 24m burst* and 1GB RAM) to a **t2.nano** (1vCPU *for a 1h 12m burst* and 0.5 GB RAM) and save $12 USD per year.

아래 예에서는 **t2.micro**(1vCPU당 2시간24분 버스트 및 1GB RAM의)를 **t2.nano**(1vCPU당 1시간12분 버스트 및 0.5GB RAM)로 축소하고 연간 $12USD를 절약 할 것을 권장합니다.
![Images/ResourceOpt06.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt06.png)


지난 14 일 동안이 인스턴스의 최대 CPU 사용률은 9%에 불과했으며,인스턴스는 86시간 동안 실행되었습니다. 그리고 모두 On-Demand 로 사용되었습니다. 사용 가능한 메모리 정보가 없으므로 Amazon EC2 Resource Optimization은 해당 데이터 포인트를 무시하고 t2.micro에서 사용 가능한 메모리의 절반인 t2.nano로 축소하는 것.을 권장합니다.

제안된 적정 크기 조정 옵션이 유효한지 테스트 할 땐 위험할 수도있고 시간이 낭비될 수도 있습니다. 방금 설치 한 CloudWatch 에이전트를 사용하면이 권장사항의 정확성을 향상시킬 수 있습니다.

이 다른 예에서는 r5.8xlarge(32vCPU 및 256GB RAM)를 r5.4xlarge (16vCPU 및 128GB RAM)로 축소하고 연간 $2,412 USD를 절약 할 것을 권장합니다.
![Images/ResourceOpt07.png](/Cost/200_AWS_Resource_Optimization/Images/ResourceOpt07.png)

이 경우 CPU 및 메모리 정보를 모두 사용할 수 있습니다. 최대 CPU 사용률은 21%이고 메모리는 5%에 ​​불과합니다. 따라서 크기 축소의 경우가 훨씬 강력하고 권장사항에 따라 새 인스턴스 크기의 CPU 및 메모리 사용률을 추정 할 수도 있습니다. 이는 CloudWatch의 과거 사용량 데이터를 기반으로 한 간단한 추정 일 뿐이므로 수정을 실행하기 전에 필요한 모든 부하 테스트를 수행하여 워크로드에 영향을 미치지 않도록해야합니다.

위에서 설명한 것처럼 Amazon EC2 리소스 최적화 로직은 지난 14 일 동안 최대 CPU 사용률이 1%에서 40% 사이 인 인스턴스를 축소하는 것이 좋습니다. 사용 가능한 메모리 정보가있는 경우 Amazon EC2 Resource Optimization은 이제 CPU 및 메모리 최대 활용률이 1 %에서 40% 사이 인 인스턴스의 크기를 줄이는 것을 고려합니다. 메모리 데이터를 사용할 수 있는 경우 유휴 권장사항이 영향을받지 않으므로 지난 14 일 동안 CPU utlization의 1%를 통과하지 못한 EC2 인스턴스는 자동으로 유휴 상태로 플래그가 지정됩니다.