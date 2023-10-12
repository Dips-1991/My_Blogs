---
title: "Day-39 Part-2: ☁AWS IAM Permissions, Policy, Role &Trust Policy  🔐🔑"
datePublished: Thu Oct 12 2023 15:59:48 GMT+0000 (Coordinated Universal Time)
cuid: clnnd8duw000809l6gwp29ryc
slug: day-39-part-2-aws-iam-permissions-policy-role-trust-policy
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697125579722/7de5d901-5e81-4ee1-a37d-33328d84590a.jpeg
tags: aws-iam, aws-iam-policies, iam-role, tws, iam-role-in-aws

---

### 📢 **Introduction**

In the last blog [Getting Started with AWS Basics☁](https://deepakcloud22.hashnode.dev/day-38-task-getting-started-with-aws-basics#heading-what-are-regions) we learned about the basics of ***AWS***, ***What is IAM***, ***Users***\*,\* **and *User groups***. We have also learned about ***Regions*** and ***Availability zones***, and we have performed some hands-on.

In this article, we are going to deep dive into the **Permissions**, **Policies**, **🔐** **IAM Role, Trust policy, Assume Role, and STS (Secure Service Token)**🔑**.**

### **🔐IAM (Identity and Access Management)**

* AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources.
    
* With IAM, you can centrally manage permissions that control which AWS resources users can access.
    
* You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.
    

### **🤔 How IAM Works?**

* IAM verifies that a user or service has the necessary authorization to access a particular service in the AWS cloud.
    
* We can also use IAM to grant the right level of access to specific users, groups, or services.
    
* For example, we can use IAM to enable an EC2 instance to access S3 buckets by requesting fine-grained permissions.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697028870192/9ce01cf4-e904-4981-9dd6-9d370e61c17d.png align="center")
    

### 🚷 **Policies and permissions in IAM**

* You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources.
    
* A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.
    
* AWS evaluates these policies when an IAM principal (user or role) makes a request.
    
* Permissions in the policies determine whether the request is allowed or denied. Most policies are stored in AWS as `JSON` documents.
    

### 🔠 **IAM Policy types**

AWS supports six types of policies: identity-based policies, resource-based policies, permissions boundaries, Organizations SCPs, ACLs, and session policies.

1. [**Identity-based policies**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_id-based) – Attach [managed](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#managedpolicy) and [inline](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#inline) policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.
    
2. [**Resource-based policies**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_resource-based) – Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies.
    
3. [**Permissions boundaries**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_bound) – A permissions boundary in IAM is an advanced feature that sets the maximum permissions a user or group can have, regardless of attached policies.
    
4. [**Organizations SCPs**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_scp) – Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU).
    
5. [**Access control lists (ACLs)**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_acl) – Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure.
    
6. [**Session policies**](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session) – Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. Session policies limit permissions for a created session.
    

### 👩‍💻 **Task 1:**

* **Create the** `EC2 instance` **as a root user, create the** `IAM user` **without any permission, and check if the IAM user is able to access the EC2 instance.**
    
* **Later on, provide full EC2 access to the IAM user using identity-based policies.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697094214677/5b20af90-8b19-4908-b8c0-38c8520b8963.png align="center")

1. **<mark>Launch the Instance:</mark>**
    
    Log in to the AWS management console and create the EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697091153608/8c9c5f66-954c-44e1-b3a7-85d487fd8238.png align="center")
    
2. **<mark>Create the IAM user:</mark>**
    
    Go to the IAM section and create the IAM user without any permission.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697091292438/6802ac28-1619-4d4b-8053-5d1d952d0c79.png align="center")
    
3. **<mark>Log in to AWS Console using IAM user and verify:</mark>**
    
    Go to the AWS management console login with the IAM user and verify if the IAM user is able to access the EC2 instance or not.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697091691573/89314304-d17d-42af-9963-d5f00aa7f25f.png align="center")
    
    We can see here Tom does not have permission to access the EC2 service.
    
