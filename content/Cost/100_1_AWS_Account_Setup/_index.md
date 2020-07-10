---
title: "AWS 계정 설정: AWS Organization & AWS SSO "
#menutitle: "Lab #1"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 1
pre : "<b>4-1. </b>"
---

## Authors
- Nathan Besh, Cost Lead Well-Architected
- +Seyong Kang 


## 소개
이 실습에서는 계정을 구성하고 비용 최적화 작업을 준비하는 단계를 안내합니다. 초기 계정 구조를 생성 및 설정하고 청구 정보에 액세스 할 수 있으며 비용최적화 팀을 만듭니다. 이를 통해 Well-Architected 비용최적화 워크샵을 완료하고 Well-Architected Framework에 따라 워크로드를 최적화 할 수 있습니다.


## Goals
- 계정 구조 구현
- 결제 서비스 구현
- 자세한 비용과 사용정보 사용
- 비용 최적화 팀 생성 및 연동

## 준비사항
- 여러개의 AWS 계정 생성 (최소 3개)
    - 마스터 계정
    - 비용최적화 팀 계정


## 필요한 권한
- 마스터와 멤버 계정에 대한 루트유저와 관리자 권한

## 비용
- https://aws.amazon.com/aws-cost-management/pricing/
- 다양한 비용이 발생합니다.
- 비용탐색기 : 1,000 사용 레코드 당 $0.01 
- S3: CUR 파일의 저장비용, S3 의 가격정책은 https://aws.amazon.com/s3/pricing/ 참고하세요.
- Sub 계정의 경우 예상비용은 $5미만.
## 완료 소요 시간
- Lab은 최소 30분 정도 시간이 걸립니다. 

## Steps:
{{% children  %}}

