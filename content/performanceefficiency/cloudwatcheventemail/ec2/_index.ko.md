---
title: "EC2 Loadtest 진행"
weight: 323
pre: "<b>3. </b>"
---

### EC2의 CPU사용량을 늘린 다음 대시보드를 확인할 것입니다:
---
EC2의 CPU사용량이 많아지면 Autoscaling Group은 자동으로 EC2 Instance 갯수를 증가시킵니다. 그리고 그 변화를 Cloudwatch의 대시보드에서 확인할 것입니다. 

#### Application Load balancer를 통한 Web 접속

1. Cloudformation에서 만든 WellArchitectedFrameworkLabsStack의 Output에 Application Load balancer의 DNS주소가 있습니다. 

    CloudFormation 콘솔로 가기 : https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2
 
1. 실습 Setup에서 만든 WellArchitectedFrameworkLabsStack을 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-stack.png#medium)

1. Output의 `ALBDNS` 값이 Application load balancer의 DNS주소입니다. 상단 탭의 Output을 선택한 후 `ALBDNS`의 값을 복사한 후 웹 브라우저 주소창에 붙여넣습니다.    
    ![CloudwatchDashboard](/images/war/cloudwatch-albdns.png#medium)

1. 다음과 같은 화면을 볼 수 있습니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-ec2.png#medium)
    이 웹서버의 CPU사용률은 0%입니다. 상단의 Load test 버튼을 클릭하면 화면이 전환하면서 EC2의 CPU사용율이 100%로 올라갑니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-ec2-loadtest.png#medium)
    이 화면을 벗어날때까지 CPU사용율은 내려가지 않을 것입니다.  

1. CloudWatch 콘솔로 이동하여 이전에 만든 사용자 대시보드를 확인하겠습니다.

    CloudWatch 콘솔 가기 : https://console.aws.amazon.com/cloudwatch/ 

1. 오른쪽 상단의 **Dashboards**를 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-dashboard.png#medium)

1. 이전에 생성한 `warworkshop-default`를 선택합니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-ec2-dashboard.png#medium)

1. 기본 대시보드의 모니터링 주기는 5분입니다.(이것은 설정에서 변경할 수 있습니다.) 5분 후 새로고침을 하면 100%를 향해 급격하게 변경된 CPUUtilization 래프를 보실 수 있습니다. 그리고 좀 더 시간이 지나면 Autoscaling group으로 4개까지 인스턴스가 확장되어있는 모습을 볼 수 있습니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-change.png)

1. 메일도 확인해봅니다. 이전에 등록한 email로 경보가 온것을 확인할 수 있습니다. 
    ![CloudwatchDashboard](/images/war/cloudwatch-alarm-mail.png)
    휴대폰 번호를 등록했다면 문자도 받으실 수 있습니다. 

Cloudwatch를 활용하여 최적의 성능을 모니터링하세요. 시스템 성능은 시간이 지남에 따라 저하될 수 있습니다. 시스템 성능을 모니터링하여 성능 저하 상태를 식별하고 운영체제 또는 애플리케이션 부하와 같은 내부 또는 외부 요인을 해소하세요. 시스템성능의 변화를 확인할 수 있는 경보를 생성하세요. 

---

#### 모범 사례:
**성능 관련 지표 기록**
    Amazon CloudWatch, 타사 서비스 또는 자체 관리형 모니터링 도구를 사용하여 성능 관련 지표를 기록합니다. 예를 들어 데이터베이스 트랜잭션, 속도가 느린 쿼리, I/O 지연 시간, HTTP 요청 처리량, 서비스 지연 시간 또는 기타 주요 데이터를 기록할 수 있습니다.

**이벤트 또는 인시던트 발생 시의 지표 분석**
    이벤트나 인시던트에 대응하는 과정에서 모니터링 대시보드나 보고서를 사용해 이벤트/인시던트의 영향을 파악하고 진단합니다. 이러한 대시보드나   보고서에서는 필요한 수준의 성능을 제공하지 못하는 워크로드 부분을 파악할 수 있습니다.

**워크로드 성능 측정을 위한 KPI 설정**
    시스템이 예상한 성능을 제공하는지 여부를 나타내는 KPI를 파악합니다. 예를 들어 API 기반 워크로드는 전반적인 성능의 지표로 전체 응답 지연 시간을 사용할 수 있으며, 전자상거래 사이트는 구매 건 수를 KPI로 사용하도록 선택할 수 있습니다.

**모니터링을 사용하여 경보 기반 알림 생성**
    직접 정의한 성능 관련 KPI를 사용해 측정값이 예상 경계를 벗어나면 경보를 자동으로 생성하는 모니터링 시스템을 사용합니다.

**일정한 간격으로 지표 검토**
    주기적인 유지 관리의 일환으로 또는 이벤트나 인시던트 대응 과정에서 수집된 지표를 검토합니다. 이러한 검토를 진행하면 문제를 해결하는 데 반드시 필요했던 지표, 그리고 문제를 확인/해결/방지하는 데 도움이 되었던 지표(추적한 경우)를 파악할 수 있습니다.
    
**사전 모니터링 및 경보 생성**
    KPI를 모니터링 및 알림 시스템과 함께 사용하여 성능 관련 문제를 사전에 해결합니다. 가능한 경우 경보를 사용해 문제 해결을 위한 자동화된 작업을 트리거합니다. 그리고 자동으로 대응할 수 없는 경우에는 대응 가능한 구성 요소로 경보를 에스컬레이션합니다. 예를 들어 필요한 KPI 값을 예측하고 해당 값이 특정 임계값을 초과하는 경우 경보를 생성할 수 있는 시스템이나, KPI가 필요한 값의 범위를 벗어나는 경우 배포를 자동으로 중지하거나 롤백할 수 있는 도구로 경보를 에스컬레이션할 수 있습니다.