4. **<mark>Assign EC2 full access to IAM user:</mark>**
    
    Now go to your `root account >` `go to IAM user >` `go to permission` &gt; click on `Add permission` &gt; and assign `EC2 full access` to the IAM user using `Add permission`.
    
    After clicking on Add permission there is two way to add permission
    
    1\. **Managed policies** – Managed policies that are created and managed by AWS.
    
    2\. **Inline policies** – You can create your custom policy and use it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697092170830/bf45fae6-6085-46d2-a3f6-11107f6ed50c.png align="center")
    
    Now after clicking on Add permission on the next page select `Attach policy directly` and in `Permissions policies` Search for `AmazonEC2FullAccess` and click on next then review and click on add permission.
    
    You can see that permission is added to the IAM user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697092356907/651c4e89-5ad9-4656-aba6-252f1943b23b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697092460583/dfbdd24e-0baa-4849-b240-aa422ec73f30.png align="center")
    
5. **<mark>Log in to AWS Console using IAM user and verify:</mark>**
    
    Once you log in as an IAM user you can see the IAM user is able to access the EC2 service and the IAM user can perform all the EC2 operations because we have given the EC2 full access to the IAM user.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697092649265/6bbaded4-6c18-4e23-a873-45e7de9a5ed5.png align="center")
    

### 👩‍💻 **Task 2:**

* **Create the** `2 S3 buckets` **in the root account, create the** `IAM user` **with** `AmazonS3ReadOnlyAccess` **permission, and check if the IAM user is able to access the S3 buckets and Put objects into the bucket.**
    
* **later on, allow the IAM user to Put the object into one of the bucket using** `Resource-based policies`**.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697094987449/7595a2e6-06d4-4de6-abce-27b450bf9eec.png align="center")

1. **<mark>Create the IAM user:</mark>**
    
    **Create the** `IAM user` **with** `AmazonS3ReadOnlyAccess` **permission.**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697099757225/33b57380-1b84-45fe-a337-c5259f4144d8.png align="center")
    
2. **<mark>Create 2 S3 Buckets:</mark>**
    
    Create 2 S3 buckets with the name `tomsnewbucket1`, `tomsnewbucket2`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697099820225/1fe06292-d017-4239-b252-87df05784ea5.png align="center")
    
3. **<mark>Log in to AWS Console using IAM user and verify:</mark>**
    
    Go to the AWS management console login with the IAM user `goto S3 bucket service` and verify if the IAM user is able to `Put the object into S3 buckets` or not.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697100359214/c2078c63-b175-4885-beb0-de914b736967.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697100395600/6e3b6228-7aa0-4f66-b01f-3a8945d490bf.png align="center")
    
    We can see that `Tom` can not create the folder into `tomsnewbucket1`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697100988769/9304afe0-6688-4f93-8215-309aea1a1861.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697101025152/b17da30e-4757-4fb8-8dcf-996d1b97d1d0.png align="center")
    
    Same, Tom can not create the folder into `tomsnewbucket2` as well.
    
    Because we have only allowed `Tom to read the bucket`.
    
