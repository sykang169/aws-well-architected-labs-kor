---
title: "Cloud9"
weight: 22
pre: "<b>2-1. </b>"

---

### Let's make a Cloud9 instance:

AWS Cloud9 is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. It includes a code editor, debugger, and terminal. Cloud9 comes prepackaged with essential tools for popular programming languages, including JavaScript, Python, PHP, and more, so you don’t need to install files or configure your development machine to start new projects. Since your Cloud9 IDE is cloud-based, you can work on your projects from your office, home, or anywhere using an internet-connected machine. Cloud9 also provides a seamless experience for developing serverless applications enabling you to easily define resources, debug, and switch between local and remote execution of serverless applications. With Cloud9, you can quickly share your development environment with your team, enabling you to pair program and track each other's inputs in real time.

Cloud9 console start: https://console.aws.amazon.com/cloud9

### Create a Workspace 
1. Select **Create Environment** from the menu. 
![cloud902](/images/setup/cloud9-create-environment.png)

1. For 'Name' type `WellArchitectedWorkshop's Cloud9`. For 'Description' type `for Workshop` and click **Next Step**.
![cloud903](/images/setup/cloud9-name-environment.png)

1. Click **Next step** button. 
![cloud904](/images/setup/cloud9-configure-setting.png)

{{% notice warning %}}
Deploy Cloud9 to the default VPC. Cloud9 may shut down if it is deployed in wellarchitectedlabs VPC when performing chasos test for the reliability pillar lab.
{{% /notice %}}

1. Review stage, check Cloud9 enviroment and settings then click **Create Environment**. 
![cloud905](/images/setup/cloud9-review.png)

1. Deployment is finished and you can now use Cloud9.
![cloud905](/images/setup/cloud9-settig-fin.png)


