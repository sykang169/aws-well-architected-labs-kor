---
title: "Test Resiliency Using EC2 Failure Injection"
menutitle: "EC2 Failure Injection"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>2. </b>"
weight: 2
---

### 4.1 EC2 failure injection

This failure injection will simulate a critical problem with one of the three web servers used by your service.

1. Open EC2 Console, Select **Instances** in left menu: <http://console.aws.amazon.com/ec2>.

1. There are two EC2 instances with a name beginning with **WellArchitectedLabsStack/ASG**. For these EC2 instances note:
      1. Each has a unique *Instance ID*
      1. There is one instance per each Availability Zone
      1. All instances are healthy
    ![EC2ShuttingDown](/images/reliability/reliability-ec2-normal.png)

1. Open up two more console in separate tabs/windows. From the left pane, open **Target Groups** and **Auto Scaling Groups** in separate tabs. You now have three console views open

    ![NavToTargetGroupAndScalingGroup](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/NavToTargetGroupAndScalingGroup.png)

1. To fail one of your EC2 instances, run the script below using your VPC ID in Cloud9's terminal. Replace \<vpc-id\> with the VPC ID you copyed before.

    ```bash
    ./fail_instance.sh <vpc-id>
    ```

1. The specific output will vary based on the command used, but will include a reference to the ID of the EC2 instance and an indicator of success.  Here is the output for the Bash command. Note the `CurrentState` is `shutting-down`

        $ ./fail_instance.sh vpc-04f8541d10ed81c80
        Terminating i-0710435abc631eab3
        {
            "TerminatingInstances": [
                {
                    "CurrentState": {
                        "Code": 32,
                        "Name": "shutting-down"
                    },
                    "InstanceId": "i-0710435abc631eab3",
                    "PreviousState": {
                        "Code": 16,
                        "Name": "running"
                    }
                }
            ]
        }

1. Go to the *EC2 Instances* console which you already have open (or [click here to open a new one](http://console.aws.amazon.com/ec2/v2/home?region=us-east-2#Instances:))

      * Refresh it. (_Note_: it is usually more efficient to use the refresh button in the console, than to refresh the browser)

           ![RefreshButton](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/RefreshButton.png)
    
      * Observe the status of the instance reported by the script. In the screen cap below it is _shutting down_ as reported by the script and will ultimately transition to _terminated_.

        ![EC2ShuttingDown](/images/reliability/reliability-ec2-shuttingdown.png)

### 4.2 System response to EC2 instance failure

Watch how the service responds. Note how AWS systems help maintain service availability. Test if there is any non-availability, and if so then how long.

#### 4.2.1 System availability

Refresh the service website several times: For the website's address, use ALBDNS in the Outputs of the CloudFormation `MasterAccount` Stack created in the lab setup.

* Website remains available
* The remaining two EC2 instances are handling all the requests (as per the displayed `instance_id`)

#### 4.2.2 Load balancing

Load balancing ensures service requests are not routed to unhealthy resources, such as the failed EC2 instance.

1. Go to the **Target Groups** console you already have open (or [click here to open a new one](http://console.aws.amazon.com/ec2/v2/home?region=us-east-2#TargetGroups:))
     * If there is more than one target group, select the one with the **Load Balancer** named **ResiliencyTestLoadBalancer**

1. Click on the **Targets** tab and observe:
      * Status of the instances in the group. The load balancer will only send traffic to healthy instances.
      * When the auto scaling launches a new instance, it is automatically added to the load balancer target group.
      * In the screen cap below the _unhealthy_ instance is the newly added one.  The load balancer will not send traffic to it until it is completed initializing. It will ultimately transition to _healthy_ and then start receiving traffic.
      * Note the new instance was started in the same Availability Zone as the failed one. Amazon EC2 Auto Scaling automatically maintains balance across all of the Availability Zones that you specify.

        ![TargetGroups](/images/reliability/reliability-ec2-targetgroup.png)    

1. From the same console, now click on the **Monitoring** tab and view metrics such as **Unhealthy hosts** and **Healthy hosts**

       ![TargetGroupsMonitoring](/images/reliability/reliability-ec2-montoring.png) 
         
#### 4.2.3 Auto scaling

Autos scaling ensures we have the capacity necessary to meet customer demand. The auto scaling for this service is a simple configuration that ensures at least three EC2 instances are running. More complex configurations in response to CPU or network load are also possible using AWS.

1. Go to the **Auto Scaling Groups** console you already have open (or [click here to open a new one](http://console.aws.amazon.com/ec2/autoscaling/home?region=us-east-2#AutoScalingGroups:))
      * If there is more than one auto scaling group, select the one with the name that starts with **WebServersforResiliencyTesting**

1. Click on the **Activity History** tab and observe:
      * You can check instance status and time.
        ![AutoScalingGroup](/images/reliability/reliability-ec2-asg.png)   

_Draining_ allows existing, in-flight requests made to an instance to complete, but it will not send any new requests to the instance. *__Learn more__: After the lab [see this blog post](https://aws.amazon.com/blogs/aws/elb-connection-draining-remove-instances-from-service-with-care/) for more information on _draining_.*

*__Learn more__: After the lab see [Auto Scaling Groups](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html) to learn more how auto scaling groups are setup and how they distribute instances, and [Dynamic Scaling for Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scale-based-on-demand.html) for more details on setting up auto scaling that responds to demand*

#### 4.2.4 EC2 failure injection - conclusion

Deploying multiple servers and Elastic Load Balancing enables a service suffer the loss of a server with no availability disruptions as user traffic is automatically routed to the healthy servers. Amazon Auto Scaling ensures unhealthy hosts are removed and replaced with healthy ones to maintain high availability.
