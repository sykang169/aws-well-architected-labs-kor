---
title: "EC2 적정크기 찾기 (MEM)"
#menutitle: "Lab #3"
date: 2020-04-24T11:16:08-04:00
chapter: false
weight: 7
pre : "<b>4-2. </b>"
---
## Authors
- Jeff Kassel, AWS Technical Account Manager
- Arthur Basbaum, AWS Cloud Economics
- +Seyong Kang, Solutions Architect

## 소개
이 실습에서는 CloudWatch 에이전트를 설치하여 메모리 사용률 (GB 소모량)을 수집하고 AWS Resource Optimization를 사용하여 EC2 올바른 크기 조정연습에 새로운 데이터 포인트가 어떻게 도움이 되는지 분석하는 단계를 안내합니다.
 
## Goals
- Amazon CloudWatch에서 CPU, 네트워크 및 디스크 사용량과 같은 지표를 확인하는 방법 알아보기
- Amazon CloudWatch에서 사용자 지정지표를 통해 메모리데이터를 설치 및 수집하는 방법에 대해 알아봅니다.
- AWS 리소스 최적화를 활성화하고 새로운 데이터 포인트(메모리)가 권장 사항에 미치는 영향을 관찰합니다.

## 준비사항
- 마스터 계정의 루트 사용자
- AWS Resource Optimization의 at *AWS Cost Explorer > Recommendations* 을 활성화합니다.

## 권한 요구사항
- 마스터 계정의 루트 사용자 액세스

## Steps:
{{% children  %}}

## 모범 사례 점검표
- [ ] Amazon CloudWatch를 시작하고 EC2 인스턴스의 평균 CPU, 디스크 및 네트워크 사용량을 관찰하십시오
- [ ] EC2 인스턴스에 CloudWatch 에이전트를 수동으로 설치하여 메모리 사용률을 추적합니다.
- [ ] 추가 데이터 포인트가있을 때 AWS 리소스 최적화에 미치는 영향을 관찰하십시오 (메모리 사용률)
