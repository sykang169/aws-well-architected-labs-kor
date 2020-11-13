---
title: "Again AWS Well-Architected Review using Well-Architected tool"
date: 2020-04-24T11:16:09-04:00
chapter: false
weight: 1

---

{{% notice tip %}}
Review based on pillars with best practices applied.
{{% /notice %}}

1. Log-in AWS console, typing `Well-Architected Tools` in service search bar. 
    you can go to this link : [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).

    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/AWSWAT0.png)


1. In the previously created workload, **Workload for AWS Workshop**, click **AWS Well-Architected Framework**. Then click on each filler to check the question that corresponds to the best practice applied.
 
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-review.png)


1. **operational excellence** as an example. Select **Operational Excellence** at the bottom.
    you can go to this link: [https://console.aws.amazon.com/wellarchitected/](https://console.aws.amazon.com/wellarchitected/).
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational.png)


1. In **Operational Excellence** labs, we managed and monitored **system configuration** and **application** using the **inventory** and **State manager** of **Systems Manager**. In addition, detailed information was organized to gain visibility into compliance status. And, we have configured the **patch manager** to automatically select and deploy operating system and software patches to all EC2 instances. These tasks can be very helpful in monitoring instances deployed in production, reducing defects, and automating patches and configurations.

    Questions that apply to the task **OPS 5. How do you reduce defects, ease remediation, and improve flow into production?** Click.
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational2.png)

1. uncheck **None of these**, click **Use configuration management systems** and **Perform patch management**. You can also click **info** in the question to find out more.
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational3.png)
    There is still more to be improved. Only 2 out of 11 questions were chosen. Being able to choose more questions can reduce your risk. Scroll down to see the various enhancements we can apply.
    ![Select WAT](/watool/100_Walkthrough_of_the_Well-Architected_Tool/Images/wareview-operational4.png)

1. When finished, click **Save and exit** at the top.

1. In this way, other pillars review again the question. To reduce the risk of the AWS Well-Architected Framework, it is necessary to apply a variety of best practices and repeat reviews. In real workloads, review periodically. It eliminates the risk of architecture and creates a scalable and secure architecture. If necessary, you can also conduct a review with a partner or SA.