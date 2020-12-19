---
title: "AWS IAM in Plain English"
date: "2019-08-29T14:29:14+06:00"
---

---

## Intro

AWS Identity and Access Management (IAM) is a web service that helps us securely control access to AWS resources. We can control authentication (who can signed in) and authorization (who has permissions to use resources) using IAM.
When we create an AWS account, we get a root user which has complete access to all AWS services and resources in the account. It is recommended that we do not use the root account regularly, instead we should create IAM users to access the AWS services and resources frequently. We can also grant other people permission to administer and use resources in our AWS account without having to share our password or access key. It is possible to grant different permissions to different people for different resources.

IAM is free to use. We will be charged only when we access other AWS services using our IAM users credentials.
As the name (AWS Identity and Access Management) says, there is Identities and there is Access management.

---

## Identities :

IAM Identities are Users, Groups, and Roles. The common use of IAM is to manage those identities.

### Users
	
IAM users are not separate accounts; they are users within our account. An IAM user doesn’t have to represent an actual person; we can create an IAM user in order to generate an access key for an application that needs AWS access.

When creating an IAM user, We can select the type of access the user will have. We can select programmatic access, access to the AWS Management Console, or both. After new users are created, they can’t access anything in our account until we give them permission. We give permissions to a user by creating an identity-based policy, which is a policy that is attached to the user or a group to which the user belongs.

> For creating an IAM user with full admin access, Just create an IAM user and attach the “AdministratorAccess” policy to that user.

### Groups

An IAM group is a collection of IAM users. It is easy to manage multiple users (of same kind) using groups. We can create new groups by simply providing the group name and permissions for that group. Then we add the users to the group.

### Roles

An IAM role is very similar to a user, in that it is an identity with permission policies that determine what the identity can and cannot do in AWS. However, a role does not have any credentials (password or access keys) associated with it. Instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. We can use IAM roles to delegate access to IAM users managed within our account, to IAM users under a different AWS account, to Applications running on EC2 or to an AWS service (such as EC2). Delegating access using IAM Roles is a secure way as they use temporary credentials.

> To decide when to create IAM Users and when to create IAM Roles, please check the official doc : https://amzn.to/2GItEb4

---

## Access Management :

Access Management is often referred to as authorization. This portion of IAM manages what a principal entity(person or application) is allowed to do in an account. We can manage access by creating policies and attaching them to IAM identities or AWS resources.

### Policy :

A policy is an object that defines permissions. Most policies are stored as JSON documents. Policies are attached to IAM identities or AWS resources. AWS evaluates these policies when a principal entity (user or role) makes a request. Permissions in the policies determine whether the request is allowed or denied. There are different types fo policies. Two importat types are Identity-based policies & Resource-based policies.

#### Identity-based policies :

Identity-based policies are attached to an IAM identity (user, group or role). These policies defines what actions the identity can perform, on which resources, and under what conditions.

- Managed Policies :
These are standalone policies that we can attach to multiple users, groups and roles.

- Inline Policies : 
We can create inline policies that are embedded directly into a single user, group or role.

#### Resource-based policies :
Resource-based policies are attached to a resource (i.e, Amazon S3 bucket). These policies control what actions a specified principal can perform on that resource and under what conditions.

---

## References

- https://aws.amazon.com/iam/faqs/
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html