4. **<mark>Assign Resource-based policies to the S3 bucket:</mark>**
    
    Now, we will assign policy permission to the `S3 bucket` `tomsnewbucket1` that only IAM user `Tom` can put the object into the bucket and we will see if the `Tom` can put an object in the bucket `tomsnewbucket2`.
    
    As of now, we have only given the `AmazonS3ReadOnlyAccess` to the IAM user `Tom`.
    
    Go to `root user account` &gt; `go to S3` &gt; `Buskets` &gt; `go to tomsnewbucket1` &gt; `go to Permissions` go down in `Bucket policy` click on `Edit` &gt; Add the `JSON documents` and click on `Save changes`.
    
    ```apache
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Statement1",
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::385136888024:user/Tom"
                },
                "Action": "S3:*",
                "Resource": "arn:aws:s3:::tomsnewbucket1/*"
            }
        ]
    }
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697113460381/89695aec-0bbd-442b-82c4-ca28e69141bb.png align="center")
    
    **Explanation of the JSON Policy:**
    
    * `Version`: This indicates the version of the policy language being used. In this case, it's set to `"2012-10-17,"` which is the current version.
        
    * `Statement`: This is an array of individual statements that define permissions. In your example, there is one statement.
        
    * `Sid`: A unique identifier for the statement. In this case, it's set to `"Statement1"` for easy reference.
        
    * `Effect`: Specifies whether the statement allows or denies the specified actions. Here, it's set to "Allow," meaning it grants permissions.
        
    * `Principal`: Defines the AWS `entity (user, group, role, or service)` that the policy is applied to. In this policy:
        
    * `"AWS": "arn:aws:iam::385136888024:user/Tom"` indicates that the policy applies to the IAM user with the `ARN (Amazon Resource Name)`.
        
    * `Action`: Specifies the AWS service API actions allowed or denied. Here, it's set to `"S3:*"` allow any action (`*`) on Amazon S3.
        
    * `Resource`: Specifies the AWS resources to which the permissions apply. In this case, it's set all permissions apply to objects within the S3 bucket named `tomsnewbucket1`.
        
5. **<mark>Log in to AWS Console using IAM user and verify:</mark>**
    
    Now, Log in with the IAM user `Tom` and go to `S3` &gt; `Buckets` &gt; `tomsnewbucket1` &gt; `Create folder` and add a folder in the bucket `tomsnewbucket1`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697113943123/698a85fb-a4c2-4668-9c9b-0b5889ec731b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697113978253/b316a2ca-4ab0-4fb4-bfa2-83368fc842e1.png align="center")
    
    Here we can see we have assigned the permission policy to the `S3 bucket` `tomsnewbucket1` that only IAM user Tom can perform the operation on the bucket `tomsnewbucket1`.
    
    Now, go to the bucket `tomsnewbucket2` and add the folder to it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697114291436/5f5fae10-8e77-45cd-ad0a-10dd82ebc8b3.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697114323848/7771a36c-2b3d-4c67-9b20-05e23f212f7e.png align="center")
    
    Here we can see Tom can not perform any operation on `tomsnewbucket2` because we have assigned the resource base policy here on the bucket `tomsnewbucket1` only that user Tom can perform any operation on only `tomsnewbucket2`.
    

### 🎭 **IAM Role & Trust Policy**

* `Purpose:` An IAM role has some similarities to an IAM user and is used to grant permissions to AWS services or non-human entities.
    
* `Usage:` They are commonly used to provide access to applications running on AWS services.
    
* `Authentication:` IAM Roles provide temporary credentials for entities assuming the role.
    
* `Permission:` Permissions are attached to the role and are assumed by entities.
    
* `Trust Relationship:` IAM Roles define trust relationships that specify which entities are allowed to assume the role.
    
* `Credential Rotation:` IAM Roles provide temporary credentials that are automatically rotated by AWS.
    
* `Auditing and Compliance:` Actions performed by entities assuming a role are logged under the role’s activity.
    

### 🤝 **Trusted entity type**

Roles can be used by the following:

1. `AWS service:` Allow AWS services like EC2, Lambda, or others to perform actions in this account.
    
2. `AWS account:` Allow entities in other AWS accounts belonging to you or a 3rd party to perform actions in this account.
    
3. `Web identity:` Allows users federated by the specified external web identity provider to assume this role to perform actions in this account.
    
4. `SAML 2.0 federation:` Allow users federated with SAML 2.0 from a corporate directory to perform actions in this account.
    
5. `Custom trust policy:` Create a custom trust policy to enable others to perform actions in this account.
    

### 🤳 **Assume Role in AWS**

Assuming a role involves **using a set of temporary security credentials that you can use to access AWS resources that you might not normally have access to**

### 🔑 **STS (Secure Service Token)**

Returns a set of temporary security credentials that you can use to access AWS resources. These temporary credentials consist of an access key ID, a secret access key, and a security token. Typically, you use AssumeRole within your account or for cross-account access.

### 👩‍💻 **Task 2:**

* **Create the EC2 instance and connect using SSH and access the S3 bucket list.**
    
* **Later on, Create the IAM Role, and attach the S3 full access permission to the role, Create the** `Trust Policy` **using** `Trusted entity` **where we will select** `AWS service`**, And will provide the** `EC2` **to assume the role within an AWS account.**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697117474929/f9108e82-d157-4b78-89e0-49e4435f0157.png align="center")

1. **<mark>Launch the Instance:</mark>**
    
    Log in to the AWS management console and create the EC2 instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697091153608/8c9c5f66-954c-44e1-b3a7-85d487fd8238.png align="left")
    
2. <mark>Connect EC2 Instance &amp; List S3 Bucket:</mark>
    
    Connect to the EC2 instance using SSH and use the command to list all S3 buckets.
    
    Note: Please install the `aws cli` before using the aws command.
    
    ```apache
    sudo apt update -y
    sudo apt  install awscli
    aws --version
    ```
    
    ```apache
    aws s3 ls
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697118337653/db3d7366-be64-478b-aba4-2daa85084eda.png align="center")
    
    We can see here we can not access the list of the S3 buckets. As we don't have permission or we can't configure our credentials`(access key & secret key)` with aws cli. But here we will use the `IAM Role`, `Trust Policy`, and `STS (Secure Service Token)` now.
    
