---
title: "EC2, RD와 AZ의 복원력 테스트"
menutitle: "EC2, RD와 AZ의 복원력 테스트"
description: "Use code to inject faults simulating EC2, RDS, and Availability Zone failures. These are used as part of Chaos Engineering to test workload resiliency"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 1
tags:
  - test_resiliency
---

{{< rawhtml >}}
<center>
<video width="600" height="450" controls>
  <source src="https://d3h9zoi3eqyz7s.cloudfront.net/Reliability/Videos/chaos1.mp4" type="video/mp4">
</video>
</center>
{{< /rawhtml >}}

## Authors

* Rodney Lester, Senior Solutions Architect Manager, AWS Well-Architected
* Adrian Hornsby, Principal Tech Evangelist, AWS
* Seth Eliot, Principal Reliability Solutions Architect, AWS Well-Architected
* Seyong Kang, Solutions Architect

## Introduction

이 실습의 목적은 애플리케이션에 장애 모드를 삽입하여 구현이 장애에 대해 탄력적인지 확인하기 위해 테스트를 사용하는 기본 사항을 가르치는 것입니다. 이것은 FMEA (고장 모드 엔지니어링 분석)를 실행하는 회사에 익숙한 개념 일 수 있습니다. 또한 이러한 실패 주입을 사용하여 워크로드 탄력성에 대한 가설을 테스트하는 Chaos Engineering의 핵심 구성 요소이기도합니다. AWS가 제공하는 주요 기능 중 하나는로드 상태에서 프로덕션 규모로 시스템을 테스트하는 기능입니다.

장애를 설계하는 것만으로는 충분하지 않으며 장애로 인해 시스템이 작동하는 방식을 이해하고 있는지 테스트해야합니다. 이러한 테스트를 수행하면 실패를 조사하는 방법에 대한 플레이 북을 만들 수 있습니다. 근본 원인을 식별하기위한 플레이 북을 만들 수도 있습니다. 이러한 테스트를 정기적으로 수행하면 장애에 탄력적이지 않은 애플리케이션의 변경 사항을 식별하고 예상치 못한 장애에 조용하고 예측 가능한 방식으로 대응하는 기술을 만들 수 있습니다.

이 실습에서는 역방향 프록시 (Application Load Balancer), Amazon Elastic Compute Cloud (EC2)의 웹 애플리케이션 및 Amazon Relational Database Service (RDS)를 사용하는 MySQL 데이터베이스가있는 3 계층 리소스를 배포합니다. 또한 동일한 스택을 다른 리전에 배포하는 옵션도 있으므로 더 간단한 구성 요소 장애 테스트에서 시뮬레이션 된 AWS 리전 장애 하에서 장애 테스트로 진행할 수 있습니다.

The skills you learn will help you build resilient workloads in alignment with the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

## Goals:

* 공통 개발 및 스크립팅 언어로 예제를 제공하여 복원력 테스트 구현에 대한 두려움을 줄입니다.
* EC2 인스턴스의 복원력 테스트
* RDS 다중 AZ 인스턴스의 복원력 테스트
* 가용 영역 장애를 사용한 복원력 테스트
* S3 객체의 복원력 테스트
* 이러한 테스트를 사용하여 복원력을 구현하는 방법 알아보기
* 인프라 내에서 장애가 발생하는 원인에 대해 생각하는 방법 알아보기
* 일반적인 AWS 서비스가 MTTR (평균 복구 시간)을 줄이는 방법 알아보기


## Steps:
{{% children /%}}

