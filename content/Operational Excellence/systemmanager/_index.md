---
title: "AWS System Manager"
chapter: false
pre: "<b>5-1. </b>"
weight: 51
---
{{% notice note %}}
[AWS Systems Manager](https://aws.amazon.com/systems-manager/features/)는 IT 운영에서 활용할 수 있는 [많은 기능들을 제공](https://aws.amazon.com/ko/systems-manager/features/)합니다. EC2 뿐만 아니라 하이브리드 환경도 지원하므로 AWS Systems Manager를 사용하면 AWS와 온프레미스 데이터 센터에서 실행되는 서버를 모두 단일 인터페이스에서 관리할 수 있습니다. Systems Manager는 서버에 설치된 경량 에이전트와 안전하게 통신하여 관리 작업을 수행합니다. 
AWS Systems Manager로 EC2 인스턴스 및 [하이브리드 환경](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-managedinstances.html)을 관리하기 위해 필요한 [요구 사항](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html) 및 [필요한 설정](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-setting-up.html)에 대한 상세 내용은 문서를 참고합니다.
{{% /notice%}}

[AWS Systems Manager의 추가 사용 요금은 없습니다.](https://aws.amazon.com/systems-manager/pricing/) AWS Systems Manager에서 관리하거나 생성한 기본 AWS 리소스(예: Amazon EC2 인스턴스 또는 Amazon CloudWatch 지표)에 대해서 사용한 만큼만 비용을 지불합니다. 최소 비용과 사전 약정은 없습니다.


### 운영 우수성과 AWS System Manager
{{% notice note %}} 여러 AWS 서비스의 운영 데이터를 중앙집중화하고 AWS 리소스 전체에서 작업을 자동화할 수 있습니다. 애플리케이션, 애플리케이션 스택의 다양한 계층 또는 프로덕션 환경 대 개발 환경 같은 논리적 리소스 그룹을 만들 수 있습니다. Systems Manager에서는 리소스 그룹을 선택하여 리소스 그룹의 최근 API 작업, 리소스 구성 변경, 관련 알림, 운영 경보, 소프트웨어 인벤토리, 패치 규정 준수 상태를 볼 수 있습니다. 운영상 필요에 따라 각 리소스 그룹에 대한 조치를 취할 수도 있습니다. 상세 내용은 링크를 참고합니다. {{% /notice%}}

#### 인벤토리
AWS Systems Manager는 인스턴스와 인스턴스에 설치된 소프트웨어에 대한 정보를 수집하여 시스템 구성과 설치된 애플리케이션에 대해 이해할 수 있도록 지원합니다. 애플리케이션, 파일, 네트워크 구성, Windows 서비스, 레지스트리, 서버 역할, 업데이트, 기타 시스템 속성을 수집할 수 있습니다. 수집된 데이터를 통해 애플리케이션 자산을 관리하고, 라이선스를 추적하고, 파일 무결성을 모니터링하고, 기존 설치 프로그램으로 설치하지 않은 애플리케이션을 찾을 수 있습니다.


#### 상태 관리자
AWS Systems Manager는 Amazon EC2 또는 온프레미스 인스턴스의 구성을 일관되게 유지하는 데 도움이 되는 구성 관리 기능을 제공합니다. Systems Manager에서는 서버 구성, 안티바이러스 정의, 방화벽 설정 등과 같은 구성 세부 정보를 제어할 수 있습니다. AWS Management Console을 통해 서버의 구성 정책을 정의하거나, GitHub 또는 Amazon S3 버킷에서 직접 기존 스크립트, PowerShell 모듈 또는 Ansible 플레이북을 사용할 수 있습니다. Systems Manager는 정의한 시간과 빈도에 따라 인스턴스 전체에 구성을 자동으로 적용합니다. 언제든 Systems Manager를 쿼리하여 인스턴스 구성 상태를 볼 수 있으므로, 규정 준수 상태에 대한 온디맨드 가시성이 제공됩니다.

#### 패치 관리자
AWS Systems Manager는 대규모 Amazon EC2 그룹 또는 온프레미스 인스턴스 전체에서 자동으로 운영 체제 및 소프트웨어 패치를 선택 및 배포하도록 지원합니다. 패치 기준선을 통해 운영 체제 또는 높은 심각도 패치 등 선택한 카테고리의 패치를 자동 승인하도록 규칙을 설정할 수 있고, 이러한 규칙을 무시하고 자동 승인 또는 거부할 패치 목록을 지정할 수 있습니다. 또한, 미리 설정된 시간에만 패치가 적용되도록 패치에 대한 유지 관리 기간을 예약할 수 있습니다. Systems Manager는 소프트웨어를 최신으로 유지하고 규정 준수 정책을 충족하는 데 도움이 됩니다.

#### 유지 관리 기간
AWS Systems Manager를 사용하면 인스턴스 전체에서 관리 및 유지 보수 작업을 실행할 시간대를 예약할 수 있습니다. 따라서 패치 및 업데이트를 설치하거나 다른 구성 변경 사항을 적용할 편리하고 안전한 시간을 선택할 수 있으므로 서비스와 애플리케이션의 가용성과 안정성을 향상할 수 있습니다.

#### Run Command
AWS Systems Manager에서는 서버에 로그인하지 않고 대규모로 인스턴스를 원격으로 안전하게 관리할 수 있는 기능을 제공하므로, 배스천 호스트, SSH 또는 원격 PowerShell이 필요 없습니다. 레지스트리 편집, 사용자 관리, 소프트웨어 및 패치 설치와 같은 일반적인 관리 작업을 인스턴스 그룹 전체에서 자동화하는 간단한 방법을 제공합니다. AWS Identity and Access Management(IAM)와의 통합을 통해 세분화된 권한을 적용하여 사용자가 인스턴스에 수행할 수 있는 작업을 제어할 수 있습니다. Systems Manager가 수행한 모든 작업이 AWS CloudTrail에 기록되기 때문에 환경 전체의 변경 사항을 감사할 수도 있습니다.

* 이 외에도 AWS System Manager는 여러 기능을 제공합니다. 상세한 사항은 [링크](https://aws.amazon.com/ko/systems-manager/features/)를 참고합니다. 