---
title: "CodeGuru AWSSDK"
weight: 42
pre: "<b>4-2. </b>"
---

1. let`s check what kind of code review has doing in pull-request.(almost wait 5min.)

1. Go to CodeCommit's console: https://console.aws.amazon.com/codecommit
    
1. Select Repositories of Source on the left and click concurrencysample.
    ![pr1](/images/pc-codecommit-select.png)

1. Select `pr-concurrencytest` for Pull requests of Repositories in the left source.
    ![pr2](/images/pr-solve-select.png)

1. If CodeCommit and Repository are connected, the following screen will appear. Select Activity at the top.
    ![pr3](/images/pr-solve-comment.png)

1. The code review comment was attached to the code that I thought had no problems.
    ![pr4](/images/pr-awssdk2.png)

1. Temporary Security Credentials rather than long-term Security Credentials such as AccessKey and SceretKey. CodeGuru tells you how and how to use the AWS SDK secure. These are things that cannot be found in simple unit tests or experience!

1. You can evaluate whether CodeGuru's suggestions are really useful through feedback. These can contribute to better CodeGuru comments.


-[And.. let`s see more....](/en/codegurupr/solve-concurrency)    