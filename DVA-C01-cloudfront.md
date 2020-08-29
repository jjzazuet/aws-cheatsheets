# AWS CloudFront

## Use cases

- Distribute content with low latency and high data transfer speeds.
- Pay per use, no allotment commitment.

## Components

- Origins:
  - S3 buckets.
  - EC2 instances.

- Origin Protocol Policy
  - HTTP Only: CloudFront uses only HTTP to access the origin.
  - HTTPS Only: CloudFront uses only HTTPS to access the origin.
  - Match Viewer: CloudFront communicates with your origin using HTTP or HTTPS, depending on the protocol of the viewer request.
    - Caches the object only once even if viewers make requests using both HTTP and HTTPS protocols.
- Viewer Protocol Policy - how viewers access content:
  - HTTP and HTTPS: Viewers can use both protocols.
  - Redirect HTTP to HTTPS: can use both protocols, but HTTP requests are automatically redirected to HTTPS requests.
  - HTTPS Only: can only access your content if they're using HTTPS.

## Content restrictions

- Signed URLs:
  - To restrict access to individual files.
  - When cookies are not supported.
- Signed cookies:
  - Provide access to multiple restricted files.
- Origin access identity:
  - Special CloudFront user identity that can be associated with the distribution to secure some or all S3 content.
- AWS WAF wev ACLs:
  - By IP address.
  - Geo restrictions.

## Links

- https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html
- https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-custom-origin.html#using-https-cloudfront-to-origin-certificate
