## AWS Identity & Access Management

## Use cases

- Controls who is authenticated, and what are they allowed to do.
- Allows other parties to use and manage resources without sharing passwords or access keys.
- Provides apps on EC2 instances to access other AWS resources via credentials.

## Components

- Resources are objects that exist within a service.
- 2FA provides added security.
- Identity federation grants other users temporary access to the AWS account.
- Access keys with ID allows programmatic access to AWS.
  - Only generated once. Needs regenerating if lost.
- IAM tags add attributes to users or roles.

### Principals

- They request actions on a resource
  - A single root user per account can access all services and resources.
  - Users, roles, federated users and apps are also principals.
- External users can be federated into IAM identities.

### IAM users

- Are users within the AWS account.
- Have their own access passwords, and optional access keys for API use.
- A new user has no permissions at all.
- Are global across all AWS.

### IAM Groups

- Groups of IAM users.
- Users can belong to multiple groups.
- Groups are unrelated to each other.
- Have no credentials.
- Cannot access services directly. Must use policies.

### IAM Roles

- Have no credentials.
- Needs to specify permissions for resource access.
- Can be temporarily attached to IAM users to perform a task.
- Can be attached to services for automatic actions on the account.
- Some services assume a special EC2 role to lanuch instances, and then pass the role to the launched instance.
- Service roles are default roles for services which define what's needed to call other services.
- To assume a role, call `AssumeRole` to get an access key with ID, secret, and a security token.
  - MFA and SAML can optionally be used.

### Policies

- Are JSON documents.
- Identity based policies.
  - Attached to users, groups or roles to grant them permissions.
- Resource based policies.
  - Attached to resources (like S3 buckets).
- Trust policies.
  - Attached to a role. Define which principals can assume the role.
- Requests are validated by policies which allow or deny the request.
  - Permission policies act on objects.
    - Identity policies.
    - Resource policies (grant cross-account access).
    - Access control lists.
  - Permission boundaries are used to limit the permissions of a principal.

### Actions

- Tied to resources. Tells what to do.
  - View
  - Create
  - Edit
  - Delete
- Services define the actions that can be done to a resource.

### Policy rules

- All requests are implicitly denied by default.
- Explicit allows overrides the default.
- Explicit denies override any allows.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ReadWriteTable",
            "Effect": "Allow",
            "Action": [
                "dynamodb:BatchGetItem",
                "dynamodb:GetItem",
                "dynamodb:Query",
                "dynamodb:Scan",
                "dynamodb:BatchWriteItem",
                "dynamodb:PutItem",
                "dynamodb:UpdateItem"
            ],
            "Resource": "arn:aws:dynamodb:*:*:table/SampleTable"
        },
        {
            "Sid": "GetStreamRecords",
            "Effect": "Allow",
            "Action": "dynamodb:GetRecords",
            "Resource": "arn:aws:dynamodb:*:*:table/SampleTable/stream/* "
        },
        {
            "Sid": "WriteLogStreamsAndGroups",
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CreateLogGroup",
            "Effect": "Allow",
            "Action": "logs:CreateLogGroup",
            "Resource": "*"
        }
    ]
}
```

### AWS Managed Policies

- Defines a set of use cases that are most common in the IT industry:
  - Administrator - Grants all acctions on all services for all resources in the account.
  - Billing - Grants access to manage billing, costs, payment methods, budgets, reports.
  - Database Administrator - Grants permissions to create, configure, and maintain databases.
  - Data Scientist - Access to information for data analytics and business intelligence.
  - Network Administrator - Setting up and maintaining AWS network resources.
  - Security Auditor - Grants permissions to view configuration data for many AWS services and to review their logs.
  - Support User - Grants permissions to create and update AWS Support cases.
  - System Administrator - Sets up and maintains resources for development operations. 
  - View Only User (ViewOnlyAccess) - Grants List*, Describe*, Get*, View*, and Lookup* access to resources for most AWS services.

https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html

https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html

Service linked roles are pre-defined by AWS for each kind of service, and cannot be changed.

## Cross account access

### Security Token Service (STS)

- Global service with single endpoint.
- Provides trusted users temporary credentials to control AWS resources.
- Are short-lived, not stored, dynamically generated and provided when requested.
- Consist of access key with ID, secret and security token.
- Granted to IAM or federated users.

## EC2 instance profile

TBD

## API calls

- `AssumeRole` - makes a principal assume and IAM role.

## Metrics

- CloudTrail logs with requests made by IAM identities.

## Pricing

- IAM and STS are offered free of charge.
