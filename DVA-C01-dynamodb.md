# AWS DynamoDB

- Highly scalable NoSQL database.
- Multi-master nodes in each region ensure eventually consistent data access.
- Allows 256 tables per region.
- 32 levels of JSON nesting.
- Connects via HTTPS with TLS certificates.
- An EC2 instance can connect directly to DynamoDB via a VPC endpoint.
- Global tables as multi-master region replicas.

## Keys and indexes

- Partition key values can't exceed 10GB.
- Primary key with onle single attribute.
- Composite primary keys with one primary key and one sort key.
- Local secondary indexes (max 5 per table) share the same primary key with the table.
    - Shares read and write throughput capacity with the base table.
    - Provides strong consistency in query results.
- Global secondary indexes (max 20) have a different partition key.
  - Has no size limit.
  - Has its own read and write capacity.
  - Support eventual consistency only.

To avoid potential throttling, the provisioned write capacity for a global secondary index should be equal or greater than the write capacity of the base table since new updates will write to both the base table and global secondary index.

## Queries

- On top of the primary key.
- On top of secondary indexes.

## DynamoDB streams

- Events are based on items:
  - Create, update, delete.
  - Events live for only 24hrs.
- Grouped into shards.
- Streams allows integration with Lambda triggers.
  - Lambda pools the DynamoDB stream from shards every 4 seconds.
- When an item in the table is modified, `StreamViewType` determines information written to the stream.
  - Valid values - `KEYS_ONLY`, `NEW_IMAGE`, `OLD_IMAGE`, and `NEW_AND_OLD_IMAGES`.

## Read consistency

- Eventual by default, reads may not reflect the latest view of the data.
- It can optionally be strongly consistent, sacrifies availability.

## Capacity units

- Read capacity: 1 unit = 4KB per second (1 strong consistent read, 2 eventual consistent reads).
- Write capacity: 1 unit = 1KB per second.
- Transactional
  - Read requests - 2 RCUs.
  - Write requests - 1 WCUs.

## API calls

To create, update, or delete an item in a DynamoDB table, use one of the following operations:

- `PutItem`
- `UpdateItem`
- `DeleteItem`

To return the number of write capacity units consumed by any of these operations, set the `ReturnConsumedCapacity` parameter to one of the following:

- `TOTAL` — returns the total number of write capacity units consumed.
- `INDEXES` — returns the total number of write capacity units consumed, with subtotals for the table and any secondary indexes that were affected by the operation.
- `NONE` — no write capacity details are returned. (This is the default.)

## Error handling

- Throws only 400 (throttling) and 500 (server errors) HTTP status codes.

## Throughput

- Auto scaling.
  - Driven by target utlization percentage.
  - It doesn't throttle.
  - It can be configured with scaling policies for tables or global secondary indexes.
- Reserved capacity.
  - Fixed capacity which does throttle.
- On demand.
  - Pay for what you use.

## Items

- Can provide atomic counters.
- Can have conditional write for item attributes (put, update, delete).

## Expressions and Queries

- Queries are projections.
- Projections use the `#` character as a substitute for an attribute.
- Can be uued for put, update, delete.
- Can read at most 1MB of data.
- Can use filtering and limit.

A query consists of:

- Primary key equality.
- Sort key range.
- Filter expression.
- Limit count.
- Pagination.

Scans:

- Are similar to queries.
- Are eventually consistent by default.

## Record locking

- Optimistic locking - uses a version number to prevent stale writes.
- Pessimistic lock with read locking - others cannot read object while in memory.
- Pessimistic lock with write locking - others cannot write object while in memory.
  - Last writer wins.

## Backup/Restore

- Recorded in CloudTrail
- NOTE: They lock tables.
- Can introduce skew values.

## Encryption & authentication

- Can only be configured at creation time of table.
- Encrypts everything.
- DynamoDB tables can be accessed via IAM policies of STS tokens.

## Monitoring

- Cloudwatch alarms.
- Cloudwatch Logs.
- Cloudwatch Events.
- CloudTrail Monitoring.

## DAX

- Im=memory caching, microsecond response.
- Can save on read capacity units.
- Not good for strongly consistent reads.
- Not good for intensive writes, good for intensive reads.
- Horizontal or vertical scaling (requires new cluster setup).

## Capacity scaling

- Hot partitions provide adaptive capcity to avoid throttling.
- Burst capacity give flexibility on partition reads.

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SecondaryIndexes.html
