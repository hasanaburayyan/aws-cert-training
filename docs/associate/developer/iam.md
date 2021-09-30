# IAM

- IAM allows you to manager users and their level of access to the AWS Console
- Centralized control of your AWS account
- Shared Access to your AWS account
- Granular Permissions
- Identity Federation
- Multi Factor Authentication
- Provide temporary access for users/devices and services, as necessary
- Allows you to set up your own password rotation policy
- Integrates with many AWS services.
- Supports PCI DSS Compliance
- Critical Terms:
  - Users: End Users (Think People)
  - Groups: Collection of users under one set of permissions
  - Roles: Create roles and then assign them to AWS resources
  - Policies: A document that defines one (or more) permissions

## Roles

- Roles allow access to resources without ACCESS keys
- Roles are preferred from a security perspective
- Roles are controlled by policies
- You can change a policy on a role and it will take immediate effect
- You can attach and detach roles to running EC2 instances without having to stop or terminate these instances