# API Gateway

- Scoped at the region level.
- Uses stages deployments and models.
- Can be isolated through VPC endpoints (optional).
- Can proxy HTTP and Lambda backends.
- Can import Swagger/OpenAPI

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

## Request proxying

- Programmatically, choose an integration type by setting the `type` property on the Integration resource.
  - Lambda proxy integration is `AWS_PROXY`.
  - Lambda custom integration and all other AWS integrations, it is `AWS`.
  - HTTP proxy integration - `HTTP_PROXY`.
  - HTTP integration - `HTTP`.
  - Mock integration - `MOCK`.

## Lambda authorizers

Is an API Gateway feature that uses a Lambda function to control access to the API.

useful if you want to implement a custom authorization scheme that uses a bearer token authentication.

When a client makes a request, API Gateway calls your Lambda authorizer, which takes the caller's identity as input and returns an IAM policy as output.

There are two types of Lambda authorizers:

- Token-based - includes a token
- Request parameter-based - puts auth data in headers

Cognito user pool authrizers can also be configured in an API gateway.

## Integration

Errors associated with HTTP 504:

- INTEGRATION_FAILURE - gateway integration failed. If response type is unspecified, defaults to `DEFAULT_5XX`.
- INTEGRATION_TIMEOUT - gateway integration timed out. If response type is unspecified, defaults to `DEFAULT_5XX`.

Integration timeout range is from 50 milliseconds to 29 seconds for all integration types:
 - Lambda, Lambda proxy.
 - HTTP, HTTP proxy.
 - AWS integrations.


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

## Links

- https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-integration-types.html
