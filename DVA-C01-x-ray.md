## AWS X-Ray

## Components

- Uses traces as the main unit of work.
- Uses segments and subsegments.
- Segments connect to form a service graph.
  - Provides visual representation of an application.
  - Connection occurs via a common trace id amongst traces.
  - JSON document, visualized in the console.

## Sampling

- Uses a sampling algorith.
  - By default, trace first request each second, then 5% of additional requests.
  - Trace sampling rate is configurable.

## Filter expressions

- Filter expressions can create groups of traces
- Use annotations to help filter expressions.
  - Segments contain:
    - System defined, or user defined annotations.
- Metadata is similar to annotations, but these are not indexed.
  - Is captured automatically for SQL databases, DynamoDB, SQS and SNS.

## Integration

- Works with EC2, ECS, Lambda, Beanstalk.
  - Needs SDK + agent installed.
  - The X-Ray daemon buffers segments in a queue and uploads to X-Ray in batches.

## Metrics

- Integrates with AWS CloudTrail to record API actions made by a user, role, or AWS service.
- Monitor X-Ray API requests in real time, store logs in:
  - Amazon S3
  - Amazon CloudWatch Logs
  - Amazon CloudWatch Events
- Can use the X-Ray SDK for Java to publish unsampled Amazon CloudWatch metrics from your collected X-Ray segments.
  - Segment start and end time
  - Error, fault and throttled status flags
