---
title: "CloudFront Config - EC2 or Load Balancer"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 2
pre: "<b>2. </b>"
---

1. Open AWS CloudFront Console: https://console.aws.amazon.com/cloudfront/home.
1. Click **Create Distribution** button.
  ![waf-1](/images/security/security-cloudfront-start.png)

1. in Web section, Click **Get Started** button.
  ![waf-1](/images/security/security-cloudfront-start2.png)
 
1. Open new browser, open **CloudFormation** console: https://console.aws.amazon.com/cloudformation/
And click **MasterAccount** stack`s **Output** tab and copy value of ALBDNS  
  ![waf-1](/images/security/security-cloudfront-start3.png)
 
1. Enter the DNS address of the Application Load Balancer copied to **Origin Domain Name** in Origin Settings. **Origin ID** will be entered automatically. 
  ![waf-1](/images/security/security-cloudfront-start4.png)
 
1. If you scroll down, you can select the `well-architected-cf-waf-acl` you created earlier in the AWS WAF Web ACL in **Distribution Setting**.
  ![waf-1](/images/security/security-cloudfront-start5.png)
  Click **Create Distribution** at the bottom to complete CloudFront setup.

1. Now you can check the distribution status of CloudFront being **in progress** `(1)` on the main screen of CloudFront. And when the deployment to the edge is completed, you can access the new **Domain Name** `(2)`.
  ![waf-1](/images/security/security-cloudfront-start6.png)
