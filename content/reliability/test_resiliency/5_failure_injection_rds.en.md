---
title: "Test Resiliency Using RDS Failure Injection"
menutitle: "RDS Failure Injection"
date: 2020-04-24T11:16:09-04:00
chapter: false
pre: "<b>3. </b>"
weight: 3
---

### 5.1 RDS failure injection {#rdsfailureinjection}

This failure injection will simulate a critical failure of the Amazon RDS DB instance.

1. Go to the RDS Dashboard in the AWS Console at <http://console.aws.amazon.com/rds>

1. From the RDS dashboard
      * Click on "DB Instances (_n_/40)"
      * Click on the DB identifier for your database (if you have more than one database, refer to the **VPC ID** to find the one for this workshop)
      * If running the **multi-region** deployment, select the DB instance with Role=**Master**
      * Select the **Configuration** tab

1. Look at the configured values. Note the following:
      * Value of the **Info** field is **Available**
      * RDS DB is configured to be **Multi-AZ**.  The _primary_ DB instance and the _standby_ DB instance is located diffrent AZ.
        ![DBInitialConfiguration](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/DBInitialConfiguration.png)


1. To fail one of your RDS instances, run the script below using your VPC ID in Cloud9's terminal. Replace \<vpc-id\> with the VPC ID you copyed before.

      ```bash
      ./failover_rds.sh <vpc-id>
      ```

1. The specific output will vary based on the command used, but will include some indication that the your Amazon RDS Database is being failedover: `Failing over mdk29lg78789zt`

### 5.2 System response to RDS instance failure

Watch how the service responds. Note how AWS systems help maintain service availability. Test if there is any non-availability, and if so then how long.


#### 5.2.1 System availability

1. The website is _not_ available. Some errors you might see reported:
      * **No Response / Timeout**: Request was successfully sent to EC2 server, but server no longer has connection to an active database
      * **504 Gateway Time-out**: Amazon Elastic Load Balancer did not get a response from the server.  This can happen when it has removed the servers that are unable to respond and added new ones, but the new ones have not yet finished initialization, and there are no healthy hosts to receive the request
      * **502 Bad Gateway**: The Amazon Elastic Load Balancer got a bad request from the server
      * An error you will _not_ see is **This site can’t be reached**. This is because the Elastic Load Balancer has a node in each of the three Availability Zones and is always available to serve requests.

1. Continue on to the next steps, periodically returning to attempt to refresh the website.

#### 5.2.2 Failover to standby

1. On the database console **Configuration** tab
      1. Refresh and note the values of the **Info** field. It will ultimately return to **Available** when the failover is complete.
      1. Note the AZs for the _primary_ and _standby_ instances. They have swapped as the _standby_ has no taken over _primary_ responsibility, and the former _primary_ has been restarted. (After RDS failover it can take several minutes for the console to update as shown below. The failover has however completed)


         ![DBPostFailConfiguration](/Reliability/300_Testing_for_Resiliency_of_EC2_RDS_and_S3/Images/DBPostFailConfiguration.png)

      1. From the AWS RDS console, click on the **Logs & events** tab and scroll down to **Recent events**. You should see entries like those below. In this case failover took less than a minute.

      > * Mon, 14 Oct 2019 19:53:37 GMT - Multi-AZ instance failover started.
      > * Mon, 14 Oct 2019 19:53:45 GMT - DB instance restarted
      > * Mon, 14 Oct 2019 19:54:21 GMT - Multi-AZ instance failover completed

#### 5.2.3 RDS failure injection - conclusion

* AWS RDS Database failover took less than a minute

---

#### Resources

*__Learn more__: After the lab see [High Availability (Multi-AZ) for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html) for more details on high availability and failover support for DB instances using Multi-AZ deployments.*

**High Availability (Multi-AZ) for Amazon RDS**
> The primary DB instance switches over automatically to the standby replica if any of the following conditions occur:
> * An Availability Zoßne outage
> * The primary DB instance fails
> * The DB instance's server type is changed
> * The operating system of the DB instance is undergoing software patching
> * A manual failover of the DB instance was initiated using Reboot with failover
