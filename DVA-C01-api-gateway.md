# API Gateway

- Scoped at the region level.
- Uses stages deployments and models.
- Can be isolated through VPC endpoints (optional).
- Can proxy HTTP and Lambda backends.

## Deployment

```
deployment (snapshot) <-- stage (dev, test, prod)

stage name: https://{restapi-id}.execute-api.{region}.amazonaws.com/{stageName}
```

## Mapping templates

- Requires use of a Context along with its variables.
- Translates the structure of an HTTP request to backend HTTP or Lambda endpoints.
- Variable types:
  - `$context`
  - `$input`
  - `$stage`
  - `$util`
  - `$method`
  - `$integration`

## Lambda authorizers

Is an API Gateway feature that uses a Lambda function to control access to the API.

useful if you want to implement a custom authorization scheme that uses a bearer token authentication.

When a client makes a request, API Gateway calls your Lambda authorizer, which takes the caller's identity as input and returns an IAM policy as output.

There are two types of Lambda authorizers:

- Token-based - includes a token
- Request parameter-based - puts auth data in headers

Cognito user pool authrizers can also be configured in an API gateway.

## Metrics and troubleshooting

- Sent to CloudWatch.
- Sends metric data to CloudWatch every minute.
- Categories:
  - 4XXError - The number of client-side errors captured in a given period.
  - 5XXError - The number of server-side errors captured in a given period.
  - CacheHitCount - The number of requests served from the API cache in a given period.
  - CacheMissCount - The number of requests served from the backend in a given period, when API caching is enabled.
  - Count - The total number API requests in a given period.
  - IntegrationLatency - The time between when API Gateway relays a request to the backend and when it receives a response from the backend.
  - Latency - The time between when API Gateway receives a request from a client and when it returns a response to the client.
- Dimensions for metrics:
  - ApiName - API with the specified API name.
  - ApiName, Method, Resource, Stage
  - ApiName, Stage
