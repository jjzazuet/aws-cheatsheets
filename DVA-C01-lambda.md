# AWS Lambda

## Languages supported

- NodeJS
- java
- Python
- C#
- Go
- Ruby

## Execution

- Works with invocation events.
- Event sources and downstream resources are connected by the labmda function itself.
- Reports to clloudwatch, with custom logging available for tracing.
- Code is stored at rest in S3.
- Max execution time of 15 mins or 900 seconds.
- Memory is adjustable, but not CPU.

## Extenral bindings

- S3
- Kinesis
- DynamoDB
- SQS

Lambda needs an IAM role to access VPC resources:

```
ec2:CreateNetworkInterface
ec2:DescribeNetworkInterfaces
ec2:DeleteNetworkInterface
```

```
ec2:DescribeSecurityGroups
ec2:DescribeSubnets
ec2:DescribeVpcs
```

Lambda can intercept Cloudfront@Edge requests/responses and alter the contents.

Can be built with CodePipeline and CodeDeploy.

Provisioned concurrency sets a fixed number of always-active Lambda instances. Reserved concurrency provisions additional instances on-demand for traffic bursts.

Individual lambdas set a concurrency limit, which reserves a portion of your account level concurrency limit for a given function.

Default Burst concurrency quotas

- 3000 – US West (Oregon), US East (N. Virginia), Europe (Ireland)
- 1000 – Asia Pacific (Tokyo), Europe (Frankfurt), US East (Ohio)
- 500 – Other Regions

https://docs.aws.amazon.com/lambda/latest/dg/invocation-scaling.html

Error codes: https://docs.aws.amazon.com/lambda/latest/dg/API_Invoke.html#API_Invoke_Errors

Throttling 

## Layers

- Just a bunch of stuff unzipped stuff in `/opt` :P.
- Can use up to 5.
- Can pull from 3rd party sources.
- Can help reduce the function code package size.

## Metrics

Lambda can report the following metrics:

- Invocation metrics
  - Invocations - successful invocations (billed).
  - Errors - timeouts, dead letter delivery failures, delivery errors.
  - Throttles
  - Provisoned concurrency
- Performance metrics
  - Duration
  - IteratorAge
- Concurrency
  - Concurrent executions
  - Provisioned concurrency executions
  - Unreserved concurrency execution

## Aliases

- Point only to one function version.
- Can be accessed by S3 using mappings.
- Need explicit access IAM policies pointing to the version (helps switch lambda versions without reconfiguring).
- Do traffic distribution by assigning fixed percentages to each function version (i.e. 10% to updated function, 90% to old function).

## Asynchronous invocation

- Needs invocation type as `Event`.
- Puts a queue in front of a lmabd function.
- Responds immediately with success, then preocesses in the background.
- Will retry events when the lambda function throttles or returns errors for up to 6 hours.

## Execution context

- Environment which provides initialization of external resources, so that new invocations don't need to be cold-started again (like DB connections or HTTP endpoints).
- Provides temporary storage.
