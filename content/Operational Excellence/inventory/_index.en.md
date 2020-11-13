---
title: "Resource Management"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 52
pre: "<b>5-2. </b>"
---
{{% notice note %}}
AWS Systems Manager는이 실습 전체에서 살펴볼 IT 운영을 지원하는 기능 모음입니다. AWS Systems Manager 인벤토리를 사용하여 하이브리드 환경의 Amazon EC2 인스턴스와 온 프레미스 서버 또는 가상 머신 (VM)에서 운영 체제 (OS), 애플리케이션 및 인스턴스 메타 데이터를 수집 할 수 있습니다. 메타 데이터를 쿼리하여 소프트웨어 정책에 필요한 소프트웨어 및 구성을 실행중인 인스턴스와 업데이트해야하는 인스턴스를 빠르게 이해할 수 있습니다.
{{% /notice%}}

### Systems Manager Prereqs
There are setup tasks and [prerequisites](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html#prereqs-powershell) that must be met before using Systems Manager to manage EC2 instances or on-premises systems in a hybrid environment.

* You must use a supported **operating system**
    * Supported operating systems include versions of Windows, Amazon Linux, Ubuntu Server, RHEL, and CentOS
* The **SSM Agent** must be installed
    * The SSM Agent for Windows also requires PowerShell 3.0 or later to run some [SSM documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-prereqs.html#prereqs-powershell)
* Your EC2 instances must have outbound internet access
* You must access Systems Manager in a **supported region**
* Systems Manager requires **IAM roles**
    * for instances that will process commands
	* for users executing commands

SSM Agent is installed by default on:
* Amazon Linux _base_ AMIs dated 2017.09 and later
* Windows Server 2016 instances
* Instances created from Windows Server 2003-2012 R2 AMIs published in November 2016 or later

#### Inventory
AWS Systems Manager Inventory provides visibility into your Amazon EC2 and on-premises computing environment. You can use Inventory to collect metadata from your managed instances. You can store this metadata in a central Amazon Simple Storage Service (Amazon S3) bucket, and then use built-in tools to query the data and quickly determine which instances are running the software and configurations required by your software policy, and which instances need to be updated. You can configure Inventory on all of your managed instances by using a one-click procedure. You can also configure and view inventory data from multiple AWS Regions and accounts.

#### State Manager
AWS Systems Manager State Manager is a secure and scalable configuration management service that automates the process of keeping your Amazon EC2 and hybrid infrastructure in a state that you define.
<!--
클라우드에서는 애플리케이션 코드에 사용하는 것과 동일한 엔지니어링 원칙을 전체환경에 적용 할 수 있습니다. 전체 워크로드(애플리케이션, 인프라 등)를 코드로 정의하고 코드로 업데이트 할 수 있습니다. 이벤트에 대한 응답으로 작업 프로시저를 트리거하여 작업 프로시저를 스크립팅하고 실행을 자동화 할 수 있습니다. 코드로 작업을 수행하면 인적오류를 줄이고 작업 활동을 일관되게 실행할 수 있습니다.

이 실습에서는 _Infrastructure as Code_ 및 _Operations of Code_ 개념을 다음 활동에 적용합니다.

* 리소스 관리
!-->

Steps:
{{% children  %}}
