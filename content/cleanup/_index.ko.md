---
title: "실습 리소스 정리"
weight: 60
pre: "<b>6. </b>"
---

{{% notice warning %}}
이 실습을 마치면 사용한 AWS 계정에 비용이 추가로 발생하지 않도록 사용한 리소스를 삭제해야 합니다. 리소스를 삭제하기 위해 기존의 **Administrator** (관리자) 계정으로 AWS 관리 콘솔에 로그인 합니다.
{{% /notice %}}

AWS CloudFormation을 사용하여 생성한 모든 AWS 리소스를 정리합니다. 사전에 CloudFormation에서 만든 리소스에서 변경 사항이 있는 것들을 삭제합니다. 
빌드 결과물이 저장되어있는 S3 Bucket과 CodeGuru를 위해 셋팅한 IAM, CodeGuru Profiler Group, CodeGuru Reviewer Associate, CodeBuild Report를 삭제합니다. 

1. [S3](/ko/cleanup/s3)
1. [IAM Role](/ko/cleanup/iam)
1. [CodeGuru Reviewr](/ko/cleanup/codeguru-associate)
1. [CodeGuru Profiler](/ko/cleanup/codeguru-profiler)
1. [CloudFormation](/ko/cleanup/cloudformatiomn)
1. [Codebuild Report Group](/ko/cleanup/codebuild)
1. [Cloud9](/ko/cleanup/cloud9)