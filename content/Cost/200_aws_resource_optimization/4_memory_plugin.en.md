---
title: "Cloudwatch Agent Manual Install"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

1. We are now going to manually install the **CloudWatch agent** to start collecting memory data, to start let's go back to the **Amazon EC2 Dashboard**.
	![Images/MemInstall01.png](/cost/200_aws_resource_optimization/Images/AgentInstall01.png)

1. Check EC2 connect infomation which `CloudWatchAgentServerRole` IAM role attached. Select EC2 instance which attached IAM role and Click Connect button.
	![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-connect-ec2.png)

1. Copy connect info in Connect to your instance 
	![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-connect-ec2-info.png)


1. This Command Line need when connect bastionhost. copy to notepad.
	1. EC2 are in PrivateSubnet, they cannot be accessed directly from outside the VPC.Use BastionHost to access EC2. Let's copy the pem key used by EC2 to bastionhost.

	{{% notice warning %}}
	You need to change the permissions of the .pem file. Enter chmod 400 <path.pem> to change the file permissions.
	{{% /notice %}}

1. Enter the command below at the location of the pem key on the terminal.

	```bash
	ssh -i <pem path> <pem filename> ec2-user@<bastionhost-public-dns>:~
	```

	- **pem-path** : Enter the path of the key pair(.pem) used by EC2.
	- **pem-filename** : Enter the name of the pem file to the copy location. (Enter the same as before.)
	- **bastionhost-public-dns** : Click on CloudFormation's output and you can see bastionhostdns. Or, you can check the public dns of bastionhost of the ec2 instance.

		- *Find it on the EC2 dashboard*
			![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bastionhost-ec2-dns.png)

		- *Find it on Cloudformation output*
			![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bastionhsotdns.png)

	Example) Please enter in the form below.

	```bash
	scp -i ./warworkshopkey.pem warworkshopkey.pem ec2-user@ec2-3-210-197-135.compute-1.amazonaws.com:~
	```

1. Upload is completed with the following message.
	![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-install-key.png)

1. Open **EC2 Dashboard**, go to **Instances** and Click EC2 instance which name **BastionHost**. 
	Click **Connect** button.
	![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bstionhost.png)

1. Click **browser-based SSH connection tool** in the newly opened dialog box, click ʻec2-user` as the User name, and click Connect.
	![Images/MemInstall04.png](/cost/200_aws_resource_optimization/Images/AgentInstall04.png)
	![Images/MemInstall05.png](/cost/200_aws_resource_optimization/Images/AgentInstall05.png)

1. If you type ls in the terminal, you can check the copied pem.
	![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-pem.png)

1. You can access the EC2 by pasting the copied EC2 connection information. You can check the changed ip of ec2-user in terminal shell Now, let's install Cloudwatch-agent in earnest.
	![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-ec2.png)

1. Download the **Amazon Cloudwatch** agent package, the instructions below are for Amazon Linux, for other OS please check [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html)

	```
	wget https://s3.amazonaws.com/amazoncloudwatch-agent/linux/amd64/latest/AmazonCloudWatchAgent.zip
	```

	![Images/MemInstall06.png](/cost/200_aws_resource_optimization/Images/AgentInstall06.png)

1. Unzip and Install the package

	```
	unzip AmazonCloudWatchAgent.zip
	sudo ./install.sh
	```

	![Images/MemInstall07.png](/cost/200_aws_resource_optimization/Images/AgentInstall07.png)

1. Configure the AmazonCloudWatchAgent profile

	Before running the CloudWatch agent on any servers, you must create a CloudWatch agent configuration file, which is a JSON file that specifies the metrics and logs that the agent is to collect, including custom metrics. You can create it by using the wizard or by writting it yourself from scratch. Any time you change the agent configuration file, you must then restart the agent to have the changes take effect.

	The wizard can autodetect the credentials and AWS Region to use if you have the AWS credentials and configuration files in place. For more information about these files, see [Configuration and Credential Files](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html) in the *AWS Systems Manager User Guide* and the [AWS documentation page](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-cloudwatch-agent-configuration-file.html).

	For now, let's start the CloudWatch agent configuration file wizard executing the command below at the selected EC2 instance.

	```
	sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
	```

	![Images/MemInstall08.png](/cost/200_aws_resource_optimization/Images/AgentInstall08.png)

	For this lab we want to keep the following structure:

	| CloudWatch Agent Configutation File Wizard                  | Parameter    |
	| ----------------------------------------------------------- |:------------:|
	| On which OS are you planning to use the agent?              | 1. Linux     |
	| Are you using EC2 or On-Premises hosts?                     | 1. EC2       |
	| Which user are you planning to run the agent?               | 2. cwagent   |
	| Do you want to turn on StatsD daemon?                       | 2. No        |
	| Do you want to monitor metrics from CollectD?               | 2. No        |
	| Do you want to monitor any host metrics?                    | 1. Yes       |
	| Do you want to monitor cpu metrics per core?                | 2. No        |
	| Do you want to add ec2 dimensions?                          | 1. Yes       |
	| Would you like to collect your metrics at high resolution?  | 4. 60s       |
	| Which default metrics config do you want?                   | 1. Basic     |
	| Are you satisfied with the above config?                    | 1. Yes       |
	| Do you have any existing CloudWatch Log Agent?              | 2. No        |
	| Do you want to monitor any log files?                       | 2. No        |
	| Do you want to store the config in the SSM parameter store? | 2. No        |

	The CloudWatch Agent config file should look like the following:

	```
	{
		"agent": {
				"metrics_collection_interval": 60,
				"run_as_user": "cwagent"
		},
		"metrics": {
				"append_dimensions": {
					"AutoScalingGroupName": "${aws:AutoScalingGroupName}",
					"ImageId": "${aws:ImageId}",
					"InstanceId": "${aws:InstanceId}",
					"InstanceType": "${aws:InstanceType}"
				},
				"metrics_collected": {
					"disk": {
						"measurement": [
							"used_percent"
					],
					"metrics_collection_interval": 60,
						"resources": [
								"*"
					]
				},
				"mem": {
						"measurement": [
							"mem_used_percent"
						],
						"metrics_collection_interval": 60
				}
			}
		}
	}
	```

1. Start the CloudWatch Agent

	```
	sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
	```

	![Images/MemInstall09.png](/cost/200_aws_resource_optimization/Images/AgentInstall09.png)

	It may take up to 5 minutes for the metrics to become available, go back to the **Amazon CloudWatch** console page, under the **Metrics** session to validate that you are getting Memory information.

	Click **CWAgent**:
	![Images/MemInstall10.png](/cost/200_aws_resource_optimization/Images/AgentInstall10.png)

	Click **ImageID,InstanceID,InstanceType**:
	![Images/MemInstall11.png](/cost/200_aws_resource_optimization/Images/AgentInstall11.png)

	Select the **Instance** from the list below:
	![Images/MemInstall12.png](/cost/200_aws_resource_optimization/Images/AgentInstall12.png)

	You have now completed the CloudWatch agent installation and will be able to monitor on Amazon CloudWatch the memory utilization of that instance.

