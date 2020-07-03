---
title: "CodeGuru Reviewer"
weight: 40
pre: "<b>4. </b>"
---

{{% notice note %}}
The final code is deploy to the production environment by merging the code that solved the problem to the master via Pull-Request.
{{% /notice %}}

1. The code for production is now complete. The develop branch's code has passed all unit tests, so we will deploy it to the production environment. junier developers usually don't have permission to push directly to the master branch. So, through pull-request, we will go through a code review with a senior developer or a other developer and reflect it in the master. 
There may be other problems you may not know.


1.	Go to the CodeCommit console to create a pull-request.

    Go to CodeCommit: https://console.aws.amazon.com/CodeCommit    

1. Select Repositories in Source and click on `concurrencysample`.
    ![pr1](/images/pc-codecommit-select.png)

1. Select Pull requests from Repositories and click **Create pull request** in the upper right. 
    ![pr2](/images/pc-codecommit-prselect.png)

1. Create pull request, Destination set **master** and Source set **develop** and click the **Compare** button.
    ![pr3](/images/pc-codecommit-createpr.png)

1. Enter `pr concurrencytest` in Title,` for workshop` in Description, and select **Create pull request** on the right.
    ![pr3](/images/pc-codecommit-fin.png)

-[You have created a pull-request. Now let`s see what happens.](/en/codegurupr/solve-awssdk)
