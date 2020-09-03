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





    


