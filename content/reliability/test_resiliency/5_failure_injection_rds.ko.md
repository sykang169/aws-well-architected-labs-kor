---
title: "RDS 장애 주입을 사용하여 안정성 테스트"
menutitle: "RDS 장애 주입"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

### 5.1 RDS 장애 주입 {#rdsfailureinjection}

이 장애 주입은 Amazon RDS DB 인스턴스의 심각한 실패를 시뮬레이션합니다.

1. AWS 콜솔의 RDS 대시보드로 이동합니다: <http://console.aws.amazon.com/rds>

1. RDS 대시보드에서
      * "DB Instances (_n_/40)"를 클릭합니다.
      * 실습환경생성에서 생성한 DB identifier를 클릭합니다. (만약 여러개의 DB가 있다면 **VPC ID**가 이전에 복사한것과 동일한 DB를 선택합니다.)
      * **Configuration**을 클릭합니다.

1. 구성된 값을 확인하십시오. 다음 사항에 유의하십시오.
      * **Info**값이 **Available**인지 확인하세요.
      * RDS DB는 **Multi-AZ**로 구성됩니다. _primary_ DB 인스턴스는와 _standby_ DB 인스턴스는 서로다른 AZ에 위치합니다.
        ![DBInitialConfiguration](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/DBInitialConfiguration.png)

1. RDS 인스턴스의 장애 조치를 수행하려면 Cloud9의 터미널에서 VPC ID를 사용하여 아래 스크립트를 실행시킵니다. \<vpc-id\>는 이전에 기록한 VPC ID로 대체합니다.
```bash
./failover_rds.sh <vpc-id>
```

1. Amazon RDS 데이터베이스가 장애 조치 중임을 나타내는 몇 가지 표시가 포함됩니다: `Failing over mdk29lg78789zt`

### 5.2 RDS 인스턴스 장애에 대한 시스템 응답

서비스가 어떻게 반응하는지보십시오. AWS 시스템이 서비스 가용성을 유지하는데 어떻게 도움이되는지 확인하십시오. 비가용성이 있는지 테스트하고 얼마나 오래 사용할 수 있는지 테스트하십시오.

#### 5.2.1 시스템 가용성

1. RDS 버튼을 클릭할 시, 웹 사이트를 사용할 수 없습니다. 보고 된 몇 가지 오류 :
      * **응답 없음 / 시간초과**: Request was successfully sent to EC2 server, but server no longer has connection to an active database
      요청이 성공적으로 EC2 서버로 전송되었지만, 활성 DB에 연결 할 수 없습니다.
      * **504 Gateway 시간초과**: Amazon Elastic Load Balancer가 서버에서 응답을받지 못했습니다. 응답 할 수 없는 서버를 제거하고 새로운 서버를 추가했지만 새 서버가 아직 초기화를 완료하지 않았고 요청을 수신 할 정상 호스트가 없을 때 발생할 수 있습니다.
      * **502 Bad Gateway**: Amazon Elastic Load Balancer가 서버에서 잘못된 요청을 받았습니다. 이 사이트에 연결할 수 없습니다. 이는 Elastic Load Balancer가 2개의 가용 영역 각각에 노드를 가지고 있고 항상 요청을 처리 할 수 있기 때문입니다.

1. 계속하여 RDS 버튼을 클릭해봅시다.

#### 5.2.2  standby로 장애 조치

1. RDS의 database 콘솔에서 **Configuration** 탭을 누릅니다.
      1. 새로고침을 하고 **Info** 값을 확인합니다. 결과적으로 이것은 장애조치가 완료되면 **Available**상태로 변경될 것입니다.
      1. _primary_ 와 _standby_ 인스턴스의 AZ를 기록합니다. 
      _standby_ 가 아직 _primary_ 책임을 가져오지 않은 상태에서 _primary_가 재시작되었기 때문에 서로의 역활이 스왑됩니다. (RDS 장애조치 후 콘솔이 업데이트 되는데 몇 분 정도 더 걸릴 수 있습니다. 그러나 장애 조치는 완료되었습니다.)


         ![DBPostFailConfiguration](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/DBPostFailConfiguration.png)

      1. AWS RDS 콘솔에서 **Logs & events** 탭을 클릭하고 **Recent events**까지 아래로 스크롤합니다. 아래와 같은 항목이 표시됩니다. 이 경우 장애 조치는 1 분도 채 걸리지 않았습니다.

      > * Mon, 14 Oct 2019 19:53:37 GMT - Multi-AZ instance failover started.
      > * Mon, 14 Oct 2019 19:53:45 GMT - DB instance restarted
      > * Mon, 14 Oct 2019 19:54:21 GMT - Multi-AZ instance failover completed

#### 5.2.3 RDS 장애 주입 - 결론

* AWS RDS 데이터베이스 장애 조치는 1 분도 채 걸리지 않았습니다.

---

#### Resources

* __Learn more__ : 실습 후 다중 AZ 배포를 사용하는 DB 인스턴스의 고 가용성 및 장애 조치 지원에 대한 자세한 내용은 Amazon RDS 용 고 가용성 (다중 AZ)을 참조하십시오.

**Amazon RDS의 고가용성(Multi-AZ)**
> 다음 조건 중 하나가 발생하면 기본 DB 인스턴스가 자동으로 standby로 전환됩니다.

> * 가용 영역 중단
> * 기본 DB 인스턴스가 실패 함
> * DB 인스턴스의 서버 유형이 변경됨
> * DB 인스턴스의 운영 체제에서 소프트웨어 패치가 진행 중입니다.
> * DB 인스턴스의 수동 장애 조치가 Reboot with failover를 사용하여 시작되었습니다.