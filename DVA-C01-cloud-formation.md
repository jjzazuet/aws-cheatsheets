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

## Metrics

- CloudWatch alarms.

## Pricing

- No charge for CloudFormation. Just the resources created.
