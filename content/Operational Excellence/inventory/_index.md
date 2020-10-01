---
title: "리소스 중앙 관리"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 52
pre: "<b>5-2. </b>"
---
{{% notice note %}}
AWS Systems Manager는이 실습 전체에서 살펴볼 IT 운영을 지원하는 기능 모음입니다. AWS Systems Manager 인벤토리를 사용하여 하이브리드 환경의 Amazon EC2 인스턴스와 온 프레미스 서버 또는 가상 머신 (VM)에서 운영 체제 (OS), 애플리케이션 및 인스턴스 메타 데이터를 수집 할 수 있습니다. 메타 데이터를 쿼리하여 소프트웨어 정책에 필요한 소프트웨어 및 구성을 실행중인 인스턴스와 업데이트해야하는 인스턴스를 빠르게 이해할 수 있습니다.
{{% /notice%}}

### Systems Manager 사전 요구 사항
Systems Manager를 사용하여 **하이브리드 환경**에서 **EC2 인스턴스** 또는 **온 프레미스 시스템**을 관리하기 전에 충족해야하는 [설정 작업 및 사전 요구 사항](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html#prereqs-powershell)이 있습니다.

* **지원되는 운영 체제**를 사용해야합니다
   * 지원되는 운영 체제에는 Windows, Amazon Linux, Ubuntu Server, RHEL 및 CentOS 버전이 포함됩니다
* **SSM 에이전트가 설치**되어 있어야합니다
   * 윈도우 환경의 SSM 에이전트를 사용하는 경우는 PowerShell 3.0이상의 버전이 필요하고 낮은 버전의 경우는 [SSM documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html#prereqs-powershell)를 확인해주세요.
   * 실습은 CloudFormation의 경우 EC2는 privatesubnet에 위치해있습니다. System Manager가 public network를 통해 EC2에 접근하는 것이 불가능하기 때문에 VPC endpoint가 필요합니다. 
* **지원되는 리전**의 Systems Manager에 액세스해야합니다
* Systems Manager에는 **IAM 역할**이 필요합니다

다음 인스턴스들에는 SSM 에이전트가 기본적으로 설치되어 있습니다.
* 2017년 9월 이후의 Amazon Linux _base_ AMI
* Windows Server 2016 인스턴스
* 2016년 11월 이후에 배포된 Windows Server 2003-2012 R2 AMI에서 생성된 인스턴스


#### 인벤토리
AWS Systems Manager는 인스턴스와 인스턴스에 설치된 소프트웨어에 대한 정보를 수집하여 시스템 구성과 설치된 애플리케이션에 대해 이해할 수 있도록 지원합니다. 애플리케이션, 파일, 네트워크 구성, Windows 서비스, 레지스트리, 서버 역할, 업데이트, 기타 시스템 속성을 수집할 수 있습니다. 수집된 데이터를 통해 애플리케이션 자산을 관리하고, 라이선스를 추적하고, 파일 무결성을 모니터링하고, 기존 설치 프로그램으로 설치하지 않은 애플리케이션을 찾을 수 있습니다.

#### 상태 관리자
AWS Systems Manager는 Amazon EC2 또는 온프레미스 인스턴스의 구성을 일관되게 유지하는 데 도움이 되는 구성 관리 기능을 제공합니다. Systems Manager에서는 서버 구성, 안티바이러스 정의, 방화벽 설정 등과 같은 구성 세부 정보를 제어할 수 있습니다. AWS Management Console을 통해 서버의 구성 정책을 정의하거나, GitHub 또는 Amazon S3 버킷에서 직접 기존 스크립트, PowerShell 모듈 또는 Ansible 플레이북을 사용할 수 있습니다. Systems Manager는 정의한 시간과 빈도에 따라 인스턴스 전체에 구성을 자동으로 적용합니다. 언제든 Systems Manager를 쿼리하여 인스턴스 구성 상태를 볼 수 있으므로, 규정 준수 상태에 대한 온디맨드 가시성이 제공됩니다.
<!--
클라우드에서는 애플리케이션 코드에 사용하는 것과 동일한 엔지니어링 원칙을 전체환경에 적용 할 수 있습니다. 전체 워크로드(애플리케이션, 인프라 등)를 코드로 정의하고 코드로 업데이트 할 수 있습니다. 이벤트에 대한 응답으로 작업 프로시저를 트리거하여 작업 프로시저를 스크립팅하고 실행을 자동화 할 수 있습니다. 코드로 작업을 수행하면 인적오류를 줄이고 작업 활동을 일관되게 실행할 수 있습니다.

이 실습에서는 _Infrastructure as Code_ 및 _Operations of Code_ 개념을 다음 활동에 적용합니다.

* 리소스 관리
!-->

Steps:
{{% children  %}}
