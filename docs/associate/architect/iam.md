# Identity and Access Management (IAM)

IAM allows you to manage users and their level of access to the AWS Console

1. Create users to grant permissions to those users
2. Create groups and roles
3. Control access to AWS resources

IAM is a global service, so users, groups, roles are all global resource

## Understanding IAM

It is important to understand IAM both for the exam and for the administrating of IAM policies in an organization

## Securing The Root Account

The root account is the email address you sign up for AWS. The root account has full administrative access to AWS. For this reason,
it is important to secure this account and not allow anyone access to the account

1. Enable Multi-factor authentication (MFA)
2. Create admin group for users
3. Create users for everyone

## Permissions with IAM

We assign permissions using policy documents, which are made up of JSON.

The following is a full admin access to the AWS Console.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

We can assign policy document to:

- Users (Typically bad practice)
- Groups (Better Practice)
- Roles (Best Practice)

### Amazon Managed Policy

Most cases a managed policy will already exist for what you need. Browse the policies for ones prefixed with the AWS Logo

## Using IAM

It is best practice for users to inherit permissions from groups, and just add and remove users from groups and apply IAM policies to groups.

### Users

- A physical person should always be 1 user to 1 human being
- Never share a user with multiple developers
- By default a new user has 0 permissions or access when created

### Groups

Functions such as administrators developers etc, Contains users

### Roles

Internal usage within AWS

### Principle of least Privilege

Only assign a user the minimum amount of privileges they need to do their job

### Single Sign On

- Can use SAML or OpenID Connect
- Free
- Syncs Active Directory provided with IAM in AWS

## Exam Tips

- Remember you assign permissions using policy documents written in JSON
- IAM is universal: It does not apply to regions at this time
- The Root Account: The Account created when you first set up your AWS account. It is all powerful and should not be used in day to day management
- Access Key ID and secret Access Keys are NOT the same as username and passwords
  - Only get to see these values once so save them or they will need to be rotated
  - Always Set up password rotation!
- By default users do not get any permissions
- IAM Federation uses SAML to do AD syncs

