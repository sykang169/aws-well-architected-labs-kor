---
title: "Cloudwatch Agent 수동 설치"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>4. </b>"
weight: 4
---

1. 이제 수동으로 **CloudWatch agent** 설치한 후 메모리 데이타 수집을 시작할 것입니다.**Amazon EC2 Dashboard**로 갑니다.
![Images/MemInstall01.png](/cost/200_aws_resource_optimization/Images/AgentInstall01.png)

2. `CloudWatchAgentServerRole` IAM role을 연결한 EC2인스턴스의 접속정보를 복사하겠습니다. IAM role을 연결한 인스턴스를 선택하고 Connect를 누릅니다.
![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-connect-ec2.png)

3. Connect to your instance 대화창에서 example에 있는 접속정보를 복사합니다.  
![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-connect-ec2-info.png)

4. 이 정보는 bastionhost에서 접속할때 필요하니 어딘가 복사해 둡니다.

5. Loadbalancer와 연결된 EC2는 PrivateSubnet에 있기 때문에 VPC외부에서는 직접 접근이 불가능합니다. BastionHost를 이용해 EC2에 접근하도록 하겠습니다. EC2가 사용하는 pem 키를 bastionhost로 복사하겠습니다.

{{% notice warning %}}
.pem 파일의 권한을 변경해야합니다. chmod 400 <path.pem> 을 입력하여 파일권한을 변경합니다.
{{% /notice %}}

6. 아래 명령어를 터미널의 pem키가 있는 위치에서 입력합니다.

```bash
ssh -i <pem path> <pem filename> ec2-user@<bastionhost-public-dns>:~
```

- **pem-path** : CloudFormation은 생성할때 만든 EC2 key pair .pem의 경로를 입력합니다.
- **pem-filename** : 복사할 위치의 pem 파일의 이름을 입력합니다. (기존과 동일하게 입력합니다.)
- **bastionhost-public-dns** : CloudFormation의 output을 클릭하면 bastionhostdns를 알 수 있습니다. 또는 ec2인스턴스의 bastionhost의 public dns를 확인하셔도 됩니다. 

	- *EC2 dashboard에서 찾기*
		![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bastionhost-ec2-dns.png)

	- *Cloudformation output에서 찾기*
		![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bastionhsotdns.png)

예) 아래와 같은 형태로 입력하세요.

```bash
scp -i ./warworkshopkey.pem warworkshopkey.pem ec2-user@ec2-3-210-197-135.compute-1.amazonaws.com:~
```

7. 아래와 같이 메세지와 함께 업로드가 완료됩니다. 
![/images/war-cost/cloudwatch-agent-connect-ec2.png](/images/war-cost/cloudwatch-agent-install-key.png)

8. 이제 **EC2 Dashboard**로 가서 왼쪽 메뉴 리스트 중 **Instances** 를 클릭하고 **BastionHost**이름의 EC2인스턴스를 클릭합니다. 
상단의 **Connect**를 클릭합니다.
![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-bstionhost.png)

9. 새로 뜬 대화창의 **browser-based SSH connection tool**를 클릭하고 User name에 `ec2-user` 그리고 Connect를 클릭합니다.
![Images/MemInstall04.png](/cost/200_aws_resource_optimization/Images/AgentInstall04.png)
![Images/MemInstall05.png](/cost/200_aws_resource_optimization/Images/AgentInstall05.png)

10. Terminal에 ls를 입력하면 복사된 pem을 확인하실 수 있습니다. 
![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-pem.png)

11. 이제 아까 복사해둔 EC2의 접속정보를 붙여넣어 해당 EC2에 접속하도록하겠습니다. 터미널 쉘의 변경된 ec2-user의 ip를 확인할 수 있습니다. 이제 본격적으로 Cloudwatch-agent를 설치하도록 하겠습니다. 
![/images/war-cost/cloudwatch-agent-bstionhost.png](/images/war-cost/cloudwatch-agent-ec2.png)

12. **Amazon Cloudwatch** agent 패키지를 다운로드합니다. 해당 링크는 Amazon Linux를 위한 패키지이며, 다른 os는 [여기](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html)서 확인하세요.

```
wget https://s3.amazonaws.com/amazoncloudwatch-agent/linux/amd64/latest/AmazonCloudWatchAgent.zip
```

![Images/MemInstall06.png](/cost/200_aws_resource_optimization/Images/AgentInstall06.png)

13. install package의 압축을 해제합니다.

```
unzip AmazonCloudWatchAgent.zip
sudo ./install.sh
```

![Images/MemInstall07.png](/cost/200_aws_resource_optimization/Images/AgentInstall07.png)

14. AmazonCloudWatchAgent profile 구성

서버에서 CloudWatch 에이전트를 실행하기 전에 사용자 정의 지표를 포함하여 에이전트가 수집 할 지표 및 로그를 지정하는 JSON 파일 인 CloudWatch 에이전트 구성파일을 작성해야합니다. 마법사를 사용하거나 처음부터 직접 작성하여 만들 수 있습니다. 에이전트 구성 파일을 변경할 때마다 변경 사항을 적용하려면 에이전트를 다시 시작해야합니다.

마법사는 AWS 자격증명 및 구성파일이있는 경우 사용할 자격증명 및 AWS 리전을 자동 검색 할 수 있습니다. 이러한 파일에 대한 자세한 내용은 *AWS Systems Manager 사용 설명서* 및 A[AWS documentation page](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-cloudwatch-agent-configuration-file.html)의 [구성 및 자격증몇 파일](https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html)을 참조하십시오.


이제 선택한 EC2 인스턴스에서 아래 명령을 실행하여 CloudWatch 에이전트 구성 파일 마법사를 시작하겠습니다.

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

15. CloudWatch Agent를 시작합니다.

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

![Images/MemInstall09.png](/cost/200_aws_resource_optimization/Images/AgentInstall09.png)

지표를 사용할 수있게되는 데 최대 5 분이 소요될 수 있습니다. 지표세션 아래의 **Amazon CloudWatch** 콘솔 페이지로 돌아가서 메모리 정보를 받고 있는지 확인하십시오.

**CWAgent**를 클릭합니다:
![Images/MemInstall10.png](/cost/200_aws_resource_optimization/Images/AgentInstall10.png)

**ImageID,InstanceID,InstanceType**를 클릭합니다:
![Images/MemInstall11.png](/cost/200_aws_resource_optimization/Images/AgentInstall11.png)

리스트의 **Instance**를 선택합니다:
![Images/MemInstall12.png](/cost/200_aws_resource_optimization/Images/AgentInstall12.png)

이제 CloudWatch 에이전트 설치를 완료했으며 Amazon CloudWatch에서 해당 인스턴스의 메모리 사용률을 모니터링 할 수 있습니다.

