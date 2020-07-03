---
title: "AMAZON EC2 리소스 최적화 CSV 파일을 다운로드하고 검색하기"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 3
pre: "<b>3. </b>"
---

1. **Amazon EC2 Resource Optimization** 레포트를 다운로드합니다:
![Images/ResourceOpt06b.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt06b.png)

2. Amazon EC2 리소스 최적화 권장 사항이없는 경우 아래 파일을 참조로 사용하십시오.
[Sample Amazon EC2 Resource Optimization file (.csv)](/Cost/100_AWS_Resource_Optimization/Code/ENT206-ec2-rightsizing-recommendations-sykang.csv)

3. 먼저 분석에서 너무 작거나 적은 시간 동안 만 실행 된 인스턴스를 제외하겠습니다.
![Images/ResourceOpt07.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt07.png)

**참고** : 계정에서 활성화 한 비용할당태그 수에 따라 아래 스크린 샷과 기본 열 이름, 수식을 일치시키려는 열이 예제와 다를 수 있습니다.


**Recommended Action** 열 오른쪽에 새 열을 삽입하십시오. 첫 번째 행은 `TooSmall` 열의 레이블입니다. 레이블 아래의 각 행에 다음 수식을 붙여 넣습니다.

```
=IF(Q2<25,1,0)
```

이제 *열 Q는 Recommended Instance Type 1 Estimated Savings*이 됩니다. 

이 공식은 한 달에 $25 이상 (또는 $300/년) 이상을 제공하지 못하는 모든 EC2 인스턴스에 "1"을 표시합니다. 조직의 Recommended Instance Type 1 Estimated Savings에 대한 임계 값을 자유롭게 조정하십시오. 잠재적 절감 대신 인스턴스 제품군에 대해 분석을 수행하려는 경우 다음 공식을 사용하여 권장 사항에서 더 작은 인스턴스를 제외 할 수도 있습니다.

```
=IF(N2="Modify",IF(SUMPRODUCT(--(NOT(ISERR(SEARCH({"nano","micro","small","medium"},D2)))))>0,"1","0"),"0")
```
*열 N은 Recommended Action* 그리고 *열 D는 Instance Type*가 되야합니다.

4. 다음으로, 이전세대 (C4, M3 등)에 속하는 EC2 인스턴스에 플래그를 지정합니다. EC2의 적정크기 찾으면서도 사용가능한 최신세대의 타입을 쓸 수 있도록합니다. 새로운 EC2 세대는 성능이 우수하여 올바른 사이징 운동의 성공 변화를 증가 시키며 일반적으로 이전 세대보다 비용이 적게 들며 높은 비용대비 이점을 제공합니다.

![Images/ResourceOpt08.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt08.png)

새로운 열 **Old Gen**을 *Instance Type* 열의 오른쪽에 넣고 아래 공식을 붙여넣습니다:
```
=IF(SUMPRODUCT(--(NOT(ISERR(SEARCH({"c4","c3","c1","m4","m3","m2","m1","r3","r4","i2","cr1","hs1","g2"},D2)))))>0,"1","0")
```
*열 D = Instance Type*

5. 이제 recommendations을 복잡성 감소와 비용 절감을 기준으로 정렬 해 보겠습니다:

**Minimum Effort:** 최소로 필요한 절약 설정


먼저 우리는 절약할만한 가치가 있는 것에 집중하겠습니다. 기준을 $100로 합니다. **Recommended Instance Type 1 Estimated Savings**의  **number filter** 를 **100보다** 크게 맞춥니다. 

### **Group 1:** 유휴 EC2 리소스

필터를 **Recommended Action = "Terminate"** 설정합니다.
데이타를 **Recommended Instance Type 1 Estimated Savings = Largest to smallest**정렬합니다.

CPU 사용률이 1 % 미만인 유휴리소스 또는 인스턴스를 필터링합니다. 이러한 인스턴스는 보통 시작된 후 잊어버린 것이므로 이런곳에서 전체 온디맨드의 잠재적인 비용 절감을 나타낼 수 있습니다.

