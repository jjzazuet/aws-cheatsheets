## AWS S3

- an Origin Access Identity (OAI) is incorrect because and OAI is just a special CloudFront user which you associate with your origins. This is primarily used to secure all or just specific items in your Amazon S3 content.

https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-policy.html
https://docs.aws.amazon.com/AmazonS3/latest/dev/S3_ACLs_UsingACLs.html

## Methods of encryption

- Fully managed AWS encryption with default KMS key(SSE-KMS).
  - `x-amz-server-side-encryption` = `aws:kms`
- Server side encryption with customer provided key(SSE-C)
  - `x-amz-server-side-encryption-customer-algorithm`
  - `x-amz-server-side-encryption-customer-key`
  - `x-amz-server-side-encryption-customer-key-md5`

  
