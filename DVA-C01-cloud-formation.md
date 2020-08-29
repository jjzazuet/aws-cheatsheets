## AWS Cloud Formation

## Use cases

- Create collections of AWS resources, with predictble provisioning.
- Model infrastructure in a JSON or YAML template to describe resources.
- Automates provisioning and updating of infrastructure.

## Components

- Templates - defines resources to configure (YAML or JSON).
  - Only requires the `Resources` section.
  - Can be edited with CloudFormation Designer.
- Template config file - JSON for template parameter values.
- Stacks - related resource units.
  - Can be rolled back. Deletes related resources.
  - Can be directly updated.
  - Can be updates by changesets.
  - Can be nested.
- Rollback Triggers
- Change Sets - Summary of proposed changes before implementation.
- AWS Stack Sets
  - Deploy stacks across multiple regions with one template.
  - Used with AWS Organizations.
  - If you create a stack set in one Region, you cannot see it or change it in other Regions.

## Integration

- CloudTrail - Captures APi calls.
- Codepipeline
- Can make use of VPC endpoints.
- Can also pull values from Systems Manager Paramter Store as keys.

AWS CloudFormation provides the following Python helper scripts that you can use to install software and start services on an Amazon EC2 instance that you create as part of your stack:

- cfn-init: Use to retrieve and interpret resource metadata, install packages, create files, and start services.
- cfn-signal: Use to signal with a CreationPolicy or WaitCondition, so you can synchronize other resources in the stack when the prerequisite resource or application is ready.
- cfn-get-metadata: Use to retrieve metadata for a resource or path to a specific key.
- cfn-hup: Use to check for updates to metadata and execute custom hooks when changes are detected.

## Metrics

- CloudWatch alarms.

## Pricing

- No charge for CloudFormation. Just the resources created.
