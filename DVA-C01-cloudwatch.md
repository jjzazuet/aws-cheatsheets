## AWS Cloudwatch

## Use cases

- Metrics repository.
- Monitoring resources and applications.
- Display metrics, create alarms, send notifications.
- Makes changes to resources based on thresholds.

## Components

- Namespace - container for metrics.
- Metrics
  - Data lasts for 15 months.
  - High resolution metrics can go down to per-second resolution.
  - Uses the `collectd` daemon.
- Dimensions - Name/value pair for a metric.
- Staticstics
  - Has unit of measure.
  - Sliced by period length
  - Min, max, avg, percentiles, etc.
- Alarms
  - Watch a single metric.
  - Billing alarms.
  - Invoke actions.
  - States: `OK`, `ALARM`, `INSUFFICIENT_DATA`.
  - Needs
    - Period - expressed in seconds.
    - Eval period - 
    - Datapoints to alarm - points that cause a breach.
- Dashboard component - monitors global resources.
- Uses IAM users or roles to grant access.

### CloudWatch Events

- Near-realtime stream that describes changes in resources.
- Can activate functions, make changes, capture state info.
  - Event - indicates a change.
  - Target - processes events.
  - Rules - match events to targets.

### CloudWatch logs

- Monitors logs from:
  - EC2 instances
  - Cloudtrail events.
- Are always kept, never expire.
- Monitor Route 53 DNS queries.
- Allows querying through CloudWatch Log Insights.
- Vended logs:
  - VPC flow log
- Metric filters used to search terms and patterns in log data.
  - Filter pattern - what to look for in the log file.
  - Metric name
  - Metric namespace
  - Metric value
  - Dfault value

## Integration

### CloudWatch Agent

- EC2 instances can install a CloudWatch Agent.
  - Collects more metrics from EC2 intances.

## Limits

- 5 actions per alarm. Can't be changed.
- 10 alarms per month per customer for free. 5000 per region per account.
- 1 million API requests per month per customer.
- Unlimited custom metrics.
- Dashboards
  - 1000 dashboard per account.
  - 100 metrics per dashboard widget.
  - 500 metrics per dashboard.
  - Can't be changed.
- 10 Dimensions per metrics. Can't be changed.
- 1000 SNS notifications per month per customer for free.

## Pricing

- Number of metrics per month.
- 1000 metrics requested with CloudWatch API calls.
- Dashboard per month.
- Alarm metric (standard and high resolution).
- Per GB collected, archived and analized.
- Data transfer out.
- Per million custom events.
- Per million cross-account events.
- On EC2
  - Basic monitoring - Data is available automatically in 5-minute periods at no charge.
  - Detailed monitoring - Data is available in 1-minute periods for an additional charge.
