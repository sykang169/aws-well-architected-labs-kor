---
title: "AWS WAF 구성"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1
pre: "<b>1. </b>"
---


1. AWS WAF 콘솔로 이동합니다: https://console.aws.amazon.com/wafv2/homev2

1. 왼쪽 메뉴에서 **Getting started**를 선택하고 오른쪽 **Create web ACL**를 클릭합니다.
  ![waf-1](/images/security/security-waf-start.png)

1. 먼저 하단의 Resource type을 CloudFront distributions로 설정합니다. 그리고 Web ACL details에 각각 항목에 맞게 입력합니다. 
  - Name : `well-architected-cf-waf-acl`
  - Description : `for well-architected CF WAF`  
  ![waf-1](/images/security/security-waf-start2.png)
  그리고 계속 다음을 선택하고 **Create web ACL**을 클릭하여 Web ACL 생성을 완료합니다.

