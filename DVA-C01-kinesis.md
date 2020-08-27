# AWS Kinesis

## Use cases

- Collect and process realtime streaming data.
- Can process large volumes of data.
- Can generate an index on a stream.
- Enforces TLS ecnryption.
- Encrypts data at rest using KMS.

## Components

- Data Producer
  - Emits records, assigning partition keys. PK determine which shard
- Shard
  - Base throughput unit.
  - Unit of streaming capability.
  - Orderd sequence of records.
  - 1000 data records per sec.
  - Ingests 1MB per second.
  - Emits up to 2MB/sec.
- Data Stream
  - Logical group of shards.
  - Data is retained for 24hrs.
  - No limit of shards.
- Data Record
  - Partition key - gets hashed and ssigned to a shard.
  - Data blob

- Video stream
  - Splits into fragments
  - Stored in chunks (contains metadata, fragment # and timestamps).
- Consumers
  - Read data from Kinesis.
- Metadata
  - Described the fragment.

## Integration

- Producer API library (read/write video).
- HTTP Live Streaming
- `GetMedia` API.
- Enhanced fan out - 2MB/second for consumers.

API Calls

- `MergeShards`
- `SplitShards` - used to increase throughput.

> To modify a shard, it must be active.

Errors

- `LimitExceeedeException`
- `ResourceInUseException`
- `ResourceNotFoundException`

## Metrics

## Pricing

- Volume of data consumed.

## Limits