![Images/ResourceOpt09.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt09.png)

필터링된 결과들은 해당 인스턴스의 어플리케이션 관리자들과 적정 사이즈에대한 토론을 시작하십시오;이러한 인스턴스가 시작된 이유를 이해하기 위해 조사를 수행하고 자원 소유자와 함께 사용상태를 검증하십시오. 그리고 가능하면 종료하십시오.

이 실습에서 제공하는 CSV 파일을 사용하는 경우, 2,534 recommendations을 16개로 필터링하여 매월 $3,458를 절약 할 수 있습니다.


### **Group 2:** 이전 세대 인스턴스

데이터를 **Recommended Actions = “Modify”**, **OldGen = “1”** 과 **TooSmall = “0”** 필터링 합니다.
데이터를 **Recommended Instance Type 1 Projected CPU < 40%** 필터링합니다.
데이터를 **Recommended Instance Type 1 Estimated Savings = Largest to smallest** 정렬합니다.

이것은 이전 세대에 인스턴스 중 활용률이 낮은 리소스(<40 % CPU)에 중점을 두고 동일한 제품군(P 열)내에서 인스턴스 크기를 축소하거나 최신 세대로 현대화 할 수 있습니다.

![Images/ResourceOpt10.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt10.png)

최신세대로 전환하려면 그룹 1에서 식별 된 인스턴스와 비교하여 추가 테스트 시간이 필요할 수 있지만 경우에 따라 비용 절감 및 성능을 극대화 할 수 있습니다.

|          | Linux     | vs new gen | Windows   | vs new gen |          | Linux     | vs new gen | Windows   | vs new gen |
| -------- |:---------:| ----------:|:---------:| ----------:| -------- |:---------:| ----------:|:---------:| ----------:|
| c3.large | $0.105/hr |     up 19% | $0.188/hr |      up 5% | m3.large | $0.133/hr |     up 27% | $0.259/hr |     up 27% |
| c4.large | $0.100/hr |     up 15% | $0.192/hr |      up 7% | m4.large | $0.100/hr |      up 4% | $0.192/hr |      up 2% |
| c5.large | $0.985/hr |         0% | $0.177/hr |         0% | m5.large | $0.096/hr |         0% | $0.188/hr |         0% |

*미국-버지니아 기준 (2019 년 11 월)*

이 실습에서 제공하는 올바른 크기 조정 CSV 파일을 사용하는 경우 *2,534recomendations를 22개로*로 줄이고 잠재적 절감 효과는 매월 *6,362입니다.

### **Group 3:** 최신 세대 인스턴스

데이터를 **Recommended Actions = “Modify”** 과 **OldGen = “0”** 과 **TooSmall = “0”**로 필터링 하세요.
**Recommended Instance Type 1 Projected CPU < 40%** 로 필터링 하세요.
데이터는 **Recommended Instance Type 1 Estimated Savings = Largest to smallest**로 정렬합니다.

현재 가장 최신세대에서 활용률이 낮은 자원을 선택합니다. 잠재적으로 절약 할 수있는 항목을 기준으로 정렬하여 더 큰 절약을 할 수 있는 인스턴스의 우선순위를 정하는 것이 좋습니다.

![Images/ResourceOpt11.png](/Cost/100_AWS_Resource_Optimization/Images/ResourceOpt11.png)


또한 다른 권장 인스턴스유형 (열 U에서 AD까지)을 확인하는 것을 잊지 마십시오:
Amazon EC2 Resource Optimization은 각 권장사항 당 최대 3개의 인스턴스를 추천합니다. 먼저 보수적인 권장사항(첫번째), 그리고 그것보다 더 적극적이고 높은 절감 권장사항(두번째 및 세번째)입니다. 


이 실습에서 제공하는 `올바른 크기 조정 CSV 파일`을 사용하는 경우 *2,534 개의 권장 사항을 22개로* 잠재적 인 절감 효과를 *월별 $4,879.56*로 필터링됩니다.