3. **<mark>Create IAM Role:</mark>**
    
    `Go to IAM` &gt; `go to Roles` &gt; `Create role` &gt; `Select trusted entity as AWS service` &gt; In the `Use case` &gt; `EC2 (Allows EC2 instances to call AWS services on your behalf)` &gt; Click on `Next` &gt; On the next page in `Permissions policies` select &gt; `AmazonS3FullAccess` &gt; Click on `Next`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697118941348/9d9b8a00-ffa9-417a-a756-93b3e5aed498.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697119263352/046a223d-1fda-43e3-adb2-2186cd165de6.png align="center")
    
    On the next page Give the `Role name` and `Description`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697119434843/2a595dad-3761-4c38-b1f0-d9c1dfc46e2c.png align="center")
    
    In the `Select trusted entities` you can see the Trust Policy is written in JSON
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697119571946/92b5552e-3ba2-48c8-ba1e-5bdb362e05c0.png align="center")
    
    As we have seen in the previous example the Policy JSON document, Here the new thing is
    
    `sts:AssumeRole` action. This action is used to request temporary security credentials to assume an IAM role.
    
    `Principal`: The policy allows EC2 instances to assume the specified role.
    
4. **<mark>Attach Role To Instance:</mark>**
    
    Here we will attach the created `Role to the EC2 instance` means the EC2 instance will assume the role on behalf of the user.
    
    Go to the `EC2 instance and select` &gt; On the right side click on `Action` &gt; click on `Security` &gt; Click on `Modify IAM Role`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697124082968/e337eb18-9f43-4e92-8e70-ef7f1365ae04.png align="center")
    
    Now select the `IAM Role` that we have created and click on `Update IAM role`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697124171115/21c05a81-5ba9-4066-b9e5-e26d5d5801ec.png align="center")
    
5. **<mark>Connect EC2 Instance &amp; List S3 Bucket:</mark>**
    
    Connect to the EC2 instance using SSH and use the command to list all S3 buckets.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697099820225/1fe06292-d017-4239-b252-87df05784ea5.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697124323572/d431ed2b-d0dc-45ef-80ab-0004bf5161fb.png align="center")
    
    Now you can see we are able to list the S3 buckets with the help of `IAM Role`, `Trust Policy(Assume Role)`, and `STS`.
    

### 📜 **Conclusion**

* In this tutorial, we have learned about AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources.
    
* We have learned how permissions and policies are used in AWS to allow and deny the set of operations with the help of hands-on
    
* We also learned about the IAM Role, Trust policy, Assume role, and STS.
    

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***