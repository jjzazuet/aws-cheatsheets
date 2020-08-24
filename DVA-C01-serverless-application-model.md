## AWS Serverless Application Model

## Use cases

- Open source serverless app model.

## Components

- JSON or YAML configs.
- Translate SAM templates into CloudFormation templaptes.
- Standalone SAM templates require the `Transform` section to become CloudFormation templates.
- Contains globals and resource definitions.
  - Api gateway resource.
  - Serverless application.
  - Functions with event sources.
  - LayerVersions.
  - SimpleTable for DynamoDB.

## Integration

- Can be used to configure API Gateway Lambda authorizers.
- And Cognito authorizers.
