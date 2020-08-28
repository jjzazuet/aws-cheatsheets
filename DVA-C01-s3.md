## AWS S3

- an Origin Access Identity (OAI) is incorrect because and OAI is just a special CloudFront user which you associate with your origins. This is primarily used to secure all or just specific items in your Amazon S3 content.

https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-policy.html
https://docs.aws.amazon.com/AmazonS3/latest/dev/S3_ACLs_UsingACLs.html

## Methods of encryption

- Fully managed AWS encryption (SSE-KMS).
  - `x-amz-server-side-encryption`
  - `x-amz-server-side-encryption-aws-kms-key-id`
- Server side encryption with customer provided key
  - `x-amz-server-side-encryption-customer-algorithm`
  - `x-amz-server-side-encryption-customer-key`
  - `x-amz-server-side-encryption-customer-key-md5`

Take note that `kms:Decrypt` is only one of the actions that you must have permissions to when you upload or download an Amazon S3 object encrypted with an AWS KMS key. You must also have permissions to `kms:Encrypt`, `kms:ReEncrypt*`, `kms:GenerateDataKey*`, and `kms:DescribeKey` actions.

## Data Retrieval

There are three options for retrieving data with varying access times and cost:

- Standard retrievals allow you to access any of your archives within several hours. Standard retrievals typically complete within 3–5 hours. This is the default option.

- Bulk retrievals are Glacier’s lowest-cost retrieval option, which you can use to retrieve large amounts, even petabytes, of data inexpensively in a day. Bulk retrievals typically complete within 5–12 hours.

- Expedited retrievals allow you to quickly access your data when occasional urgent requests for a subset of archives are required. Expedited retrievals are typically made available within 1–5 minutes.

## Data Replication

To enable the cross-region replication feature in S3, the following items should be met:

- The source and destination buckets must have versioning enabled.
- The source and destination buckets must be in different AWS Regions.
- Amazon S3 must have permissions to replicate objects from that source bucket to the destination bucket on your behalf.

## Transfer Acceleration

Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and your Amazon S3 bucket. Transfer Acceleration leverages Amazon CloudFront’s globally distributed AWS Edge Locations. As data arrives at an AWS Edge Location, data is routed to your Amazon S3 bucket over an optimized network path. 

## Cross Domain Request Sharing

A CORS configuration is an XML file that contains a series of rules within a <CORSRule>. A configuration can have up to 100 rules. A rule is defined by one of the following tags:

- `AllowedOrigin` - Specifies domain origins that you allow to make cross-domain requests.
- `AllowedMethod` - Specifies a type of request you allow (GET, PUT, POST, DELETE, HEAD) in cross-domain requests.
- `AllowedHeader` - Specifies the headers allowed in a preflight request.

Below are some of the CORSRule elements: 
- `MaxAgeSeconds`  - Specifies the amount of time in seconds (in this example, 3000) that the browser caches an Amazon S3 response to a preflight OPTIONS request for the specified resource. By caching the response, the browser does not have to send preflight requests to Amazon S3 if the original request will be repeated.
- `ExposeHeader`  - Identifies the response headers (in this example, x-amz-server-side-encryption, x-amz-request-id, and x-amz-id-2) that customers are able to access from their applications (for example, from a JavaScript XMLHttpRequest object).
