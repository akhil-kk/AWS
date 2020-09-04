## IAM - Identitiy Access Management

* Its a Global service.
* Root account created by default, shouldn't be used or shared.
* Groups only contain users, not other groups.
* A user dont ahve to belong to a group, and a user can belong to multiple groups.
* Users or Groups can be assigned JSON document called policies.
* In AWS you apply the least privilege principle: dont give more permissions than a user needs.

**IAM password policy**

* set a min password length
* Require users to chnage their password after some time.
* MFA = password you know + security device you own.

### MFA devices in AWS

* Google authenticator
* Authy - muti-device
* Yubikey - support multiple root
* Hardware key fob MFA

## AWS CLI

* To access AWS you have three options.
    * AWS management console.
    * AWS command line interface
    * AWS sofwtare development kit.
* Access keys are generated through the AWS console.
```
aws iam list-users          // list all users
```

## IAM Roles

* Some AWS service will need to perform actions on your behalf.
* To do so we will assign permissions to AWS services with IAM roles.
* Common Roles
    * EC2 Instance Roles.
    * Lambda Function Roles.
* IAM roles are a secure way to grant permissions to entities that you trust. Examples of entities include the following:

    * IAM user in another account.
    * Application code running on an EC2 instance that needs to perform actions on AWS resources.
    * An AWS service that needs to act on resources in your account to provide its features.
    * Users from a corporate directory who use identity federation with SAML.
    * IAM roles issue keys that are valid for short durations, making them a more secure way to grant access.

## IAM securtiy tools

* IAM Credentials report

A report that lists all your account's users and the status of their various credentials.

* IAM Access advisor 

Access advisor shows the service eprmissions granted to auser and when those services were last accessed.

## IAM Guidelines

* Dont use root account except for aws account setup
* One physical user = one AWS user.
* Assign users to groups and assign permissions to groups.
* Create a strong password policy.
* Use and enforce the use of MFA.
* Create and use Roles for giving permissions to AWS services.
* Use Access Keys for Programmatic Access.
* Audit permissions of your account with the IAM credentails report.

## Amazon EC2

* Most popular of AWS' offering.
* EC2 = Elastic Compute Cloud = Infrastructure as aservice.
* Capabilities
    * Reting VMs (EC2).
    * Storing data on Virtual drives(EBS).
    * Distributing load across machines(ELB).
    * Scaling services using an auto-scaling group (ASG).

## EC2 sizing & Config

* OS
* CPU
* RAM
* Storage 
    * Network-attached(EBS & EFS)
    * hardsware (EC2 instance & Store)
* N/W card
* Bootstrap script: EC2 user data.

## EC2 instance types, examples

![Ec2 instance types](img/ec2.png?raw=true "Title")

## Launching an EC2 instance

 * Choose an Amazon Machine Image (AMI) - contains all your software config.

## Introduction to Security groups

* Act as a firewall on EC2 instances.
* How traffic is allowed into or out of our EC2 instances.
* Security groups only contain allow groups
* Security groups can reference by Ip or by security group.
* They regulate 
    * Access to ports
    * Authorised IP ranges

## Ports to know

![Ports](img/ports.png?raw=true "Title")

## SSH

![SSH](img/ssh.png?raw=true "Title")

## EC2 instance launch types

* On demand instance; short workload, predictable pricing
* Reserved: (min 1year)
* Dedicated hosts.
* Spot instances

## EC2 instance Storage

### EBS volume (Elastic Block Store)

* network drive you can attach to your instances while they run.
* It allows your instances to persist data even after their termination.

**EBS Volume**

* Its a network drive
* Uses nw to communicate to instance.
* It can be detached from an EC2 instance and attcahed to another one.
* Its locked to an availability zone
* To move volume across, you need to snapshot it.
* Have provisioned capacity.

## EBS Snapshots

* Make a backup of your EBS volume at a point in time.
* Not necessary to detach volume eto do snapshot, but recommended.
* Can copy snaoshots across AZ or Region.

## AMI

* AMI = Amazon Machine Image
* AMI are a customization of an EC2 instance
* You add your own software, configuration, operating system, monitoring…
* Faster boot / configuration time because all your software is pre-packaged
* AMI are built for a specific region (and can be copied across regions)
* You can launch EC2 instances from:
* A Public AMI: AWS provided
* Your own AMI: you make and maintain them yourself

## EC2 Instance Store

* EBS volumes are network drives with good but “limited” performance
* If you need a high-performance hardware disk, use EC2 Instance Store
* Better I/O performance
* EC2 Instance Store lose their storage if they’re stopped (ephemeral)
* Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails
* Backups and Replication are your responsibility

## EFS – Elastic File System
* Managed NFS (network file system) that can be mounted on 100s of EC2
* EFS works with Linux EC2 instances in multi-AZ
* Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning

![EBSvsEFS](img/ebsVsefs.png?raw=true "Title")



