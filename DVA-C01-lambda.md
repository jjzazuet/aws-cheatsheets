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

Lambda will always leave 100 concurrency units as unreserved concurrency. Only 900 units can be
reserved across functions.

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

## Invocations

- `RequestResponse` (default) - Invoke the function synchronously.
  - Keep the connection open until the function returns a response or times out.
  - The API response includes the function response and additional data.
- `Event` - Invoke the function asynchronously.
  - Puts a queue in front of a lambda function.
  - Responds immediately with success, then processes in the background.
  - Will retry events when the lambda function throttles or returns errors for up to 6 hours.
  - Sends events that fail multiple times to the function's dead-letter queue (if it's configured).
  - The API response only includes a status code.
- `DryRun` - Validate parameter values and verify that the user or role has permission to invoke the function.

## Integration

- Works with CodeDeploy to perform Canary deployments.

https://docs.aws.amazon.com/whitepapers/latest/modern-application-development-on-aws/canary-deployments-to-aws-lambda.html

### Proxy integration types

TODO

https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-simple-proxy-for-lambda-output-format


### Error Codes

TODO

https://aws.amazon.com/premiumsupport/knowledge-center/malformed-502-api-gateway/
https://docs.aws.amazon.com/apigateway/api-reference/handling-errors/

## Execution context

- Environment which provides initialization of external resources, so that new invocations don't need to be cold-started again (like DB connections or HTTP endpoints).
- Provides temporary storage.

### Environment Variables:

- `_X_AMZN_TRACE_ID`
  - Contains tracing header, including sampling decision, trace ID, parent segment ID.
  - If Lambda receives a tracing header when function is invoked, that header will be used to populate the `_X_AMZN_TRACE_ID` environment variable (passive tracing).
  - If a tracing header was not received, Lambda will generate one for you.
- `AWS_XRAY_CONTEXT_MISSING`
  - X-Ray SDK uses this variable to determine what to do if the function tries to record X-Ray data, but no tracing header is found.
  - Lambda sets this value to `LOG_ERROR` by default.
- `AWS_XRAY_DAEMON_ADDRESS`
  - Exposes the X-Ray daemon's address as `IP_ADDRESS:PORT`.
  - Use the X-Ray daemon's address to send trace data to X-Ray daemon directly, without using the X-Ray SDK.
