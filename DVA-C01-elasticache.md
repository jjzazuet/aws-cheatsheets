## AWS Elasticache

## Use cases

- Expensive data retrieval operations.
- Data accessed with high frequency.
- Relatively static data. If rapidly chaning, data where stale copies is tolerable.

## Components

- Base unit of work is an ElastiCache node.
- Nodes run Redis or Memcached engines.
- Configured as EC2 instances with DNS names and access ports.
- Require a maintenance window to be specified.

## Redis engine

- Can cache collections.
- Supports multiple availability zones on read replicas when cluster supports replication.
- Supports in transit and at rest encryption.
- Can be used as data store.
- A group of Redis shards forms a cluster (1 to 90 shards).
- A cluster has a primary node and replicas.
- If a primary node fails with no replicas, data is lost.
- Needs backup and restore to migrate or resize Redis clusters.
  - Can do automatic or manual backups.
- Global data store offers cross-region replication.
- Scales vertically on demand.

## Memcached engine

- Can cache database records.
- Uses automatic node discovery.
- Flexible availability zone placement for nodes and clusters.
- Data does not persist.
- Does not support fail-over or replication.
- Does not support snapshots.
- Supports up to 100 nodes per customer, per region. 1-20 nodes max per cluster.
- Uses endpoint addresses for client connections.
  - Individual nodes have their own endpoints.
  - The whole cluster has a configuration endpoint.
- Access is controlled via security groups.
- Does not support encryption.
- Horizontal scaling does not affect the cluster.
- Vertical scaling requires re-creating the cluster.

## Caching types

- Lazy loading
  - Only requested data gets cached.
  - Can have cache misses.
  - Data may be stale.
- Write-through
  - Adds or updates data in the cache when it's written to the target backend.
  - No stale data.
  - Writes incurr performance penalties (write to backend, then to cache).
  - Cache churn: if most data is never read, wasting resources.

## Integration

- Redis:
  - Uses TLS for in-flight encryption, and KMS customer master keys for at-rest enryption.
  - Can configure optional authentication via Redis AUTH with passwords.

- Both:
  - Uses cache parameter groups to configure either engine (i.e. memory, eviction, storage, etc.).
  - Network access is granted from whitelisted EC2 instances.
  - Use subnet groups or security groups to allow EC2 instance access.
  - Elasticache needs a `cache subnet` group to choose a subnet and IP addresses to associate with nodes.

## Metrics

- Elasticache publishes host and engine metrics every 60 seconds.
- Elasticache events are sent to SNS topics (config, security events, etc.).
- Recommended metrics to monitor:
  - CPUUtilization
  - EngineCPUUtilization
  - SwapUsage
  - Evictions
  - CurrConnections

## Pricing

- On-demand nodes - pay by hour of use, no long term commitment.
- Reserved nodes - one upfront payment for each reserved node from 1 to 3 years. Has discounts on hourly usage.
- 1 Redis snapshot free per Redis cluster. Additional backups are charged.
- Charges when transferring between availability zones of the same region.
