---
title: "CloudFront 구성 - EC2 또는 Load Balancer"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---

1. CloudFront 콜솔로 이동합니다: https://console.aws.amazon.com/cloudfront/home.
1. 콘솔 대시보드에서 **Create Distribution**를 클릭합니다.
  ![waf-1](/images/security/security-cloudfront-start.png)

1. Web 섹션의 **Get Started**를 클릭합니다.
  ![waf-1](/images/security/security-cloudfront-start2.png)
 
1. 새로운 브라우저를 띄운 다음 **CloudFormation**으로가서 **MasterAccount**의 **Output**탭을 클릭하여 ALBDNS값을 복사합니다: https://console.aws.amazon.com/cloudformation/  
  ![waf-1](/images/security/security-cloudfront-start3.png)
 
1. **Origin Settings**의 **Origin Domain Name**에 복사한 Application Load Balancer의 DNS주소를 입력합니다. 자동으로 **Origin ID**가 입력됩니다. 
  ![waf-1](/images/security/security-cloudfront-start4.png)
 
1. 스크롤을 내리면 **Distribution Setting**의 **AWS WAF Web ACL**에서 이전에 만든 `well-architected-cf-waf-acl`를 선택할 수 있습니다. 
  ![waf-1](/images/security/security-cloudfront-start5.png)
  맨 아래 Create Distribution을 클릭하여 CloudFront 셋팅을 완료합니다. 

1. 이제 CloudFront의 메인화면에서 배포중인 CloudFront의 **배포중인 상태**를 **확인**`(1)`하실 수 있습니다. 그리고 엣지로 배포가 완료되면 새로운 **Domain Name**`(2)`으로 접속이 가능해집니다.  
  ![waf-1](/images/security/security-cloudfront-start6.png)
