## AWS X-Ray

## Components

- Uses segments as the main unit of work. For HTTP, it has:
  - Host
  - Request
  - Response
  - Start, end time, and subsegments.
  - Errors, faults and exceptions.
- Segments can have subsegments.
  - Subsegments are defined for services which do not emit segment data.
- Segments get grouped into Traces.
- Segments connect to form a service graph.
  - Provides visual representation of an application.
  - Connection occurs via a common trace id amongst traces.
  - JSON document, visualized in the console.

## Filter expressions

- Filter expressions can create groups of traces
- Use annotations to help filter expressions.
  - Segments contain:
    - System defined, or user defined annotations.
- Metadata is similar to annotations, but these are not indexed.
  - Is captured automatically for SQL databases, DynamoDB, SQS and SNS.

## Namespaces

- Container for metrics.
- No default namespace. Can be specified when creating a metric.
- Exmaple:
  - `AWS/service`
  - `AWS/EC2`

## API Calls

- `GetTraceSummaries`
- `BatchGetTraces`
- `GetGroup` - group resource details.

## Useful headers

- `X-Forwarded-For` - gets the source client IP.

## Integration

- Four ways to integrate:
  - Active tracing - samples/traces incoming requests.
  - Passive tracing - instruments requests sampled by another service.
  - Request tracing - Adds tracing header to incoming requests, propagates downstream.
  - Tooling - Runs the X-ray daemon to receive segments from the X-Ray SDK.
    - Needs SDK + daemon agent installed.
    - X-Ray Daemon.
    - Runs on port UDP 2000.
    - The X-Ray daemon buffers segments in a queue and uploads to X-Ray in batches.
    - X-Ray SDK uses:
      - Interceptors - for requests directed to the service
      - Client handlers - for other SDKs (i.e. aws cli).
      - HTTP client - for calls to external HTTP api's or services.
- Works with:
  - EC2 - Tooling.
  - ECS - Tooling.
  - Lambda - Active, passive instrumentation.
  - Beanstalk - Tooling.
  - API Gateway - Active, passive instrumentation. Uses sampling rules.
  - ELB - request tracing.
- Sampling rules
  - Can work on the X-Ray SDK with active tracing.
  - TBD how is sampling customized.

## Metrics

- Integrates with AWS CloudTrail to record API actions made by a user, role, or AWS service.
- Monitor X-Ray API requests in real time, store logs in:
  - Amazon S3
  - Amazon CloudWatch Logs
  - Amazon CloudWatch Events
- Can use the X-Ray SDK for Java to publish unsampled Amazon CloudWatch metrics from your collected X-Ray segments.
  - Segment start and end time
  - Error, fault and throttled status flags

## Pricing

- Bill = # of traces recorded retrieved, scanned.
- Max trace size is 500KB.
- Trace data is retained for 30 days at no cost.

https://docs.aws.amazon.com/xray/latest/devguide/xray-concepts.html#xray-concepts-tracingheader
