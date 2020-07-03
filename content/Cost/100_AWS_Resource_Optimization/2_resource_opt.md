---
title: "Amazon EC2 리소스 최적화 Recommendations 사용"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---




{{% notice info %}}
**참고**:이 단계를 완료하려면 Amazon EC2 리소스 최적화를 활성화해야합니다. AWS Cost Explorer의 권장 사항 섹션으로 이동하여 Amazon EC2 리소스 최적화를 활성화화세요.
{{% /notice %}}

**Amazon EC2 Resource Optimization**은 추가비용 없이 AWS Cost Explorer에서 올바른 크기 조정 권장 사항을 제공합니다. 이러한 권장 사항은 계정, 리전 및 태그에서 유휴 상태이거나 사용률이 낮은 인스턴스를 식별합니다. 이러한 권장사항을 생성하기 위해 AWS는 기존 EC2리소스 사용량(Amazon CloudWatch 사용) 및 기존 예약공간을 분석하여 비용 절감기회를 찾아냅니다(예:유휴 인스턴스를 종료하거나 활성 인스턴스를 동일한 제품군/세대 내에서 더 저렴한 옵션으로 축소).

1. **AWS Cost Explorer** 로 가겠습니다. 
![Images/ResourceOpt01.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt01.png)

2. 왼쪽 메뉴바에서 **Recommendations**를 선택하세요.
![Images/ResourceOpt2.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt02.png)

3. **Resource Optimization Recommendations** 섹션의 **View All**을 클릭합니다.
![Images/ResourceOpt3.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt03.png)

**Amazon EC2 리소스 최적화**를 활성화하지 않은 경우 첫번째 권장사항을 생성하는 데 최대 24시간이 걸릴 수 있습니다. 일반 또는 billing계정(마스터계정)만 사용하도록 설정할 수 있으며 billing계정(마스터계정)이 설정 페이지(오른쪽 상단)에서 특별히 금지하지 않는 한 기본적으로 연결된 계정과 마스터계정 모두 **Recommendations**에 접근 할 수 있습니다.
![Images/ResourceOpt4.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt04.png)

**recommendations**의 품질을 향상시키기 위해, AWS은 다른 디스크, 메모리 사용율 같은 지표(CloudWatch Agent 필요)를 수집할 수 있습니다. 모든 자원 지표는 익명으로 집계되며 AWS는 모델학습을 위해 이 자료들을 사용할 수 있습니다.
만약 지표 수집과 모델개선을 원치 않으시면 [AWS support ticket](https://docs.aws.amazon.com/awssupport/latest/user/getting-started.html)을 제출할 수 있습니다..더 자세한 정보는 [AWS Service Terms](https://aws.amazon.com/service-terms/)을 참고해주세요..

4. Amazon EC2 리소스 최적화 권장 사항을 활성화했다고 가정하면 권장사항(있는 경우)을 제공하는 화면이 표시됩니다.
![Images/ResourceOpt5.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt05.png)

- **Optimization opportunities** – 사용가능한 권장사항
- **Estimated monthly savings** – 제공된 각 권장사항과 관련된 예상 월별 절감액의 합계
- **Estimated savings (%)** – 권장사항의 인스턴스와 Amazon EC2 비용(온디맨드)과 비교하여 나타나는 절감액

필요에 따라 권장 사항을 필터링 할 수도 있습니다.

5. 나타난 recommendation들의 **view** 를 클릭하면 더 자세한 사항들을 볼 수 있습니다.:
![Images/ResourceOpt6.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt06.png)

